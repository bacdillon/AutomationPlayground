<h1><b>Automation Opportunities Assessment (PDD, SDD, BPMN)</b></h1><br>
<b>Loan Application Processing from Process Discovery to Automation</b>
<br><br>
<b>Overview</b>

Analysed a manual loan application process and designed an enterprise automation solution using UiPath. The project involved documenting the business process, identifying automation opportunities, defining business rules and exception scenarios, and producing both a Process Definition Document (PDD) and Solution Design Document (SDD) to support implementation.

The automation processes loan applications submitted through UiBank by validating business rules, generating Loan IDs for approved applications, and notifying business users through automated email responses. The solution is designed to run as an unattended process scheduled through UiPath Orchestrator.

<b>Business Analysis Perspective</b>
Reviewed the existing manual loan application workflow and assessed its suitability for automation.
Conducted process analysis to identify repetitive, rule-based activities suitable for RPA.
Documented the end-to-end business process using a Process Definition Document (PDD).
Defined process scope, business rules, applications used, input/output requirements, and exception scenarios.
Designed the future-state automated workflow and identified business exceptions requiring manual intervention.
Collaborated with business stakeholders to define automation objectives and expected business outcomes.

<b>Process Definition Document (PDD)</b>

Developed a comprehensive PDD covering:

1. Business process overview
2. Process scope and objectives
3. Applications involved
4. As-Is process flow
5. Automation opportunities
6. In-scope and out-of-scope activities
7. Business rules
8. Business exception scenarios
9. Error handling requirements
10. Reporting and monitoring requirements
11. Supporting process documentation

The PDD specifies business validation rules such as acceptable loan terms, applicant age requirements, loan amount limits, and handling of missing emails, missing attachments, or invalid input files. It also defines reporting requirements for process logs, transaction logs, and error monitoring.

<b>Solution Design Document (SDD)</b>

Produced a Solution Design Document (SDD) describing the technical implementation of the automation.

The document includes:

1. Automation architecture
2. Runtime configuration
3. UiPath project structure
4. Production environment
5. Orchestrator configuration
6. Scheduling strategy
7. Asset configuration
8. Logging and reporting
9. Deployment prerequisites
10. Future enhancements
11. Technical glossary

The solution was designed as an Unattended Robot deployed through UiPath Orchestrator, using configuration files and Orchestrator Assets to support secure execution and centralized scheduling.

<b>Business Rules</b>

Examples of business rules documented include:

- [x] Loan Term must be 1, 3, 5, or 10 years.
- [x] Applicant age must meet the minimum eligibility requirement.
- [x] Requested loan amount must satisfy the bank's lending policy.
- [x] Loan application must contain complete and valid input data.

Business exception scenarios and expected robot actions were defined for missing emails, missing attachments, empty CSV files, and invalid business inputs.

<b>Solution Architecture</b>

Unattended UiPath Robot
UiPath Orchestrator scheduling
Configuration through Assets
Windows Virtual Machine deployment
Automated email processing
Loan ID generation
Centralized logging
Operational reporting

The SDD also defines runtime details, deployment prerequisites, reporting through Orchestrator logs, and scheduling via Orchestrator.
