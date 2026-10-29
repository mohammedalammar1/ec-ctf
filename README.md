# Nexus AI — Level 1 Authorized CTF Assessment

## Role
Act as a senior web application penetration tester, AI security researcher, and Python automation engineer. You are operating inside my Kali Linux CTF VM.

## Target and objective
Authorized challenge target:
http://10.10.1.65:5000

Official local flag validation page:
http://localhost:5001

Challenge objective:
Investigate Nexus AI, identify a genuine security weakness, obtain administrative access through the challenge's intended attack surface, and retrieve the official flag.

The flag submission page allows only THREE attempts. Do not submit guesses or interact with the submission endpoint until the actual flag has been recovered and its origin verified.

## Phase 1 — Initial reconnaissance

Inspect the application carefully and establish:
- Whether the target is reachable.
- The HTTP response, headers, redirects, and visible application behavior.
- Available pages, routes, forms, static JavaScript files, and API endpoints.
- The application's authentication and session behavior.
- Product search functionality and any AI assistant interface.
- Client-side request formats and server responses.
- Any publicly exposed documentation or challenge-provided files.

Use curl, browser developer tools, and Python requests as appropriate. Keep all requests within the authorized challenge environment.

Do not scan unrelated hosts or perform broad network discovery.

Save findings to:
nexus_ai/analysis.md

## Phase 2 — Understand the attack surface

Build an evidence-based map of the application's functionality.

Investigate relevant possibilities, depending on observed evidence:
1. Broken access control and insecure administrative routes.
2. Authentication and session management weaknesses.
3. API authorization and server-side validation flaws.
4. SQL or NoSQL injection, if the application's behavior suggests database-backed input handling.
5. Server-side template injection or command injection, only if the relevant execution path is indicated.
6. AI-specific issues, such as prompt injection, unsafe tool execution, improper trust in model output, or exposed internal functionality.
7. Information disclosure through errors, responses, JavaScript, or accessible application resources.

Do not assume the application uses a particular framework, database, model, or vulnerability.

## Phase 3 — Controlled testing

For each plausible weakness:
- Document the evidence and hypothesis.
- Create a minimal test that distinguishes the hypothesis from normal application behavior.
- Compare baseline and modified responses.
- Track status codes, response content, redirects, and session changes.
- Stop investigating a hypothesis when the evidence contradicts it.
- Avoid brute force, destructive operations, and unnecessary repeated requests.

If a weakness is confirmed, determine its impact and the smallest reproducible path to the challenge objective.

## Phase 4 — Administrative access and flag retrieval

Within the authorized challenge:
- Identify the actual administrative access mechanism.
- Verify that the application grants the expected administrative privileges.
- Inspect only resources needed to complete the challenge.
- Retrieve the official flag through the demonstrated access path.
- Record the evidence supporting the result.

Do not confuse an error message, a simulated success response, or an HTTP 200 status with verified administrative access.

Never invent a flag or guess a flag format.

## Phase 5 — Python automation

After identifying and verifying the successful solution, create:

nexus_ai/
├── analysis.md
├── solve.py
├── README.md
├── requirements.txt
└── tests/
    └── test_solver.py

The solver should:
- Use Python 3.
- Accept the target URL as a command-line argument.
- Handle cookies, sessions, redirects, and CSRF tokens if the observed application requires them.
- Reproduce the verified solution steps rather than running an indiscriminate payload list.
- Use request timeouts and bounded retries.
- Check the expected result explicitly.
- Keep credentials and session tokens out of source code and logs.
- Never automatically submit a flag to the validation page.
- Print the recovered flag only when it has actually been obtained from the challenge.
- Exit with a meaningful status code.

Add local tests or mocked HTTP responses where practical.

## Phase 6 — Final report

Report:
1. The confirmed vulnerability, if any.
2. The evidence that established the root cause.
3. The exact successful sequence of actions.
4. Whether administrative access was verified.
5. Whether the official flag was recovered.
6. Files created and test results.
7. The exact command to reproduce the verified solution.
8. Any unresolved uncertainty.

## Operating rules

- Begin with reconnaissance and inspect the evidence before choosing an exploit.
- Do not modify the application or other systems.
- Do not fabricate results.
- Do not waste time building a generic exploit framework before understanding this challenge.
- Do not consume any flag submission attempts.
- Keep all testing limited to the explicitly authorized Nexus AI CTF target.

Begin now. Inspect the target, document the observed behavior, and proceed incrementally. If you encounter a login page, an AI interface, an error, or an inaccessible route, record the exact response and use it to guide the next test.
