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
As-Is process flow
Automation opportunities
In-scope and out-of-scope activities
Business rules
Business exception scenarios
Error handling requirements
Reporting and monitoring requirements
Supporting process documentation

The PDD specifies business validation rules such as acceptable loan terms, applicant age requirements, loan amount limits, and handling of missing emails, missing attachments, or invalid input files. It also defines reporting requirements for process logs, transaction logs, and error monitoring.

<b>Solution Design Document (SDD)</b>

Produced a Solution Design Document (SDD) describing the technical implementation of the automation.

The document includes:

Automation architecture
Runtime configuration
UiPath project structure
Production environment
Orchestrator configuration
Scheduling strategy
Asset configuration
Logging and reporting
Deployment prerequisites
Future enhancements
Technical glossary

The solution was designed as an Unattended Robot deployed through UiPath Orchestrator, using configuration files and Orchestrator Assets to support secure execution and centralized scheduling.

<b>Business Rules</b>

Examples of business rules documented include:

Loan Term must be 1, 3, 5, or 10 years.
Applicant age must meet the minimum eligibility requirement.
Requested loan amount must satisfy the bank's lending policy.
Loan application must contain complete and valid input data.

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
