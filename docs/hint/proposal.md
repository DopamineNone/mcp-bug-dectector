# Undergraduate Graduation Project Proposal Report
## Basic Information
**English Title**：Design and Implementation of a Vulnerability Static Detection Tool for MCP Programs

---

## 1. Research Background and Significance
With the rapid development of artificial intelligence technology, **MCP (Model Context Protocol)** is an open communication protocol promoted by OpenAI and other institutions. It realizes free interconnection among different AI models, plugins, applications and toolchains, greatly improving the automation capability of AI systems and being widely adopted in various AI application scenarios.

However, its highly interconnected feature significantly expands the attack surface of AI systems and brings growing security risks. The core components of the MCP ecosystem include **MCP Host, MCP Client, MCP Server**, supporting interaction with local file systems, IDEs, databases, Web APIs and AI tools over network transport layers. Typical MCP interaction mechanisms cover notification, sampling, tool invocation, resource access and prompt delivery.

At present, security research targeting MCP is still in the initial stage, and dedicated large-scale vulnerability detection tools for MCP programs are extremely scarce, resulting in an obvious security protection gap in the MCP ecosystem. Most existing static detection tools are designed for general-purpose programs, lacking adaptation to MCP’s unique architecture and interaction logic, and cannot effectively identify MCP-specific vulnerabilities such as insecure tool registration and excessive privilege operation.

This project aims to design and implement a dedicated static detection tool for common vulnerabilities in MCP programs, filling the research and tool blank in this field. The research can provide technical support for the secure development of MCP applications, help developers discover and fix vulnerabilities timely, ensure stable operation of AI systems, and improve the security protection system of the MCP ecosystem. It also promotes the secure large-scale deployment of MCP technology, possessing important theoretical research value and practical application significance.

> Figure 1: MCP Protocol Architecture Diagram

---

## 2. Main Research Contents & Key Problems to Be Solved
### 2.1 Main Research Contents
1. **Security Risk Investigation and Vulnerability Feature Summarization of MCP Programs**
Collect and sort typical MCP vulnerabilities and insecure implementation cases from CVE databases, security reports and open-source MCP projects. Summarize vulnerability triggering patterns and code feature characteristics, and construct a vulnerability pattern library for static detection.

2. **Investigation of Existing Static Detection Technologies and Tools**
Research mainstream static analysis libraries in Python/TypeScript ecosystems (Bandit, Semgrep, ESLint, PyLint, etc.). Analyze their rule mechanism, scalability and adaptability to MCP projects, and determine reusable components and overall technical route for the tool.

3. **Design of Lightweight Static Detection Method**
Design a lightweight static detection solution tailored for MCP projects based on existing analysis frameworks, including code structure parsing, basic data/control flow inspection and rule matching strategies, focusing on detecting common insecure implementation flaws in MCP development.

4. **Design and Implementation of Static Detection Tool**
Develop a runnable MCP program static detection tool with Python or TypeScript. Core capabilities include project code scanning, rule-based vulnerability matching and detection, and structured detection report output to identify typical MCP vulnerability patterns accurately.

5. **Tool Testing and Optimization**
Adopt multiple real MCP sample projects (normal samples + vulnerable samples) to verify detection performance. Analyze false positives and false negatives, adjust detection rules iteratively, and optimize tool usability and stability.

6. **Graduation Thesis Writing and Defense Preparation**
Systematically summarize research contents, technical methods and experimental results, complete thesis compilation, prepare defense materials and participate in graduation defense.

### 2.2 Key Problems to Be Solved
1. Comprehensively sort out security risks of MCP programs, extract representative vulnerability features, and build a complete vulnerability pattern library to support static detection.
2. Design a lightweight detection method adapted to MCP architectural characteristics based on existing static analysis technologies, balancing detection efficiency and accuracy.
3. Implement core functions of the tool to support efficient scanning of MCP projects, accurate vulnerability rule matching, and output clear and detailed detection reports.
4. Adopt a reasonable testing scheme to discover tool defects, reduce false positive and false negative rates, and improve tool practicability and reliability.

---

## 3. Research Methods and Implementation Measures
### 3.1 Research Methods
1. **Literature Research Method**
Extensively review MCP official specifications, security vulnerability research reports, static detection technology papers and official documents of mainstream SAST tools. Master MCP technical architecture, current security status, research progress and technical trends of static analysis.

2. **Case Analysis Method**
Collect vulnerability and insecure implementation cases from CVE databases and open-source MCP projects. Conduct in-depth analysis on vulnerability trigger conditions, code features and risk impacts, providing support for constructing the vulnerability pattern library.

3. **Comparative Research Method**
Compare multiple static analysis libraries in Python/TypeScript ecosystems from the dimensions of rule system, scalability and scenario adaptability, analyze their advantages and disadvantages, and determine technical selection and reusable components for the project.

4. **Engineering Implementation Method**
Select Python or TypeScript as the development language. Based on the chosen static analysis framework, design and implement core modules of the MCP static detection tool, including code scanning & parsing, rule matching and result output.

5. **Test Verification Method**
Construct an MCP test set containing both normal and vulnerability-implanted samples. Conduct multiple rounds of testing on the prototype tool, verify performance indicators such as detection accuracy and scanning speed, and analyze the causes of false positives and false negatives.

### 3.2 Implementation Measures
1. **Systematic Preliminary Investigation**
Sort out MCP official protocol specifications, open-source ecosystem documents and security incident bulletins. Analyze MCP message interaction mode, service resource structure and tool invocation mechanism, clarify security boundaries and potential attack surfaces. Meanwhile, review domestic and international research on static analysis, including Python/TypeScript language features, AST abstract syntax tree, code pattern matching, taint analysis and rule-based detection framework. Establish theoretical foundation for tool modeling, form structured literature overview, clarify research gaps in MCP ecosystem security, and verify the research hypothesis that MCP vulnerabilities can be effectively identified via rule-based static analysis.

2. **Construction of MCP Vulnerability Knowledge Base**
Extract real risk samples from MCP source code, demo programs, security papers, community reports and CVE records. Refine common vulnerability characteristics through source code structure analysis, and establish a standardized structured vulnerability description system covering vulnerability cause, trigger condition, AST features, context dependency, false positive source and severity level. Classify MCP vulnerabilities into categories such as command execution risk, resource access out-of-bounds, missing input validation and file system exposure, forming a theoretical classification framework for MCP static vulnerability research.

3. **Modular Tool Architecture Design**
Adopt a modular development architecture for the detection tool, divided into three core modules:
- **AST Parsing Module**: Perform syntax decomposition and static structure extraction on Python/TypeScript MCP project files.
- **Rule Matching Module**: Realize syntax structure mapping based on node relationships to execute vulnerability pattern detection.
- **Risk Assessment Module**: Score risks by integrating vulnerability matching strength and context correlation, and output interpretable detection reports.

> Figure 2: Flowchart of MCP Vulnerability Static Detection Technology

4. **Establishment of Verification and Evaluation System**
Build a standardized test dataset including normal MCP demo projects and manually implanted vulnerability samples. Evaluate tool performance via false positive rate, false negative rate and detection coverage. Analyze detection bottlenecks such as false positive sources, rule conflicts and context missing, and optimize rule design in tool iteration.
