# Secure Coding Guardian

### A security-focused coding Skill for Claude Code

**Secure Coding Guardian** helps Claude Code write, review, and improve **more secure Python, C, and C++ code**.

It is designed for developers who use AI-assisted development and want security to be part of the coding process — not something that happens only after the application is finished.

Instead of simply looking for known vulnerabilities, Secure Coding Guardian first tries to understand **what the project is, how it works, what can be attacked, and what security risks matter for that specific application**.

It then uses that context to guide implementation, review code, identify vulnerabilities, recommend or apply fixes, run available security checks, create security regression tests, and provide a final security assessment.

---

## What Does It Actually Do?

Imagine you are building a Python API with Claude Code.

Normally, you might ask:

```text
Build a user registration endpoint.
```

Claude writes the code.

With Secure Coding Guardian, security becomes part of the development process.

The Skill can reason about questions such as:

- Is user input validated?
- Can the endpoint be abused?
- Is authentication required?
- Is authorization actually enforced?
- Can one user access another user's data?
- Is the database query safe?
- Can an attacker inject commands or SQL?
- Are passwords stored safely?
- Are tokens or secrets exposed?
- Can an uploaded file escape its intended directory?
- Can an external URL be abused for SSRF?
- Can the endpoint be used for denial of service?
- Are errors exposing sensitive information?
- Are dependencies introducing known vulnerabilities?

The goal is not simply to report:

```text
Potential vulnerability found.
```

The goal is to help move the code toward:

```text
Identify the risk
        ↓
Understand why it is dangerous
        ↓
Fix the underlying problem
        ↓
Add a regression test when possible
        ↓
Verify the fix
```

---

# Why Does This Exist?

AI-assisted coding makes software development dramatically faster.

But faster code generation can also mean:

- Security assumptions are missed.
- Authentication is implemented but authorization is forgotten.
- User input is trusted accidentally.
- Dangerous APIs are used without understanding their risks.
- Dependencies are added without security review.
- Error handling leaks sensitive information.
- File and process operations become exploitable.
- C and C++ memory-safety problems are introduced.
- Security fixes are made without regression tests.

Secure Coding Guardian is designed to add a **security-aware layer to AI-assisted development**.

It treats generated code as code that must be reviewed — not code that is automatically trusted.

---

# What Makes It Different?

Secure Coding Guardian is **not just a vulnerability scanner**.

A traditional scanner might look for patterns such as:

```text
eval(...)
shell=True
strcpy(...)
unsafe API usage
```

Those checks are useful, but they do not always understand why the code exists or how the application works.

Secure Coding Guardian tries to understand the project first.

For example:

```text
Repository
    ↓
Application Type
    ↓
Language / Framework
    ↓
Entry Points
    ↓
Trust Boundaries
    ↓
Attack Surface
    ↓
Threat Model
    ↓
Security Rules
    ↓
Implementation Review
    ↓
Security Testing
    ↓
Security Gate
```

This allows security analysis to be **context-aware**.

A local CLI application does not need the same security review as an internet-facing API.

A C++ network parser does not need the same priorities as a Django application.

A Python application that executes local commands has a different threat model from a Python data-processing script.

The Skill adapts its security focus accordingly.

---

# What Can It Help With?

## Python

Secure Coding Guardian can review and help secure Python applications against issues such as:

- Command injection
- SQL injection
- NoSQL injection
- LDAP injection
- SSRF
- XSS
- SSTI
- CSRF
- Broken authentication
- Broken authorization
- IDOR / BOLA
- Unsafe deserialization
- `pickle` misuse
- Unsafe YAML loading
- `eval()` / `exec()` risks
- Path traversal
- Arbitrary file access
- Unsafe file uploads
- Symlink attacks
- Temporary-file vulnerabilities
- Weak cryptography
- Insecure randomness
- Secret leakage
- ReDoS
- Resource exhaustion
- Race conditions
- Unsafe subprocess execution
- Insecure configuration
- Dependency vulnerabilities

Framework-aware analysis can be applied where relevant to technologies such as:

- Django
- Flask
- FastAPI
- Starlette

---

# C and C++ Security

For C and C++, the Skill places strong emphasis on **memory safety, undefined behavior, input handling, and native attack surfaces**.

It can review for:

- Buffer overflows
- Out-of-bounds access
- Use-after-free
- Double-free
- Invalid memory access
- Null-pointer dereferences
- Uninitialized memory
- Memory leaks
- Integer overflow
- Integer truncation
- Signed/unsigned conversion problems
- Format-string vulnerabilities
- Undefined behavior
- Race conditions
- TOCTOU
- Unsafe parsing
- Command execution
- Path traversal
- Unsafe filesystem operations
- Privilege-boundary problems
- Unsafe dynamic loading
- Serialization problems
- Resource exhaustion

For C++, it additionally reviews areas such as:

- Ownership
- RAII
- Smart pointers
- Dangling references
- Iterator invalidation
- Object lifetime
- Unsafe casts
- Exception boundaries
- Move semantics
- Concurrency
- FFI boundaries

---

# Web Security

For internet-facing applications and APIs, Secure Coding Guardian can focus on:

### Authentication

- Password storage
- Session management
- Token security
- Brute-force protection
- Password reset
- Account enumeration
- MFA-related security
- Credential exposure

### Authorization

- Missing authorization checks
- IDOR
- BOLA
- Horizontal privilege escalation
- Vertical privilege escalation
- Resource ownership failures
- Administrative endpoint exposure

### Input and Injection

- SQL injection
- NoSQL injection
- Command injection
- Template injection
- XSS
- LDAP injection
- Header injection
- Unsafe deserialization

### API Security

- Input validation
- Schema validation
- Mass assignment
- Excessive data exposure
- Rate limiting
- Pagination limits
- Request-size limits
- Response-size limits
- Secure error handling

### Network Security

- TLS configuration
- Certificate validation
- Hostname validation
- SSRF
- Unsafe redirects
- Connection limits
- Request timeouts
- Resource exhaustion

---

# Local and Offline Applications

Security is not only about internet-facing software.

Secure Coding Guardian also considers applications such as:

- CLI tools
- Desktop applications
- Local automation
- Developer tools
- Background services
- Embedded applications
- Native utilities
- Local agents

It can review risks involving:

- Local privilege escalation
- File permissions
- Configuration tampering
- Temporary files
- Symlink attacks
- PATH manipulation
- DLL/SO loading
- Local IPC
- Unix sockets
- Named pipes
- Plugins
- Local databases
- Environment variables
- Update mechanisms
- Local secret storage

An application does not become automatically secure simply because it does not have a public HTTP endpoint.

---

# FFI and Native Boundaries

Applications that combine Python with C/C++ can create particularly important security boundaries.

Secure Coding Guardian can review:

- Buffer ownership
- Buffer lifetime
- Pointer validity
- Size calculations
- Integer conversions
- Type conversions
- ABI assumptions
- Encoding conversions
- Exception boundaries
- Error propagation
- Memory ownership transfer
- Threading assumptions

These boundaries are treated as high-risk areas because security assumptions can change when data crosses language or process boundaries.

---

# Threat Modeling

The Skill does not only inspect individual lines of code.

For security-sensitive work, it can build a lightweight threat model.

It considers:

```text
Assets
  ↓
Actors
  ↓
Entry Points
  ↓
Trust Boundaries
  ↓
Data Flows
  ↓
Threats
  ↓
Mitigations
  ↓
Residual Risk
```

It can use concepts such as:

- STRIDE
- Attack surface analysis
- Trust-boundary analysis
- Threat-based security review

The purpose is simple:

> Understand how the application could be attacked before deciding how the code should be secured.

---

# Security During Development

Secure Coding Guardian can be used at different stages of development.

## Building a New Feature

Ask Claude Code:

```text
Implement this feature securely.
```

The Skill can help identify security requirements before and during implementation.

---

## Reviewing Existing Code

```text
Review this code for security vulnerabilities.
```

The Skill analyzes the relevant code and project context, identifies risks, and suggests remediation.

---

## Securing AI-Generated Code

```text
Review the code I just generated for security issues.
```

The Skill performs a security-focused review rather than assuming generated code is safe.

---

## Fixing a Vulnerability

```text
Fix this security vulnerability and add a regression test.
```

The intended workflow is:

```text
Understand vulnerability
        ↓
Reproduce when possible
        ↓
Implement fix
        ↓
Add regression test
        ↓
Run security checks
        ↓
Review final change
```

---

## Pre-Release Security Review

```text
Perform a security review before release.
```

The Skill can inspect the project, identify relevant attack surfaces, run available security tooling, and produce a security assessment.

---

# Security Workflow

The general workflow is:

```text
Understand
    ↓
Classify
    ↓
Threat Model
    ↓
Secure Design
    ↓
Secure Implementation
    ↓
Static Analysis
    ↓
Security Testing
    ↓
Dependency Review
    ↓
Manual Security Review
    ↓
Regression Testing
    ↓
Security Gate
```

Not every task requires every step.

The Skill chooses the appropriate depth based on the project and the requested task.

---

# Project-Aware Security

Secure Coding Guardian attempts to understand the project before applying security rules.

It can inspect:

- Source code
- Project structure
- `CLAUDE.md`
- README files
- Dependencies
- Lockfiles
- Build systems
- Frameworks
- Configuration
- CI/CD configuration
- Existing security tools
- Test suites
- Compiler configuration
- Deployment configuration

It then determines which security concerns are relevant.

For example:

| Project | Main Security Priorities |
|---|---|
| FastAPI API | Auth, authorization, injection, SSRF, API security |
| Python CLI | Filesystem, subprocess, permissions, environment |
| Django application | Auth, sessions, CSRF, authorization, injection |
| C++ network parser | Memory safety, parsing, fuzzing, DoS |
| C desktop application | Memory safety, local files, IPC, permissions |
| Embedded C | Memory safety, firmware, input parsing, privilege boundaries |

This prevents irrelevant security checks from dominating development.

---

# Security Tools

Secure Coding Guardian can work with security tooling already available in the project or environment.

## Python

Potential integrations include:

- Bandit
- pip-audit
- Semgrep
- OSV-Scanner

## C / C++

Potential integrations include:

- Clang Static Analyzer
- clang-tidy
- cppcheck
- Compiler security warnings
- AddressSanitizer
- UndefinedBehaviorSanitizer
- LeakSanitizer
- ThreadSanitizer
- MemorySanitizer
- libFuzzer
- AFL++

The Skill does not assume that every tool is installed.

It should prefer existing project tooling and use additional tools when they are appropriate and available.

---

# Security Testing

Depending on the project, the Skill can help with:

- Security-focused unit tests
- Integration tests
- Regression tests
- Sanitizer builds
- Fuzzing
- Malformed-input tests
- Boundary-value tests
- Authentication tests
- Authorization tests
- Resource-limit tests
- Parser tests

Security testing complements code review and static analysis.

It does not replace them.

---

# Security Findings

Findings are classified by severity:

```text
CRITICAL
HIGH
MEDIUM
LOW
INFO
```

The Skill considers context rather than treating every security warning as equally important.

It considers factors such as:

- Exploitability
- Impact
- Exposure
- Required privileges
- Attack complexity
- Confidentiality impact
- Integrity impact
- Availability impact
- Existing mitigations

---

# Security Status

The final assessment uses explicit statuses:

```text
PASS
PASS WITH WARNINGS
FAIL
UNKNOWN
```

`UNKNOWN` is intentional.

If the Skill cannot verify a security property, it should not pretend that the property is secure.

For example:

```text
TLS certificate validation: UNKNOWN
```

is better than incorrectly reporting:

```text
TLS certificate validation: PASS
```

---

# Security Gate

For security-sensitive work, the Skill can provide a final security gate.

Example:

```text
Security Gate
────────────────────────────

Threat Model          PASS
Input Validation      PASS
Authentication        PASS
Authorization         PASS
Injection             PASS
Filesystem Security   PASS
Memory Safety         PASS
Dependencies          PASS WITH WARNINGS
Secrets               PASS
Security Tests        PASS
Static Analysis       PASS

Final Status:
PASS WITH WARNINGS
```

The report should also clearly identify unresolved risks.

---

# Security Modes

Secure Coding Guardian can operate with different levels of scrutiny.

### Standard

Normal security-aware development and review.

### Hardened

Stronger security checks and broader testing.

### Critical

For security-sensitive components where practical.

Critical reviews may include:

- Expanded threat modeling
- Static analysis
- Sanitizers
- Fuzzing
- Dependency auditing
- Security regression tests
- Hardening review
- Release security gate

---

# What It Does Not Do

Secure Coding Guardian does **not** claim to make software perfectly secure.

It does not:

- Guarantee zero vulnerabilities
- Replace professional penetration testing
- Replace security audits
- Replace secure infrastructure configuration
- Automatically trust AI-generated code
- Treat passing tests as proof of security
- Blindly install security tools
- Rewrite entire projects unnecessarily
- Invent cryptographic algorithms
- Assume an offline application is safe
- Hide uncertainty

Its purpose is to **reduce security risk and make secure development easier**.

---

# Who Is It For?

Secure Coding Guardian is intended for:

- Python developers
- C developers
- C++ developers
- Backend developers
- Systems programmers
- Desktop developers
- Embedded developers
- Security-conscious developers
- AI-assisted developers
- Teams using Claude Code
- Developers building security-sensitive software

You do not need to be a security expert to use it.

The idea is to let Claude Code help bring security considerations into everyday development.

---

# Example Prompts

You can use natural language.

### Python

```text
Review this Python application for security vulnerabilities.
```

```text
Secure this FastAPI endpoint.
```

```text
Check this CLI for command injection and filesystem vulnerabilities.
```

```text
Review this Python code for unsafe deserialization.
```

### C

```text
Review this C code for memory-safety vulnerabilities.
```

```text
Harden this network parser against malformed input.
```

```text
Find integer overflow and buffer overflow risks in this code.
```

### C++

```text
Perform a security review of this C++ network service.
```

```text
Review this code for lifetime, ownership, and memory-safety problems.
```

```text
Harden this C++ parser and add security regression tests.
```

### General

```text
Threat-model this application.
```

```text
Review the security of the changes I just made.
```

```text
Run a security review before release.
```

```text
Find the highest-risk security problems in this project.
```

---

# Installation

Claude Code Skills are installed as Skill directories containing a `SKILL.md` file. Skills can be installed for a specific project or for your personal Claude Code environment.

## Project Installation

Place the Skill in:

```text
your-project/
└── .claude/
    └── skills/
        └── secure-coding-guardian/
            └── SKILL.md
```

The complete Skill package also contains its supporting security references, workflows, checklists, scripts, and examples.

## Personal Installation

For personal use across projects:

```text
~/.claude/skills/secure-coding-guardian/
```

---

# Project Structure

```text
secure-coding-guardian/
│
├── SKILL.md
├── README.md
├── LICENSE
│
├── references/
│   ├── python/
│   ├── c/
│   ├── cpp/
│   ├── web/
│   ├── native/
│   ├── cryptography/
│   ├── authentication/
│   ├── authorization/
│   ├── dependencies/
│   ├── memory-safety/
│   └── threat-modeling/
│
├── workflows/
│   ├── discovery.md
│   ├── secure-implementation.md
│   ├── security-review.md
│   ├── vulnerability-remediation.md
│   └── release-security-gate.md
│
├── checklists/
│   ├── python.md
│   ├── c.md
│   ├── cpp.md
│   ├── web.md
│   ├── native.md
│   └── final-security-gate.md
│
├── scripts/
│   ├── detect-project.sh
│   ├── security-scan.sh
│   └── validate-skill.sh
│
└── examples/
    ├── python-web.md
    ├── python-cli.md
    ├── cpp-network-parser.md
    └── c-native.md
```

---

# Why Use It During Vibe Coding?

Traditional development often looks like:

```text
Write Code
    ↓
Test
    ↓
Deploy
    ↓
Security Review
```

AI-assisted development can move much faster:

```text
Prompt
 ↓
Generate
 ↓
Modify
 ↓
Refactor
 ↓
Generate Again
 ↓
Ship
```

Security can easily be forgotten in that loop.

Secure Coding Guardian aims to change the workflow to:

```text
Prompt
 ↓
Understand Security Requirements
 ↓
Generate Securely
 ↓
Review
 ↓
Test
 ↓
Fix
 ↓
Verify
 ↓
Continue Coding
```

The objective is to make security a **continuous part of AI-assisted development** rather than a final checkpoint.

---

# Limitations

No automated coding Skill can guarantee that software is secure.

Security also depends on:

- Architecture
- Infrastructure
- Deployment
- Operating system
- Cloud configuration
- Third-party dependencies
- Runtime configuration
- Operational practices
- Human decisions
- Unknown vulnerabilities

Secure Coding Guardian should therefore be considered a **security engineering assistant**, not a replacement for professional security assessment where one is required.

---

# Roadmap

Potential future improvements include:

- More language support
- More framework-specific security analysis
- Expanded fuzzing support
- Container security
- CI/CD security
- Infrastructure-as-Code security
- SBOM generation
- Secret scanning integrations
- Cloud security profiles
- AI/LLM application security
- MCP security
- Agent security
- Plugin security
- Automated security baselines
- Project-specific security policies

---

# Contributing

Contributions are welcome.

Potential contribution areas include:

- New security rules
- New language support
- New framework profiles
- New security checklists
- New workflows
- Tool integrations
- Security regression examples
- Documentation
- False-positive improvements
- Threat-modeling improvements

Before contributing a security rule, explain:

1. What vulnerability it addresses.
2. Why the vulnerability matters.
3. Which languages or frameworks it affects.
4. How the rule should be applied.
5. Potential false positives.
6. How the rule can be tested.

---

# Security

If you discover a security vulnerability in Secure Coding Guardian itself, please follow the project's security disclosure process documented in [`SECURITY.md`](SECURITY.md).

Do not publicly disclose sensitive vulnerability details before the maintainers have had an opportunity to investigate.

---

# License

See [`LICENSE`](LICENSE).

---

# Final Idea

Secure Coding Guardian is built around a simple idea:

> **AI can make developers dramatically faster. Security should become faster too — not easier to forget.**

Instead of asking only:

```text
"Does this code work?"
```

Secure Coding Guardian encourages Claude Code to also ask:

```text
"How can this code be attacked?"

"What does the attacker control?"

"What trust boundaries exist?"

"What happens with malicious input?"

"Can privileges be bypassed?"

"Can sensitive data escape?"

"Can this operation corrupt memory?"

"Can resources be exhausted?"

"How can we verify the fix?"
```

The result is a development workflow where **security is considered while code is being designed, written, changed, and reviewed**.

---

## Secure Coding Guardian

**Secure Python. Secure C. Secure C++. Build faster without treating security as an afterthought.**