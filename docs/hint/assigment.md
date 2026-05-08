# Undergraduate Graduation Project (Thesis) Assignment
## School of Cyber Space Security

### Basic Information
| Item | Content |
| :--- | :--- |
| **English Title** | Design and Implementation of Vulnerability Static Detection Tool for MCP Programs |
| **Project Type** | Engineering Practice |
| **Project Source** | Not derived from scientific research projects |

## Main Research Content
MCP (Model Context Protocol) is an open communication protocol promoted by OpenAI and other institutions. It enables free interconnection among different AI models, plugins, applications and toolchains, significantly improving the automation capability of AI systems while expanding the attack surface simultaneously. At present, security research on MCP is insufficient, large-scale vulnerability detection tools are scarce, and there exists an obvious security protection gap.

This project investigates MCP-related vulnerability characteristics and analyzes the limitations of existing static detection tools, aiming to design and implement a static detection tool for common vulnerabilities in MCP programs. It fills the blank of detection tools in the MCP field and provides technical support for MCP ecosystem security. The main research contents are as follows:
1. **Security Risk Investigation and Vulnerability Feature Summarization of MCP Programs**
Collect and sort typical MCP vulnerabilities and insecure implementation cases from public resources including CVE databases, security reports and open-source MCP projects, such as insecure tool registration, excessive permission operation, missing input validation, and unrestricted resource access. Summarize triggering modes and code pattern features to build a vulnerability pattern library for static detection.

2. **Investigation of Existing Static Detection Technologies and Tools**
Research static analysis libraries in Python/TypeScript ecosystems (e.g., Bandit, Semgrep, ESLint, PyLint). Analyze their rule systems, scalability and adaptability to MCP projects, and confirm reusable components and technical routes for this tool.

3. **Design of Lightweight Static Detection Method**
Design a lightweight static detection method applicable to MCP projects based on existing analysis libraries, including code structure parsing, basic data/control flow inspection and rule matching. Focus on detecting common implementation flaws such as unchecked user input, insecure file operations and unrestricted tool calls.

4. **Design and Implementation of Static Detection Tool**
Develop a runnable MCP program static detection tool using Python or TypeScript. The tool supports project scanning, pattern-based vulnerability detection and structured report output, including vulnerability type, risk location and corresponding code line numbers for typical vulnerability patterns.

5. **Tool Testing and Optimization**
Test detection performance using multiple real MCP sample projects (including normal and defective cases). Analyze false positives and false negatives, adjust detection rules and optimize tool usability.

6. **Graduation Thesis Compilation and Defense**
Conduct comprehensive literature research to evaluate the rationality and innovation of the topic. Clarify the design principle, implementation details and test results of the static detection tool in progress report. Systematically summarize research background, methods and experimental results in the thesis, and analyze practical value and improvement space of the tool. Prepare defense materials (thesis, tool demo, PPT) and complete graduation defense.

## Technical Requirements
1. **Vulnerability Investigation Requirement**
Collect no less than 6 typical security risks or insecure implementation modes of MCP programs, and form vulnerability feature descriptions including trigger conditions, risk explanations and basic code examples.

2. **Static Analysis Technology Investigation Requirement**
Research at least 2 static detection frameworks applicable to Python/TypeScript, compare their rule systems, detection capability and scalability, and clarify the technical selection rationale for this project.

3. **Detection Method Requirement**
Propose a implementable and extensible lightweight detection scheme, including definition of common MCP vulnerability rules, inspection strategies (AST matching, string pattern matching, basic data flow analysis) and complete detection workflow (input-analysis-output). The scheme shall be directly deployable in tool development.

4. **Tool Development Requirement**
- Development language: Python or TypeScript (optional)
- Core functions: Code scanning and parsing, identification of typical vulnerability patterns, structured detection result output (JSON/HTML format supported)

5. **Testing and Optimization Requirement**
Construct or collect MCP test cases and conduct no less than two rounds of testing. Record and analyze false positive and false negative problems, and complete targeted optimization.

## Main References
1. OpenAI. Model Context Protocol (MCP) Specification. 2025.
2. Wang B, et al. MCPGuard: Automatically Detecting Vulnerabilities in MCP Servers. arXiv:2510.23673, 2025.
3. Yan B, et al. MCP Does Not Stand for Misuse Cryptography Protocol: Uncovering Cryptographic Misuse in MCP Implementations at Scale. arXiv:2512.03775, 2025.
4. Wang Z, et al. MPMA: Preference Manipulation Attack Against Model Context Protocol. arXiv:2505.11154, 2025.
5. Yang Y, et al. MCPSecBench: A Systematic Security Benchmark and Playground for Testing Model Context Protocols. arXiv:2508.13220, 2025.
6. Zhao S, et al. Mind Your Server: A Systematic Study of Parasitic Toolchain Attacks on the MCP Ecosystem. arXiv:2509.06572, 2025.
7. Wang Z, et al. MindGuard: Tracking, Detecting, and Attributing MCP Tool Poisoning Attacks via Decision Dependence Graph. arXiv:2508.20412, 2025.
8. Shivashankar K, Martini A. PyExamine: A Comprehensive, UnOpinionated Smell Detection Tool for Python. arXiv:2501.18327, 2025.
9. Li L, et al. Scalpel: The Python Static Analysis Framework. arXiv:2202.11840, 2022.
10. Ruohonen J, et al. A Large-Scale Security-Oriented Static Analysis of Python Packages in PyPI. arXiv:2107.12699, 2021.

## Schedule Arrangement
1. **Stage 1**: Literature review of MCP protocol and static analysis technology; summarize static-detectable vulnerability patterns of MCP programs; investigate Python/TypeScript static analysis tools and determine technical route; complete and submit proposal report.
2. **Stage 2**: Design static detection methods (AST rules, matching logic) for MCP vulnerabilities; build MCP test set (normal & vulnerable samples); develop core modules including AST parsing, rule matching and result output; complete debugging and local testing.
3. **Stage 3**: Improve vulnerability rule library; conduct multiple scanning tests on prototype tool; analyze false positives/false negatives and evaluate scanning speed & detection accuracy; submit mid-term progress report and complete mid-term inspection.
4. **Stage 4**: Conduct in-depth experiments and tool iteration; complete main body of graduation thesis; realize report visualization (JSON/Markdown output); improve rule accuracy; carry out comparative experiments with existing static analysis tools and analyze experimental results.
5. **Stage 5**: Revise and polish the thesis according to supervisor’s requirements to meet defense standards; prepare defense PPT and tool demonstration materials.
6. **Stage 6**: Complete undergraduate graduation defense.
