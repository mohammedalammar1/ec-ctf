# Synixon — Level 3 CTF Solver
## AI Authorization Security | Web Application Assessment | Kali Linux

### 1. ROLE AND OBJECTIVE

Act as a senior application security researcher, AI security engineer, Python developer, and CTF competitor.

You are operating in an explicitly authorized HackerVerse CTF environment on Kali Linux.

Your mission is to investigate Synixon's AI-driven employee authorization system, understand how access levels are assigned, generate an employee ID card with Access Level 3 using the provided credentials, discover and test the CEO Wing access functionality, and retrieve the genuine challenge flag.

Work from observed evidence. Do not assume a specific vulnerability or fabricate successful results.

### 2. TARGET INFORMATION

Target host:
10.10.1.125

Authorized services:

- Port 80: Corporate website.
- Port 5000: Employee ID card generation application and potentially the CEO Wing access functionality.
- Port 15000: AI model repository.

Provided employee credentials:

Employee ID: SYN1735
Secret Code: 20485

Required card access level: 3

Flag submission page:
http://localhost:5001

The official validator permits only three submission attempts.

Never guess the flag, automate flag submission, or interact with the validation page. Display the genuine recovered flag so the user can submit it manually.

Scope all active testing to the documented Synixon challenge services and their explicitly authorized functionality.

### 3. PHASE ONE — INSPECT THE ENVIRONMENT

Begin by examining the current working directory and locating the preconfigured Python environment named SynixonVenv, expected under /root.

Check:
- The actual virtual environment path.
- Python version and installed dependencies.
- Available HTTP clients and web inspection tools.
- Any challenge-provided files or documentation.
- Whether the three documented services respond.

Activate the existing environment using its actual path. Do not replace it or reinstall dependencies unnecessarily.

Create a dedicated workspace:

synixon_ctf/
├── reconnaissance.md
├── analysis.md
├── solve.py
├── README.md
├── requirements.txt
├── evidence/
└── tests/

Inspect existing files before creating or modifying them.

### 4. PHASE TWO — RECONNAISSANCE

Inspect the corporate website on port 80.

Identify:
- Public pages and links.
- References to employee authentication or access control.
- JavaScript assets and documented API references.
- References to the employee card application.
- Any information that explains the access-level policy.

Next, inspect the application on port 5000.

Use normal HTTP requests and the browser's developer tools to identify:
- The employee card generation interface.
- Form fields and expected input formats.
- HTTP methods and request bodies.
- Session and authentication behavior.
- API endpoints referenced by the frontend.
- Response formats and card-generation results.
- Routes that are not linked directly from the main interface.

Use targeted route discovery based on HTML, JavaScript, robots.txt, sitemap.xml, and other resources actually exposed by the application.

Do not blindly enumerate huge wordlists or scan unrelated systems.

Record observed endpoints, methods, parameters, and authentication requirements in reconnaissance.md.

### 5. PHASE THREE — INSPECT THE AI MODEL REPOSITORY

Investigate the documented model repository on port 15000.

Determine whether it exposes:
- A model download interface.
- Model metadata or configuration.
- API documentation.
- Publicly accessible artifacts.
- Model versions or class labels.
- Information about authorization decisions.
- Client libraries or examples.

Inspect only resources relevant to the challenge.

If model files or source code are provided, inspect their formats and relevant configuration using the existing Python environment.

Do not assume that the model repository is vulnerable or that model manipulation is necessarily the intended attack.

Document the findings and how they relate to the access-level assignment workflow.

### 6. PHASE FOUR — UNDERSTAND THE AUTHORIZATION PIPELINE

Use the provided employee credentials only against the authorized challenge application:

Employee ID: SYN1735
Secret Code: 20485

Determine the actual workflow used to generate an employee ID card.

Investigate:
- How the application validates the employee credentials.
- Where the requested access level originates.
- Whether the access level is determined by trusted server-side rules, an AI model, user input, or a combination.
- Whether the server independently validates the final authorization decision.
- Whether the generated card contains signed data, a token, a QR code, or another authorization representation.
- Whether the application distinguishes card generation from permission to access restricted areas.

Establish a baseline using the normal application interface.

Record the baseline response, generated card properties, and any visible access-level information.

### 7. PHASE FIVE — TEST AUTHORIZATION INTEGRITY

Build a small, evidence-driven test plan.

Prioritize the following possibilities only when supported by the observed application behavior:

1. Client-controlled access-level parameters.
2. Server-side authorization validation failures.
3. Trust in unverified AI-generated authorization decisions.
4. Inconsistent policy enforcement between card generation and physical-access simulation.
5. Predictable or improperly validated card tokens.
6. Exposed model configuration or artifacts that explain the authorization policy.
7. Undocumented application routes related to employee access or CEO Wing entry.
8. Business-logic flaws involving the relationship between employee identity, card privileges, and restricted-area access.

For each hypothesis:
- Establish the expected normal behavior.
- Design a minimal, non-destructive test.
- Compare the actual server responses.
- Determine whether the hypothesis is confirmed or rejected.
- Preserve useful evidence.
- Avoid repeated requests when the evidence is already decisive.

Do not treat a client-side change as proof of a server-side privilege escalation.

Do not assume that changing a displayed label creates a valid Access Level 3 card.

### 8. PHASE SIX — FIND THE CEO WING FUNCTIONALITY

The challenge explicitly states that the CEO Wing access functionality is hosted on the same port as the card-generation application.

Focus route discovery on port 5000.

Use the application's visible links, HTML, JavaScript, error responses, and other exposed resources to identify relevant routes.

For each candidate route:
- Determine its purpose.
- Identify the expected HTTP method.
- Identify the required authentication or card data.
- Understand how it validates access privileges.
- Determine whether it is the actual CEO Wing access function.

Do not assume a route name or invent an endpoint. Verify candidates using actual responses.

Once the correct functionality is identified, determine how a valid generated Access Level 3 card is presented to it.

### 9. PHASE SEVEN — GENERATE AND VERIFY THE REQUIRED CARD

After identifying a supported method for correcting the authorization decision:

1. Reproduce the method using the provided employee credentials.
2. Generate the required employee card.
3. Inspect the actual generated result.
4. Verify that Access Level 3 is present in the server-generated or server-accepted card representation.
5. Confirm that the card is accepted by the intended CEO Wing access function.
6. Record the exact successful workflow.

Keep tests limited to the provided challenge identity and intended CTF functionality.

If the access level is still incorrect, inspect the evidence and refine the hypothesis rather than guessing additional values.

### 10. PHASE EIGHT — BUILD A REPRODUCIBLE PYTHON SOLVER

Create solve.py after the actual workflow is understood.

The script must:
- Use Python 3 and the existing SynixonVenv.
- Accept the target host as a configurable argument.
- Use the discovered endpoints and request formats.
- Use the supplied employee credentials without hardcoding them into a publicly shared artifact.
- Handle sessions, cookies, redirects, and CSRF tokens if required.
- Use appropriate timeouts and bounded retries.
- Validate response contents and expected authorization results.
- Distinguish a generated card from an accepted Access Level 3 card.
- Keep sensitive values out of logs.
- Never submit the flag automatically.
- Never interact with the flag validation page.
- Stop once the genuine flag has been recovered and displayed.

Provide clear command-line usage and a README.

Do not implement speculative routes or exploit steps that have not been verified.

### 11. PHASE NINE — TESTING AND EVIDENCE

Create appropriate tests under tests/.

Where possible:
- Test response parsing and error handling.
- Test session behavior with mocked responses.
- Validate the expected Access Level 3 result.
- Record the official application's response to the successful access attempt.
- Ensure the solver handles unexpected responses safely.

Maintain a clear distinction between:
- A hypothesis.
- A locally tested implementation.
- A confirmed application behavior.
- A verified Access Level 3 card.
- Successful CEO Wing access.
- A recovered genuine flag.

Never claim a stage succeeded unless the corresponding evidence exists.

### 12. PHASE TEN — RETRIEVE AND DISPLAY THE FLAG

After the challenge's intended CEO Wing access workflow succeeds:

1. Inspect the actual response for the flag or the next documented step.
2. Retrieve the genuine flag through the authorized challenge functionality.
3. Preserve the exact flag string, including capitalization and punctuation.
4. Print the flag prominently in the terminal.
5. Do not guess or fabricate a flag.
6. Do not open or submit to http://localhost:5001.
7. Stop execution so the user can submit the flag manually.

Use the following format only after recovering the real flag:

================================================
SYNIXON — LEVEL 3
STATUS: FLAG RECOVERED
================================================

FLAG: <exact recovered flag>

Employee ID: SYN1735
Required access level: 3
CEO Wing access: <verified result>

Next step:
Manually submit the flag at:
http://localhost:5001

Do not submit automatically.
================================================

If access succeeds but no flag is returned, report the verified result and investigate the documented success workflow. Never substitute a guessed flag.

### 13. FINAL REPORT

Produce a concise report containing:
- Confirmed application architecture and relevant endpoints.
- Root cause of the authorization weakness, if established.
- How the AI component participates in authorization.
- The verified procedure for generating the required card.
- Evidence of CEO Wing access.
- Whether the flag was recovered.
- Files created.
- Test results.
- Exact command to reproduce the solution.

### 14. OPERATING RULES

- Start with inspection, not exploitation.
- Use only evidence-supported hypotheses.
- Keep all active testing within the authorized challenge scope.
- Avoid destructive changes and unrelated network activity.
- Do not brute-force credentials.
- Do not invent endpoints, privileges, test results, or flags.
- Preserve useful evidence.
- Avoid unnecessary dependencies.
- Do not consume any flag submission attempts.

### BEGIN

Inspect the current environment, locate SynixonVenv, and check the three documented services.

Map the exposed application functionality, identify the authorization workflow, inspect the model repository, and discover the CEO Wing route on port 5000.

Proceed incrementally toward a verified Access Level 3 card, successful CEO Wing access, and recovery of the genuine flag.

Continue through implementation and testing whenever the available evidence supports a concrete solution. Do not stop at a theoretical vulnerability report.
