User Requirements Specification (URS) for HenderForge
Document Number: URS-HF-001 
Version: 1.0 
Date: February 02, 2026 
Prepared by: Dr. Andrew Henderson, Silver Cavalry Engineering Ltd. 
Reviewed by: Grok 
Approved by: Dr. Andrew Henderson, Silver Cavalry Engineering Ltd.

Change History
Version	Date	Changes Made	Rationale
1.0	2026-02-02	Initial draft	Creation of URS for HenderForge demo app

1. Purpose and Scope
The purpose of this User Requirements Specification (URS) is to define the user needs for HenderForge, a demonstration application that leverages machine learning (ML) to generate a complete suite of living Software Development Lifecycle (SDLC) validation documents for computerized systems in the pharmaceutical industry. This app is intended as a portfolio showcase to demonstrate capabilities in transitioning from Computer Systems Validation (CSV) to ML engineering, by automating compliant document generation under GAMP 5 principles.
Scope:
•	The system shall generate drafts of validation documents including Validation Plan (VP), GMP Risk Assessments, User Requirements Specification (URS), Functional Requirements Specification (FRS) and other specifications (e.g., DDS, SDS, CS depending on complexity), Requirements Traceability Matrix (RTM), Site Acceptance Tests (SAT), Installation/Operational Qualification (IOQ), and Validation Summary Report (VSR), as well as system-specific operation and maintenance SOPs.
•	It includes a user interface for input, AI-assisted guidance, audit trails, and automatic propagation of changes across documents.
•	Out of scope: Full production deployment, real-world GxP validation (demo only), advanced user authentication beyond simplified session IDs, and integration with external systems like actual Kneat Gx (though compatible in format).
•	Budget: Zero budget; the system shall be developed using open-source tools, browser-local storage, and no external cloud services to minimize costs.
•	This URS focuses on user needs; a future Functional Specification (FS) will detail how these requirements are met technically.
REQ-1.1: The system shall demonstrate reduction of CSV lead times by 70-80% for GAMP 5 Category 4-5 systems compared to manual processes. 
REQ-1.2: The system shall incorporate design advantages over generic LLMs (e.g., ChatGPT) by ensuring deterministic outputs, built-in ALCOA+ audit trails, traceable propagation, and domain-grounded generation to support compliant, reproducible results.

2. System Overview and Intended Use
HenderForge is a browser-based demo app for generating and managing living SDLC validation documents for pharma computerized systems. It uses a questionnaire-driven approach to collect inputs, applies ML and rule-based logic to produce drafts, and supports upload of approved electronic documents (e.g., Kneat Gx-style PDFs) for automatic updates to downstream artifacts. The app features an animated assistant (Valhender) for text-based guidance, emphasizing regulatory compliance and user confidence.
Intended use: Portfolio demonstration for ML in regulated environments; not for production GxP activities without further customization to meet 21 CFR Part 11 and EudraLex Vol. 4 Annex 11/22.
The system operates on zero budget, relying on local execution (e.g., browser storage for sessions, open-source libraries).

3. User Roles and Responsibilities
REQ-3.1: The system shall support an Administrator role for uploading SOPs and WIs (read-only for users). 
REQ-3.2: The system shall support a User role for generating documents, querying assistance, and uploading approved PDFs. 
REQ-3.3: Authentication shall be simplified (name entry on load, session UUID) for demo purposes.

4. Functional Requirements
Requirements are categorized for clarity. Each is traceable, testable, and prioritized (High/Medium/Low risk).

4.1 User Interface and Layout
REQ-4.1.1 (High): The system shall display a main UI with: Valhender mascot (animated like MS Office 1997 Mr. Clippy, with glowing brain nodes on response), User Query field, Valhender Response field, Project Setup sidebar (tree navigation), and Workflow panel with tabs (Validation, History, Session Audit Trail).
 
Figure 1: Example UI layout
REQ-4.1.2 (Medium): Valhender shall communicate via text only, animating to draw attention, and use Chris Voss negotiation techniques in responses (e.g., late-night DJ tone via text emphasis, deference, pauses indicated by ellipses) to build user confidence. Responses limited to 1000 characters; longer split with navigation buttons.
 
(Figure: Valhender mascot example)
REQ-4.1.3 (Medium): On load, a popup shall prompt for user name; interface greyed until entered.
 
(Figure 3: Loading popup example)
REQ-4.1.4 (High): Initial Valhender response shall offer options: Introduction, About Creator, Disclaimer, Generate Docs (bubble style with hover lights).
 
(Figure 4: Initial screen example)

4.2 Project Setup and Workflow
REQ-4.2.1 (High): Project Setup sidebar shall list navigable titles (e.g., Validation Effort Outline, SOPs & WIs); clicking highlights and displays content in Workflow/Validation tab. 

REQ-4.2.2 (High): Workflow tab shall include scrollable content, OK/Save buttons; History tab for chat log; Session Audit Trail tab as table with ALCOA+ columns (Timestamp, User ID, Action, Field/Section Changed, Old Value, New Value, Reason for Change). Downloadable as CSV.

Figure 2: Audit trail table example
REQ-4.2.3 (Medium): Admin shall upload SOP/WI PDFs (read-only for users); system shall generate docs consistent with them.

4.3 Questionnaire and Document Generation
REQ-4.3.1 (High): On "Generate Validation Docs," display multi-screen questionnaire (3-7 screens, 3-8 questions each) with progressive disclosure, Next/Back/Save buttons, progress bar, tooltips. Save/resume via session UUID.
REQ-4.3.2 (High): Questions shall cover project context, system details, GxP functions, GAMP category (via decision tree logic), interfaces, risks.
REQ-4.3.3 (High): On OK, generate living docs sequentially (Risk Assessments, VP, URS, FRS/specs, CS, Operating SOP, SAT, IOQ, RTM, VSR) using inputs, preferring approved uploads. Display status (amber dots, ticks, arrows). 

(Figure 5: Project status indicators example)
REQ-4.3.4 (Medium): Draft folders shall show Word file, download option, read-only preview.

(Figure 6: Draft preview example)
REQ-4.3.5 (High): For FRS, support variable sub-docs (FRS, DDS, SDS, CS) based on decision tree; display links and previews.

Figure 8: FRS draft screen example

4.4 Upload and Propagation
REQ-4.4.1 (High): Approved/Post-Approved folders shall allow upload of electronic PDFs (e.g., Kneat-style, no handwriting/scans); extract text, display preview, confirm with OK/Delete.
REQ-4.4.2 (High): On upload confirmation, propagate changes to downstream drafts automatically, updating with ticks/amber circles.

(Figure 7: Uploaded PDF preview example)
REQ-4.4.3 (Medium): For SAT/IOQ Post-Approved, prompt for discrepancy inclusions in PDF.

4.5 Report Defending and Queries
REQ-4.5.1 (High): Valhender shall defend generated content with references to SOPs, regs (21 CFR Part 11, Annex 11/22), traceability; use Voss techniques to reassure users.

REQ-4.5.2 (Medium): Handle off-topic queries with cheesy jokes and refusal.
REQ-4.5.3 (High): Emphasize advantages over generic LLMs: deterministic generation, no hallucinations via grounding, privacy (local data).

4.6 Exceptions and Additional Features
REQ-4.6.1 (Medium): Display popup exceptions (e.g., too many users, memory full, errors).
REQ-4.6.2 (Low): Admin dashboard (accessible only to creator) for metrics (visits/hour, memory, errors, ratings).

5. Non-Functional Requirements
REQ-5.1 (High): Performance: Generate full suite in minutes; responses <1000 chars. 
REQ-5.2 (Medium): Availability: Browser-based, no server for zero budget. 
REQ-5.3 (High): Security/Privacy: Local storage, no external data sharing. 
REQ-5.4 (High): Determinism: Identical inputs yield identical outputs (via seeds/rules). 
REQ-5.5 (Medium): Usability: Animated Valhender, intuitive navigation. 
REQ-5.6 (Low): Scalability: Handle up to 50 systems.

6. GMP and Regulatory Requirements
REQ-6.1 (High): Docs shall comply with 21 CFR Parts 11/210/211, EudraLex Vol. 4 Annexes 11/15/22, PIC/S, GAMP 5. 
REQ-6.2 (High): Audit trail ALCOA+ compliant (simplified for demo). 
REQ-6.3 (High): Disclaimer: Demo only; requires customization for real use. 
REQ-6.4 (Medium): Support electronic uploads/extractions (clean PDFs).

7. Risk and Criticality Assessment
Risk-based per GAMP 5: Demo app is low-risk (no real GxP impact). High-risk reqs (e.g., propagation) prioritized for verification.

8. Acceptance Criteria
REQ-8.1: Verify via manual testing: Generate suite, upload PDF, check propagation, audit trail. Traceability Matrix (Appendix A) links reqs to tests.

9. Reference Documents
•	GAMP 5 Guide (ISPE)
•	21 CFR Part 11, EudraLex Vol. 4 Annex 11/22
•	Chris Voss "Never Split the Difference"
•	Creator CV (attached)

Appendix A: Traceability Matrix


