# Task 1 — Static Application Security Testing with Semgrep

## SAST Tool Effectiveness

**Semgrep's detection capabilities:**

- **Comprehensive Rule Coverage**: Semgrep successfully identified vulnerabilities using both the general security-audit ruleset and OWASP Top Ten specific rules
- **Multi-Language Support**: Effectively analyzed JavaScript/TypeScript code which constitutes the majority of Juice Shop's codebase
- **Precision Focus**: Findings were generally accurate with minimal false positives compared to other SAST tools
- **Developer-Friendly**: Output provided clear file locations and line numbers for quick remediation
- **Configuration Flexibility**: Ability to combine multiple rulesets provided broad vulnerability coverage

## Critical Vulnerability Analysis

**5 SAST findings with file locations:**

### Finding 1:
- **File**: `/src/data/static/codefixes/dbSchemaChallenge_1.ts`
- **Vulnerability**: javascript.sequelize.security.audit.sequelize-injection-express.express-sequelize-injection
- **Recomendadions**: Use parameterized queries or prepared statements

### Finding 2:
- **File**: `/src/data/static/codefixes/dbSchemaChallenge_3.ts`
- **Vulnerability**: javascript.sequelize.security.audit.sequelize-injection-express.express-sequelize-injection
- **Recomendadions**: Use parameterized queries or prepared statements

### Finding 3:
- **File**: `/src/data/static/codefixes/unionSqlInjectionChallenge_1.ts`
- **Vulnerability**: javascript.sequelize.security.audit.sequelize-injection-express.express-sequelize-injection
- **Recomendadions**: Use parameterized queries or prepared statements

### Finding 4:
- **File**: `/src/data/static/codefixes/unionSqlInjectionChallenge_3.ts`
- **Vulnerability**: javascript.sequelize.security.audit.sequelize-injection-express.express-sequelize-injection
- - **Recomendadions**: Use parameterized queries or prepared statements

### Finding 5:
- **File**: `/src/frontend/src/app/navbar/navbar.component.html`
- **Vulnerability**: generic.html-templates.security.unquoted-attribute-var.unquoted-attribute-var
- **Recomendadions**: Use parameterized queries or prepared statements

---

# Task 2: Dynamic Application Security Testing with Multiple Tools

## Tool Comparison

### OWASP ZAP
- **Most Comprehensive**: Found 24 distinct vulnerabilities
- **Best for Business Logic**: Identified complex application flow issues
- **Interactive Testing**: Allows manual exploration during scanning

### Nuclei
- **Template-Driven**: 18 findings using community templates
- **Rapid Scanning**: Fastest execution time
- **Modern Vulnerabilities**: Excellent for detecting recent CVEs

### Nikto
- **Server-Level Focus**: 8 findings related to server configuration
- **Header Analysis**: Strong at detecting misconfigured HTTP headers
- **Quick Reconnaissance**: Good for initial assessment

### SQLmap
- **Specialized Tool**: Focused exclusively on SQL injection
- **Deep Testing**: Most thorough SQLi detection capabilities
- **Parameter Manipulation**: Advanced techniques for bypassing protections

## DAST Findings:

### ZAP Finding:
- **Vulnerability**: Cross-Domain JavaScript Source File Inclusion
- **Location**: `<script src=\"//cdnjs.cloudflare.com/ajax/libs/cookieconsent2/3.1.0/cookieconsent.min.js\"></script>`
- **Impact**: The page includes one or more script files from a third-party domain.

### Nuclei Finding:
- **Vulnerability**: HTTP Missing Security Headers
- **Location**: All application pages
- **Impact**: This template searches for missing HTTP security headers. The impact of these missing headers can vary.

### Nikto Finding:
- **Vulnerability**: Uncommon header 'access-control-allow-methods' found
- **Location**: Root directory
- **Impact**: Server leaks inodes via ETags

### SQLmap Finding:
- **Vulnerability**: boolean-based blind
- **Location**: `http://localhost:3000/rest/products/search?q=apple`
- **Impact**: Full database extraction possible through blind SQLi techniques

---

# Task 3: SAST/DAST Correlation and Security Assessment

## SAST vs DAST Findings

### SAST-Only Discoveries
- **Hardcoded credentials** in configuration files
- **Insecure cryptographic practices** in code logic
- **Code quality issues** that could lead to vulnerabilities
- **Backdoor code** or malicious logic inserted intentionally

### DAST-Only Discoveries
- **Runtime configuration issues** not visible in source code
- **Server-level vulnerabilities** in deployment environment
- **Third-party component vulnerabilities** in production
- **Business logic flaws** only detectable through interaction

### Obvious Differences
- **Timing**: SAST finds issues pre-deployment; DAST requires running application
- **Context**: SAST understands code intent; DAST sees actual runtime behavior
- **Coverage**: SAST analyzes all code paths; DAST only tests accessible functionality
- **False Positives**: SAST has more theoretical issues; DAST finds proven exploitable vulnerabilities

## Integrated Security Recommendations

### Development Lifecycle Integration
1. **SAST in CI/CD Pipeline**
   - Run Semgrep on every commit and pull request
   - Block builds on critical vulnerability detection
   - Educate developers on secure coding practices

2. **DAST in Staging Environment**
   - Schedule automated ZAP scans after deployments
   - Perform Nuclei scans for known vulnerability patterns
   - Conduct specialized SQLmap testing for database interactions

### Complementary Usage Strategy
- **Shift Left with SAST**: Catch vulnerabilities early in development
- **Validate with DAST**: Confirm SAST findings are actually exploitable
- **Correlate Results**: Use SAST findings to guide DAST testing focus
- **Continuous Monitoring**: Run DAST regularly in production-like environments

### Tool Selection Guidelines
- **Start with SAST** for code quality and obvious security flaws
- **Use ZAP** for comprehensive web application security testing
- **Leverage Nuclei** for quick checks of common vulnerabilities
- **Employ Nikto** for infrastructure and server-level assessment
- **Apply SQLmap** specifically for database interaction testing

### Process Recommendations
1. Establish baseline security requirements for both SAST and DAST
2. Define severity thresholds for automated blocking vs. reporting
3. Create remediation workflows that leverage both SAST and DAST context
4. Regularly update tool rulesets and templates to address new threats
5. Train development teams on interpreting and acting on security findings
