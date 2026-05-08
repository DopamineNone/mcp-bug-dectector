# Undergraduate Graduation Project Mid-term Progress Check Form

### Basic Information
**English Title**：Design and Implementation of a Vulnerability Detection Tool for MCP Programs

---

## Completed Tasks So Far
### 1. Overall Progress Overview
Focusing on the emerging **Model Context Protocol (MCP)** in the LLM ecosystem, this project targets its security protection gaps such as ambiguous permission boundaries and opaque tool invocation chains. A dual-engine detection tool integrating **SAST static analysis** and **LLM semantic analysis** has been systematically designed and implemented.

Completed phased achievements:
1. **Theoretical Risk Modeling**: Audited MCP official specifications and open-source Server projects, established cognition covering code-level vulnerabilities (injection, privilege escalation) and semantic-level risks (tool poisoning, hijacking).
2. **Core Architecture Implementation**: Built a prototype tool with a six-layer decoupled architecture, realized cross-engine reuse of AST (Abstract Syntax Tree) based on a unified parser.
3. **Key Module Breakthrough**: Implemented intra-procedural taint analysis path taking MCP tool input parameters as taint sources; completed interface development of semantic detector based on local LLM.

The project is currently at the key transition stage from **prototype verification** to **engineering improvement**. The follow-up work will focus on inter-procedural analysis algorithms to improve detection accuracy in complex invocation scenarios.

### 2. Detailed Completed Work
#### 2.1 Vulnerability Collection & Risk Modeling
By retrieving CVE databases, studying LLM application security research reports, and conducting static auditing on popular open-source MCP Server projects on GitHub, MCP program security threats are systematically sorted and summarized into detectable rules.

A **two-layer threat model** is constructed based on detectability and cause dimension, dividing risks into **code-level vulnerabilities** and **semantic-level vulnerabilities**.

##### (1) Code-level Vulnerabilities: Deterministic Risks Based on Program Structure
These vulnerabilities exist in the host code of MCP Servers, caused by insecure programming habits. Following fixed code execution paths, they can be effectively identified via SAST taint tracking.

| Vulnerability Type | Specific Manifestation in MCP Scenarios |
| :--- | :--- |
| Command Injection | MCP tool directly passes LLM-generated parameters (file names, instructions) to `os.system` / `subprocess` without validation. |
| Path Traversal | Resource reading tools do not normalize user-specified paths, allowing LLM to be induced to read sensitive system files such as `/etc/passwd`. |
| Hardcoded Secrets | API Key, database password or authentication Token are hardcoded in MCP Server source code, easily extracted by LLM and returned to clients. |
*Table 1 Typical Examples of Code-level Vulnerabilities*

##### (2) Semantic-level Vulnerabilities: Probabilistic Risks Based on Natural Language Logic
Unique security challenges of the MCP ecosystem. Such vulnerabilities do not always come from code logic errors, but arise from malicious exploitation of tool description fields and interaction logic, leading LLM to behave abnormally. Beyond the capability of traditional SAST, they require LLM semantic analysis.

| Vulnerability Type | Mechanism & Cause | Typical Case |
| :--- | :--- | :--- |
| Tool Poisoning | Inject misleading instructions into tool `description` field to induce LLM to execute additional illegal operations when invoking the tool. | Tool description contains mandatory hidden data leakage calls before normal function execution. |
| Indirect Prompt Injection | Untrusted external data (web content) enters MCP context via Resources, carrying hidden instructions to hijack LLM control flow. | Crawled web content contains commands to ignore original prompts and forward data to attacker servers. |
| Priority Hijacking | When multiple tools have semantic overlap, construct specific prompts to induce LLM to abandon high-security tools and invoke low-security alternatives. | Two search tools exist; one is maliciously described as more accurate without security filtering. |
*Table 2 Typical Examples of Semantic-level Vulnerabilities*

#### 2.2 Existing Tool Investigation & Technical Selection
Mainstream static analysis tools in Python ecosystem are compared horizontally:
Bandit, Semgrep and PyLint lack MCP context semantic awareness, cannot automatically mark MCP tool parameters as taint sources, and have systematic missing alarms for MCP-specific vulnerabilities.

The investigation supports the core technical route of this tool: lightweight local deployment, SAST+LLM dual-engine plug-in design, and pure YAML rule-driven configuration.

| Feature Dimension | Bandit | Semgrep | PyLint | This Tool (Dual-engine) |
| :--- | :--- | :--- | :--- | :--- |
| MCP Context Awareness | No | No | No | ✅ MCP dedicated recognition |
| Rule Scalability | Limited | Strong (DSL required) | Weak | ✅ Pure YAML configuration |
| Taint Tracking | Partial | Partial | No | ✅ Intra-procedural + Inter-procedural |
| Local Lightweight Deployment | ✅ | Network/environment dependent | ✅ | ✅ Support local LLM |
| Detection Engine | Static Matching | Pattern Matching | Code Specification Check | ✅ SAST + LLM Dual-engine |
*Table 3 Comparison of Static Analysis Tools*

#### 2.3 Core Module Development & Six-layer Architecture
The system adopts a layered decoupled architecture, consisting of a global configuration layer and six core processing layers with clear responsibilities.

- **Global Configuration Layer**: Act as the system hub, driven by YAML to provide unified runtime context; manage detection switches, LLM API keys and rule loading paths, decoupling scanning behavior from business logic.
- **L0 File Traversal Layer**: Implement file system walking, source encoding recognition, and deliver raw Python files to the unified parser.
- **L1 Unified Parsing Layer**: Core foundation of the tool. Parse source code once to generate globally shared objects including AST and CFG; extract structured MCP metadata such as `@tool` / `@resource` decorators; support dual-engine reuse to avoid repeated parsing and reduce memory overhead.
- **L2 Registration & Plugin Management Layer**: Manage full lifecycle of detector plugins; support dynamic loading without recompilation; classify detectors into `SASTDetector` for code structure and `LLMDetector` for semantic logic.
- **L3 Execution Layer**: Core computing layer supporting parallel scheduling. Run AST-based SAST analysis and LLM prompt rendering simultaneously; SAST engine implements pattern matching, intra-procedural taint analysis and missing validation detection; LLM engine invokes local models via abstract interfaces for semantic risk assessment.
- **L4 Result Aggregation Layer**: Deduplicate and reconcile raw outputs from multiple detectors; merge confidence scores; standardize results into unified `Finding` objects with 11 fixed fields including severity level, CWE ID and repair suggestions.
- **L5 Report Output Layer**: Support template-based multi-format export; compatible with **JSON** (automation integration) and **Markdown** (manual audit and reading).

> Figure 1 Six-layer Architecture Diagram

##### SAST Static Analysis Engine
As the core component for deterministic code-level vulnerability detection, it integrates three complementary analysis paradigms driven by external YAML rules:
1. **AST Pattern Matching**: Traverse AST via Visitor mode, identify hardcoded secrets and dangerous API calls; avoid interference from comments and invalid strings to reduce false positives.
2. **Taint Tracking**: Automatically mark `@tool` function input as taint source; track variable pollution propagation; trigger alarms when tainted data flows into sensitive sinks such as `os.system`, `subprocess.run` and `open`. Intra-procedural analysis is fully implemented; inter-procedural cross-function analysis is under optimization.
3. **Missing Validation Detection**: Check whether MCP tool parameters pass predefined sanitizer functions before sensitive operations; identify missing input validation and unauthorized access risks.

##### LLM Semantic Detection Engine
Solve MCP-specific semantic blind spots beyond traditional SAST such as tool poisoning and semantic conflict. Adopt adapter pattern to achieve model neutrality, seamlessly connecting Ollama, DeepSeek, Llama and remote OpenAPI services. Support three analysis granularities: single tool analysis, prompt template analysis and cross-tool global analysis.

Introduce confidence control to suppress LLM hallucination: set a threshold of 0.7; only generate alarm records when model self-evaluation confidence exceeds the threshold.

##### Unified Result Aggregation
Unify output protocols of SAST and LLM engines in L4 layer. All results are normalized into standard objects with unified engine source, severity, confidence, code line number, CWE ID and repair suggestions, facilitating unified security audit.

### 3. Preliminary Experimental Results
The tool prototype completes end-to-end scanning workflow: automatic file traversal, parsing, rule matching and report generation for Python projects. Preliminary test results show that the detection recall rate of command injection vulnerabilities reaches about **80%**, and the overall false positive rate is within an acceptable range, verifying basic detection capability.

---

## Progress Compliance
Compliant with the schedule specified in the assignment task: **Yes ☑ No □**

---

## Remaining Tasks
1. Complete engineering implementation of **inter-procedural taint tracking** for SAST detector; realize limited-depth cross-function parameter propagation based on call graph to eliminate missing alarms.
2. Expand test set scale, conduct multiple rounds of systematic scanning; count false positive and false negative data, optimize rule thresholds and matching logic.
3. Compile preliminary performance evaluation report with key indicators such as detection accuracy.
4. Conduct in-depth experiments and iteration, complete main body of graduation thesis, optimize report visualization and analyze experimental results.

---

## On-time Completion Evaluation
Can complete the graduation project on schedule: **Yes ☑ No □**

---

## Existing Problems & Solutions
### Existing Problems
1. Cross-function taint propagation analysis is unfinished; vulnerabilities via intermediate variables or helper function transfer still cause missing alarms.
2. Rule library needs further expansion; insufficient rule coverage for MCP resource processing and indirect prompt injection auxiliary paths.

### Proposed Solutions
1. For inter-procedural taint analysis: implement call-graph based analysis in the next stage; give priority to single-layer function invocation scenarios, then expand to multi-layer recursion.
2. For rule library expansion: systematically sort MCP official security announcements and community vulnerability cases; supplement rule entries by vulnerability category and verify effectiveness with standardized test sets.
