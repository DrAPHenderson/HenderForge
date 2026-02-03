Functional Specification (FS) for HenderForge
Document Number: FS-HF-001 
Version: 1.0 
Date: February 02, 2026 
Prepared by: Grok 
Reviewed by: Dr. Andrew Henderson, Silver Cavalry Engineering Ltd. 
Approved by: Dr. Andrew Henderson, Silver Cavalry Engineering Ltd.

Change History
Version	  Date	    Changes Made	  Rationale
1.0	    2026-02-02	Initial draft	  Creation of FS based on URS-HF-001 v1.0 to detail design implementation

1.	Purpose and Scope 
This Functional Specification (FS) details how the user requirements defined in URS-HF-001 v1.0 will be met through technical design and implementation. It describes the system's architecture, components, data flows, and logic to achieve the required functionality for HenderForge, a browser-based demo app for generating living SDLC validation documents.
Scope:
•	Covers functional design for all REQ-IDs in the URS, including UI, questionnaire, document generation, propagation, audit trails, and Valhender assistance.
•	Assumes zero budget: Implemented using open-source JavaScript libraries, browser APIs (e.g., localStorage, IndexedDB), no server-side components.
•	ML elements: Simulated via rule-based logic and client-side libraries like TensorFlow.js for deterministic generation.
•	Out of scope: Full ML training (use pre-defined prompts/rules), production security hardening, external integrations.
•	This FS traces back to URS REQs and will inform coding; a future Configuration Specification (CS) may detail specific parameters if needed.

2.	System Architecture and Design Overview HenderForge is a single-page application (SPA) built with vanilla JavaScript, HTML5, and CSS3 for zero-cost deployment. Key components:
•	Frontend Framework: Vanilla JS with modular structure (no heavy frameworks like React to keep it lightweight; can upgrade later).
•	Storage: localStorage for session data (e.g., user name, questionnaire answers); IndexedDB for larger items (e.g., uploaded PDFs, generated docs).
•	Document Handling: jsPDF or docx.js for generating Word/PDF drafts; pdf.js for extracting text from clean electronic PDFs.
•	ML/Logic: Rule-based decision trees in JS for GAMP categorization; few-shot prompting with deterministic seeds for text generation (via local LLM simulation or string templates).
•	Animation/UI: CSS animations for Valhender; Bootstrap or custom CSS for layout.
•	Determinism: Use fixed random seeds (Math.seedrandom) and hardcoded rules to ensure identical inputs yield identical outputs.
•	Deployment: Static HTML file hostable on GitHub Pages.
Data Flow: User inputs → Questionnaire storage → Rule-based/ML generation → Doc storage → Upload parsing → Propagation updates → Audit logging.

3.	User Roles and Implementation 
FS-3.1 (traces to REQ-3.1): Administrator role implemented via a hidden query param (e.g., ?admin=creatorKey) checked in JS; enables upload/delete buttons for SOP/WI in Project Setup. Read-only for users via disabled inputs. 
FS-3.2 (traces to REQ-3.2): User role as default; all functions accessible post-name entry. FS-3.3 (traces to REQ-3.3): On load, generate UUID via crypto.randomUUID(); store name + UUID in localStorage.

4.	Functional Design Each subsection details how URS REQs are met.
4.1 User Interface and Layout FS-4.1.1 (traces to REQ-4.1.1): Main UI as 
containers: Valhender [image] with CSS keyframes for glow; text fields as <textarea>; sidebar as 
tree with onclick events; Workflow as tabbed switched via JS.
 
(Figure 1: Example UI layout)
FS-4.1.2 (traces to REQ-4.1.2): Valhender responses in 
; animation via CSS class toggle on response; text emphasis (bold/italics/ellipses) for Voss tones; split long text into array and add prev/next buttons.
FS-4.1.3 (traces to REQ-4.1.3): Overlay 
with grey CSS filter on body; prompt  for name; on submit, store and remove overlay.
 
(Figure 3: Loading popup example)
FS-4.1.4 (traces to REQ-4.1.4): Initial response as list with hover CSS; onclick loads predefined text; Go Back button resets to initial.
 
(Figure 4: Initial screen example)

4.2 Project Setup and Workflow FS-4.2.1 (traces to REQ-4.2.1): Sidebar as dynamic 
; onclick updates Workflow inner HTML with relevant content/templates.
FS-4.2.2 (traces to REQ-4.2.2): Tabs via JS event listeners; Audit Trail as 
populated from array; CSV export via Blob and URL.createObjectURL. 


Figure 2: Audit trail table example

FS-4.2.3 (traces to REQ-4.2.3): File input for PDFs; store in IndexedDB; generation logic references stored SOP text via string matching.
4.3 Questionnaire and Document Generation FS-4.3.1 (traces to REQ-4.3.1): Multi-screen as array of objects; Next/Back buttons cycle array; progress as <progress> element; save to localStorage as JSON.
FS-4.3.2 (traces to REQ-4.3.2): Questions as form elements; decision tree as JS function (if-else based on inputs).
FS-4.3.3 (traces to REQ-4.3.3): On OK, loop through doc types; use templates + inputs to fill; status icons via CSS classes. 

 
(Figure 5: Project status indicators example)
FS-4.3.4 (traces to REQ-4.3.4): Draft view as <iframe> for preview; download via docx.js export.
 
(Figure 6: Draft preview example)
FS-4.3.5 (traces to REQ-4.3.5): Decision tree outputs sub-doc list; display as clickable links loading previews.
 
(Figure 8: FRS draft screen example)
4.4 Upload and Propagation FS-4.4.1 (traces to REQ-4.4.1): File input; pdf.js to extract text; display in 
; OK/Delete buttons update storage.
FS-4.4.2 (traces to REQ-4.4.2): Parse extracted text; regex-match changes; regen downstream via template functions; update icons.
 
(Figure 7: Uploaded PDF preview example)
FS-4.4.3 (traces to REQ-4.4.3): On select, show alert prompt via JS.

4.5 Report Defending and Queries FS-4.5.1 (traces to REQ-4.5.1): Query handler function with predefined responses + string templates referencing regs/SOPs.
FS-4.5.2 (traces to REQ-4.5.2): Keyword check for off-topic; return joke array random select.
FS-4.5.3 (traces to REQ-4.5.3): Specific query matcher; explain via text.

4.6 Exceptions and Additional Features FS-4.6.1 (traces to REQ-4.6.1): Try-catch blocks; show <dialog> popups.
FS-4.6.2 (traces to REQ-4.6.2): Hidden div; use performance APIs and local counters for metrics.

  5.	Non-Functional Design FS-5.1 (traces to REQ-5.1): Async functions for generation; throttle responses. FS-5.2 (traces to REQ-5.2): All client-side. FS-5.3 (traces to REQ-5.3): No network calls. FS-5.4 (traces to REQ-5.4): Math.seedrandom for any randomness. FS-5.5 (traces to REQ-5.5): Responsive CSS. FS-5.6 (traces to REQ-5.6): Array limits in loops.
  6.	GMP and Regulatory Design FS-6.1 (traces to REQ-6.1): Templates hardcoded with compliant sections. FS-6.2 (traces to REQ-6.2): Array push on actions; immutable. FS-6.3 (traces to REQ-6.3): Alert on load. FS-6.4 (traces to REQ-6.4): pdf.js for clean text.
  7.	Risk Mitigation High-risk (e.g., propagation): Unit tests in JS; simulate in code_execution tool if needed.
  8.	Acceptance and Traceability See updated Traceability Matrix (Appendix A) with Design Ref column.
  9.	Reference Documents
  	URS-HF-001 v1.0
  	JS libraries: pdf.js, docx.js, etc.
 
Appendix A: Traceability Matrix
