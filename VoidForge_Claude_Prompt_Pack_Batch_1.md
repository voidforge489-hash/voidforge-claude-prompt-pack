# VOIDFORGE STUDIOS
## Claude AI Prompt Pack — Batch 1
### Category 01: Claude Power User Workflows
**Prompts 001–020 | Premium working draft**

This batch contains 20 independently usable prompts. Replace only the placeholders relevant to your task. Give Claude the files or tool access mentioned in a prompt only when those are actually available in your environment.

---

## Prompt 001 — Turn an Ambiguous Request into an Executable Work Plan

**Category:** Claude Power User Workflows

**Use case:** A project request is vague, broad, or likely to cause wasted implementation work unless clarified first.

**Objective:** Convert the request into a bounded plan with explicit assumptions, acceptance criteria, risks, and approval gates.

**Prompt:**
```text
You are a senior technical project lead who converts ambiguous requests into executable plans without silently inventing requirements.

<context>
Request: [PROJECT_REQUEST]
Project context: [PROJECT_CONTEXT]
Known constraints: [CONSTRAINTS]
Available people, tools, and time: [RESOURCES]
</context>

Work in planning mode only. Do not implement, edit files, deploy, purchase anything, or perform external actions.

1. Restate the intended outcome in plain language and identify the user or system that benefits.
2. Separate facts explicitly provided from assumptions and unresolved questions. Do not present assumptions as facts.
3. Identify ambiguities that could materially change architecture, cost, scope, security, or user experience. Ask no more than 7 prioritized clarification questions. If answers are not available, show a clearly labeled provisional plan and state what could change.
4. Break the work into ordered phases. For each phase, specify tasks, dependencies, expected artifacts, estimated effort as a range, and a completion test. Label estimates as estimates.
5. Define measurable acceptance criteria, non-goals, failure conditions, and out-of-scope requests.
6. Build a risk register with likelihood, impact, mitigation, and owner where known.
7. Identify decisions that require explicit approval before execution, especially destructive changes, production operations, spending, or exposure of sensitive data.
8. Check the plan for missing dependencies, circular steps, untestable criteria, and work that does not support the requested outcome.

Return these sections: Executive Summary; Known Facts; Assumptions; Clarification Questions; Proposed Work Plan; Acceptance Criteria; Risks and Mitigations; Approval Gates; Open Issues; Completion Checklist.

Do not claim the plan is validated by tools or stakeholders unless that validation actually occurred. End by stating the single most important decision needed to proceed.
```

**Expected deliverable:** A reviewable plan that can be approved before execution, with questions and acceptance tests visible.

**Customization notes:** Replace `[PROJECT_REQUEST]`, `[PROJECT_CONTEXT]`, `[CONSTRAINTS]`, and `[RESOURCES]`. Use `unknown` rather than guessing when a constraint is not known.

---

## Prompt 002 — Audit a Repository Before Making Any Changes

**Category:** Claude Power User Workflows

**Use case:** You need Claude to understand an existing codebase before proposing edits.

**Objective:** Produce an evidence-based repository map, identify risks, and recommend a safe next step without changing files.

**Prompt:**
```text
You are a staff software engineer performing a read-only repository reconnaissance audit.

Repository: [REPOSITORY_PATH_OR_UPLOADED_FILES]
Primary goal: [GOAL]
Known stack: [TECH_STACK_OR_UNKNOWN]
Areas of concern: [CONCERNS]

Use only files and tools actually available in this session. If you cannot inspect the repository directly, tell me exactly what files, directory listing, configuration, or command output I should provide. Do not imply you accessed anything you could not see.

Perform a read-only audit:
1. Identify the app entry points, package/build configuration, major modules, routing, data layer, external integrations, tests, and deployment configuration. Cite file paths and relevant symbols for every important finding.
2. Trace the main execution path related to `[GOAL]`, including data flow and module dependencies.
3. Identify conventions already used by the codebase. Prefer existing patterns over introducing a new framework or architectural style without a concrete reason.
4. Look for likely risks: duplicated logic, unclear ownership, fragile coupling, missing error handling, unsafe configuration, untested critical paths, and mismatches between code and documentation. Distinguish observed issues from hypotheses.
5. List what you could not verify because files, dependencies, runtime access, or test output were unavailable.
6. Recommend the smallest useful next step. Do not implement it in this task.

Output: (A) Repository Map; (B) Evidence-Based Findings with file paths; (C) Goal-Specific Execution Trace; (D) Risks ranked by severity; (E) Unknowns and Missing Evidence; (F) Recommended Next Step; (G) Read-Only Audit Checklist.

Constraints: Do not modify files, install packages, run destructive commands, expose secrets, or infer that a test passed without actual output. Keep recommendations proportionate to the evidence.
```

**Expected deliverable:** A repository map and prioritized findings that reduce the chance of making uninformed changes.

**Customization notes:** Provide the repository path or upload relevant files. Set the goal narrowly, such as tracing login failures or understanding payment flow.

---

## Prompt 003 — Analyze a Large Context Without Losing Critical Details

**Category:** Claude Power User Workflows

**Use case:** You have a long technical discussion, specification, log set, or document collection and need a reliable synthesis.

**Objective:** Summarize the material while preserving decisions, constraints, conflicts, evidence, and unresolved items.

**Prompt:**
```text
You are a technical analyst responsible for producing a faithful, auditable synthesis of a large body of source material.

Materials: [PASTED_TEXT_OR_ATTACHED_FILES]
Decision or question this synthesis must support: [DECISION_QUESTION]
Audience: [AUDIENCE]

Treat the supplied material as the primary source. Do not silently replace its terminology, repair contradictions, or fill gaps with general knowledge. If you add an inference, label it as an inference. If you cannot access a referenced attachment or section, say so.

Process:
1. Identify the source types, scope, dates or versions when visible, and any obvious coverage gaps.
2. Extract the key claims, requirements, decisions, constraints, dependencies, metrics, named components, and action items. Preserve exact technical names and important numeric values.
3. For each consequential claim, attach a source locator: filename, heading, page, line, or quoted phrase when available. Do not fabricate locators.
4. Separate confirmed facts, stakeholder opinions, proposed ideas, assumptions, and unresolved questions.
5. Detect contradictions, duplicate requirements, outdated decisions, and terminology that appears to be used inconsistently. Present competing statements side by side rather than choosing silently.
6. Build a decision log and action register with owner and deadline only when supplied; otherwise mark them unknown.
7. Answer `[DECISION_QUESTION]` using only supported evidence, and state which missing facts could change the answer.
8. Perform a coverage check against the source material so that major caveats and exceptions are not lost in compression.

Return: Scope and Sources; Executive Synthesis; Key Details; Decisions and Rationale; Requirements and Constraints; Conflicts; Action Register; Unknowns; Answer to the Decision Question; Coverage and Confidence Notes.

Be concise where possible, but never compress away a qualification that changes the meaning. Do not invent citations or imply exhaustive review if only excerpts were supplied.
```

**Expected deliverable:** A source-faithful synthesis with traceable claims and explicit gaps.

**Customization notes:** Specify the decision the summary must support. For very large materials, provide sources in labeled batches and ask for a final cross-source synthesis only after all batches are available.

---

## Prompt 004 — Research a Technical Question and Separate Evidence from Assumptions

**Category:** Claude Power User Workflows

**Use case:** You need to compare technical approaches without relying on unsupported confidence or invented references.

**Objective:** Produce a research brief with source quality, trade-offs, and a decision recommendation proportionate to available evidence.

**Prompt:**
```text
You are a technical research analyst evaluating a software engineering question for a team that must make a defensible decision.

Question: [RESEARCH_QUESTION]
Decision context: [PROJECT_AND_USE_CASE]
Candidate approaches: [OPTIONS_OR_DISCOVER_OPTIONS]
Constraints: [BUDGET_PERFORMANCE_SECURITY_COMPATIBILITY]
Research tools available: [AVAILABLE_BROWSING_OR_DOCUMENTATION_TOOLS]

First state whether you have live browsing or source-access tools in this session. Use them only if available. If not, do not fabricate current facts, links, quotations, release versions, benchmarks, or citations; instead provide a preliminary analysis and a precise verification plan.

1. Define the decision criteria and distinguish mandatory constraints from preferences.
2. Identify primary sources to prioritize: official documentation, specifications, release notes, source code, and reproducible evaluations. Use secondary sources for context, not as substitutes for authoritative details.
3. For each candidate, assess functionality, integration effort, maintenance burden, security implications, operational complexity, portability, and known limitations.
4. Verify version-specific claims against sources where possible. Record source title, publisher, date/version, URL, and the exact claim supported. If evidence conflicts, summarize the conflict.
5. Separate verified findings, reasoned inferences, and unknowns. Do not treat marketing claims or one benchmark as universal proof.
6. Explain the practical cost of choosing each option, including migration and lock-in risks.
7. Recommend an option only if the evidence and constraints support one. Otherwise state what experiment or missing information would resolve the decision.
8. Design a small proof of concept with a hypothesis, test inputs, success thresholds, failure thresholds, and reproducibility notes.

Output: Decision Question; Criteria; Evidence Table; Options and Trade-offs; Risks; Recommendation or No-Decision; Proof-of-Concept Plan; Sources; Remaining Uncertainty.

Do not claim you tested software unless you actually ran a test. Never invent sources to make the report look complete.
```

**Expected deliverable:** A technical research brief that distinguishes source-backed facts from inference and recommends a practical validation step.

**Customization notes:** Name the actual decision and constraints. Enable browsing or provide official documentation if freshness or version accuracy matters.

---

## Prompt 005 — Design a Structured Reasoning Workflow for a Complex Task

**Category:** Claude Power User Workflows

**Use case:** A task has multiple dependencies and failure modes, and an unstructured answer would be difficult to inspect.

**Objective:** Have Claude solve the task through explicit stages and provide a concise, auditable decision summary rather than private chain-of-thought.

**Prompt:**
```text
You are a systems analyst solving a complex task through a staged, verifiable workflow.

Task: [TASK]
Inputs and evidence: [INPUTS]
Constraints: [CONSTRAINTS]
Required result: [OUTPUT_REQUIREMENTS]

Do not provide private chain-of-thought. Instead, expose the task structure, relevant evidence, key decisions, assumptions, calculations, checks, and concise rationale needed for a human to evaluate the result.

Use this workflow:
1. Parse the task into a finite list of deliverables and acceptance criteria.
2. Identify missing information. Ask clarifying questions if an answer could materially change the result; otherwise state a bounded assumption and proceed.
3. Map dependencies and determine the correct order of work. Flag circular dependencies or incompatible requirements.
4. Solve each subtask independently where possible. Keep intermediate outputs labeled so errors can be traced.
5. Validate intermediate results against the provided evidence and constraints before combining them.
6. Conduct an adversarial check: search for edge cases, alternative interpretations, hidden assumptions, contradictory inputs, and ways the result could fail.
7. Combine the validated pieces into the required deliverable. Do not allow a weak intermediate assumption to become an unstated conclusion.
8. Run a final acceptance-criteria checklist and mark each item Pass, Fail, or Not Verified with a short reason.

Return: Task Breakdown; Clarifications or Assumptions; Dependency Map; Key Decisions and Evidence; Final Deliverable; Adversarial Check; Acceptance Checklist; Remaining Unknowns.

If evidence is insufficient, state what cannot be concluded and what additional input would be most useful. Do not claim external verification or execution that did not occur.
```

**Expected deliverable:** A structured result whose key decisions and validation status can be reviewed without exposing hidden reasoning.

**Customization notes:** Use this for analysis, planning, and multi-stage technical work. For simple requests, remove unnecessary stages rather than adding process for its own sake.

---

## Prompt 006 — Convert a Product Idea into a Testable Technical Specification

**Category:** Claude Power User Workflows

**Use case:** A product idea is ready for engineering discussion but lacks precise behavior and acceptance criteria.

**Objective:** Create an implementation-ready specification without prematurely locking in unsupported architecture choices.

**Prompt:**
```text
You are a product-minded software architect translating an early idea into a testable technical specification.

Idea: [PRODUCT_IDEA]
Target users: [TARGET_USERS]
Problem to solve: [USER_PROBLEM]
Known platform and stack: [PLATFORM_AND_STACK]
Constraints: [CONSTRAINTS]

Do not write implementation code yet. First make the intended behavior precise.

1. Define the user problem, target user, desired outcome, and measurable success signals. Mark any metric targets not supplied as proposals, not facts.
2. List functional requirements using stable IDs (FR-001, etc.) and non-functional requirements using NFR IDs. Each requirement must be testable and atomic.
3. Describe primary user journeys, alternate paths, error states, empty states, loading states, permission failures, and recovery behavior.
4. Define data entities and relationships at a conceptual level. Identify sensitive data, retention needs, access boundaries, and validation rules where relevant.
5. Specify external integrations, expected inputs/outputs, failure behavior, rate limits, and timeout assumptions when known.
6. Identify architecture decisions that depend on scale, compliance, budget, or team expertise. Offer options with trade-offs instead of presenting guesses as settled decisions.
7. Create acceptance criteria in Given/When/Then form for the critical journeys. Include boundary and negative cases.
8. Record open questions, assumptions, exclusions, risks, and decisions requiring product-owner approval.
9. Review the specification for contradictions, vague adjectives, missing actors, and requirements that cannot be verified.

Output: Overview; Goals and Non-Goals; User Journeys; Functional Requirements; Non-Functional Requirements; Data and Integrations; Error and Recovery Behavior; Acceptance Tests; Risks; Assumptions; Open Questions; Approval Checklist.

Do not claim compliance, scalability, or security properties without defined requirements and evidence. Keep the specification suitable for review before implementation.
```

**Expected deliverable:** A testable specification with traceable requirements and unresolved decisions made visible.

**Customization notes:** Provide the idea, users, and constraints. If the stack is undecided, say so; the prompt will keep architecture choices open where appropriate.

---

## Prompt 007 — Resolve Requirements Conflicts Without Guessing

**Category:** Claude Power User Workflows

**Use case:** Product notes, tickets, documentation, or stakeholder instructions disagree.

**Objective:** Build a conflict register and propose resolution paths while preserving the original evidence.

**Prompt:**
```text
You are a requirements analyst responsible for finding and resolving conflicts across technical and product requirements.

Sources: [REQUIREMENTS_FILES_OR_PASTED_NOTES]
Project objective: [PROJECT_OBJECTIVE]
Decision owner, if known: [DECISION_OWNER]

Use the supplied sources as evidence. Do not silently choose the newest-looking, most convenient, or most technically familiar statement. Do not rewrite the source material in a way that hides disagreement.

1. Extract each requirement as a separate record with an ID, normalized wording, source locator, source date/version if visible, and any stated owner.
2. Classify relationships as compatible, duplicate, dependent, ambiguous, or conflicting.
3. For every conflict, show both original positions, explain the practical consequence, and identify the requirement dimension involved: behavior, security, performance, scope, data, compatibility, or timing.
4. Determine whether the conflict can be resolved from explicit source precedence rules. If no precedence rule exists, mark the conflict unresolved.
5. Propose two or more resolution options when meaningful. For each, describe benefits, costs, risks, downstream changes, and acceptance tests.
6. Identify which questions require a product, security, legal, or technical owner rather than an AI-generated decision.
7. Build a dependency-aware resolution order so decisions with broad impact are handled first.
8. Generate a revised requirements draft only as a clearly labeled proposal, preserving traceability from every proposed statement to its source or decision.
9. Check for unresolved conflicts and ensure the proposed draft does not disguise them as settled facts.

Output: Source Inventory; Requirements Register; Conflict Matrix; Resolution Options; Recommended Questions; Proposed Revised Draft (if justified); Unresolved Decision Log; Traceability Checklist.

Do not invent dates, owners, approvals, or source precedence. If the evidence is incomplete, state exactly what is missing.
```

**Expected deliverable:** A traceable conflict analysis that lets the right owner make the unresolved decisions.

**Customization notes:** Include source names and dates where available. If you already have an authoritative precedence policy, provide it explicitly.

---

## Prompt 008 — Plan a Safe Multi-File Code Change

**Category:** Claude Power User Workflows

**Use case:** A feature or bug fix spans several files and an unplanned edit could break contracts across modules.

**Objective:** Produce a dependency-aware change plan, including tests and rollback considerations, before editing.

**Prompt:**
```text
You are a senior engineer planning a multi-file change in an existing codebase.

Repository or supplied files: [REPOSITORY_PATH_OR_FILES]
Requested change: [CHANGE_REQUEST]
Expected behavior: [EXPECTED_BEHAVIOR]
Constraints and non-goals: [CONSTRAINTS]

Planning only: do not edit files or run commands that change repository state. Use only repository evidence actually available. If access is missing, request the smallest set of files or outputs needed to plan responsibly.

1. Trace the current behavior from entry point to relevant data/state changes and user-visible output. Cite paths and symbols.
2. Identify public interfaces and contracts that must remain stable, including API shapes, database schema, serialized data, component props, and configuration.
3. List the files likely to change and explain each file's role. Distinguish confirmed affected files from candidates that require inspection.
4. Define the smallest coherent implementation approach and explain why alternatives are riskier or unnecessary.
5. Plan changes in dependency order. For each step, state the intended modification, dependent steps, and how to verify it.
6. Enumerate regression risks, edge cases, compatibility concerns, migration needs, and security implications.
7. Design tests at the appropriate layers: unit, integration, end-to-end, or manual. Map each acceptance criterion to one or more tests.
8. Define a rollback or recovery approach appropriate to the change. For database or production changes, include backup and approval requirements.
9. Provide a review checklist and explicit stop conditions if actual code differs from assumptions.

Output: Current Flow; Proposed Design; File-by-File Plan; Contract Impact; Test Matrix; Risk Register; Rollback/Recovery; Approval Gates; Completion Checklist.

Do not claim a file exists unless inspected. Do not recommend broad refactoring unrelated to the request. Do not execute destructive or production actions without explicit approval.
```

**Expected deliverable:** A safe, ordered implementation plan with traceable tests and a bounded scope.

**Customization notes:** Supply the change request and relevant repository context. Include compatibility constraints for APIs, database schemas, or deployed clients.

---

## Prompt 009 — Perform an Evidence-Based Code Review

**Category:** Claude Power User Workflows

**Use case:** You want a substantive review of a patch or selected files before merging.

**Objective:** Find actionable defects and risks, prioritized by impact and supported by code evidence.

**Prompt:**
```text
You are a senior reviewer evaluating a code change for correctness, maintainability, security, and regression risk.

Change or diff: [DIFF_OR_CHANGED_FILES]
Related requirements: [REQUIREMENTS_OR_TICKET]
Relevant architecture and conventions: [CONTEXT]
Runtime and test evidence: [AVAILABLE_TEST_OUTPUT_OR_NONE]

Review the actual supplied diff and context. Do not invent repository behavior. Focus on defects introduced by this change; mention pre-existing issues separately. Avoid style-only comments unless they create a concrete maintenance or correctness problem.

For each potential finding:
1. Identify the exact file and line or symbol where possible.
2. Describe a realistic triggering condition.
3. Explain the consequence and why the behavior is incorrect or risky.
4. Assign severity using this scale: Critical (immediate severe impact), High (major failure/security risk), Medium (meaningful defect), Low (limited impact). Explain the basis rather than inflating severity.
5. Provide a minimal correction or test that would address it.
6. State confidence and any missing context that could invalidate the finding.

Inspect relevant areas including logic and edge cases, data validation, error handling, authorization, concurrency, resource cleanup, compatibility, performance, and tests. Do not force every category to have a finding.

If test output is supplied, interpret it accurately. If tests were not run or you cannot run them, say so. Never claim a vulnerability is exploitable without adequate evidence; describe the suspected path and verification needed.

Output: Summary Verdict; Findings (highest severity first); Positive Design Notes; Missing Tests; Questions for the Author; Unverified Areas; Merge Recommendation.

A finding-free review is acceptable only if no actionable defect is supported by the evidence. Do not manufacture issues to fill the report.
```

**Expected deliverable:** A prioritized review report with actionable, evidence-backed findings rather than vague style feedback.

**Customization notes:** Provide a diff whenever possible, plus the ticket and relevant surrounding code. Include test logs if you want conclusions about test behavior.

---

## Prompt 010 — Choose Between Technical Options with a Decision Record

**Category:** Claude Power User Workflows

**Use case:** A team must choose between libraries, architectures, databases, deployment models, or implementation approaches.

**Objective:** Compare options against explicit criteria and produce a decision record that can be revisited later.

**Prompt:**
```text
You are a software architect facilitating a defensible technical decision.

Decision to make: [DECISION]
Options under consideration: [OPTIONS]
System context: [SYSTEM_CONTEXT]
Constraints: [CONSTRAINTS]
Decision participants or owner: [OWNER_OR_UNKNOWN]

Do not select an option based on familiarity alone. Separate hard constraints from weighted preferences. If critical requirements are missing, ask for them or clearly label a provisional analysis.

1. Write a concise decision statement and explain why the decision is needed now.
2. Define decision criteria, their importance, and what evidence would demonstrate that each criterion is met. Do not assign precise weights unless justified; if using weights, label them as stakeholder-proposed.
3. Evaluate each option consistently across functionality, complexity, cost, security, performance, operability, team capability, ecosystem health, reversibility, and lock-in where relevant.
4. Separate known facts, sourced claims, estimates, and subjective judgments. Flag information that requires current documentation or a proof of concept.
5. Identify the strongest argument against the leading option and conditions under which another option would be better.
6. Recommend a small experiment if the decision depends on uncertain performance, integration, or maintenance assumptions.
7. State the decision, rationale, rejected alternatives, consequences, migration implications, and triggers that should cause reconsideration.
8. Produce an Architecture Decision Record (ADR) draft with status set to Proposed unless approval was explicitly provided.

Output: Decision Statement; Criteria; Comparison Matrix; Evidence and Uncertainty; Counterargument; Validation Experiment; Proposed ADR; Revisit Triggers.

Do not imply consensus or approval that has not occurred. Avoid fake precision in scoring and avoid presenting an estimate as a measured result.
```

**Expected deliverable:** A transparent comparison and reusable ADR draft documenting the rationale and consequences.

**Customization notes:** List real options and constraints. If stakeholders disagree on criteria, surface the disagreement before scoring the options.

---

## Prompt 011 — Create a Context Handoff for a Long-Running Project

**Category:** Claude Power User Workflows

**Use case:** Work is moving to a new session, teammate, or AI assistant and important decisions may be lost.

**Objective:** Create a compact but sufficient handoff that distinguishes completed work from plans and open issues.

**Prompt:**
```text
You are a technical project maintainer preparing a handoff that allows another engineer or AI session to continue safely without relying on hidden conversation history.

Project: [PROJECT_NAME_AND_GOAL]
Available conversation, notes, files, and logs: [MATERIALS]
Next milestone: [NEXT_MILESTONE]

Use only supplied material. Do not claim access to prior sessions, files, systems, or decisions unless their contents are included or available through an actual tool. Preserve important names, paths, versions, commands, and constraints exactly.

Create the handoff with these steps:
1. Summarize the product or engineering goal and the current state in a few precise sentences.
2. Record decisions already made, including rationale and source evidence where available. Distinguish approved decisions from proposals.
3. List completed work and the evidence for completion. Mark tasks as complete only when the material supports that status.
4. List current architecture, relevant files, commands, environment requirements, integrations, and reproducible setup steps that are actually known.
5. Record bugs, failed attempts, error messages, test outcomes, and approaches ruled out. Do not omit a failed approach if repeating it would waste time.
6. Create an open-work queue prioritized by dependency and impact. For each item, include the next action, expected result, acceptance test, and blocking question.
7. Identify risky actions that require approval, such as destructive migrations, production changes, spending, or handling secrets.
8. List unknowns and missing artifacts. Do not fill gaps with plausible guesses.
9. Provide a short “start here” sequence for the next person and a set of questions they should ask before changing anything.
10. Verify that the handoff is self-contained and does not refer vaguely to “the previous chat.”

Output: Project Snapshot; Confirmed Decisions; Completed and Verified Work; Environment and File Map; Failed Attempts; Next Actions; Risks and Approval Gates; Unknowns; Start-Here Checklist.

Keep the handoff concise enough to scan but detailed enough to reproduce the next step. Never include credentials, access tokens, or private keys; refer to secret names only when necessary.
```

**Expected deliverable:** A portable project snapshot that preserves decisions, evidence, failure history, and the next safe action.

**Customization notes:** Include the relevant history and artifacts. If no test evidence is available, mark status as reported or unverified rather than complete.

---

## Prompt 012 — Improve an Existing Prompt Without Changing Its Intent

**Category:** Claude Power User Workflows

**Use case:** A prompt produces inconsistent or generic output, but its underlying objective must remain intact.

**Objective:** Diagnose prompt failure modes and deliver an improved version with a test plan.

**Prompt:**
```text
You are an expert prompt designer specializing in reliable, testable instructions for Claude.

Original prompt: [ORIGINAL_PROMPT]
Observed weak outputs or failure cases: [EXAMPLES_OR_NONE]
Intended user and task: [INTENDED_USE]
Required output format: [OUTPUT_FORMAT]
Constraints that must not change: [NON_NEGOTIABLES]

Preserve the original intent. Do not add capabilities, tools, permissions, data sources, or business rules that the user did not authorize.

1. Diagnose the prompt's likely weaknesses: ambiguous verbs, missing context, conflicting instructions, underspecified outputs, hidden assumptions, excessive scope, absent edge cases, or unverifiable success criteria.
2. Separate defects demonstrated by examples from risks inferred from the wording.
3. Identify the minimum changes needed to improve reliability. Avoid adding length unless it provides an operational benefit.
4. Rewrite the prompt with clear role, task, input boundaries, workflow, constraints, output schema, uncertainty handling, and completion checks as appropriate.
5. Add placeholders only where user-specific information is truly needed. Explain each placeholder briefly.
6. Include explicit instructions against fabricated facts, sources, tool access, and test results when relevant to the task.
7. Design a small evaluation set of at least 5 representative test cases, including one ambiguous input and one edge case. Define observable pass/fail criteria.
8. Compare the original and revised prompts against the same criteria. If you cannot execute the tests, label the comparison as a proposed evaluation, not measured performance.
9. Check that the revised prompt still satisfies every non-negotiable constraint and has not drifted into a different task.

Output: Intent to Preserve; Failure Diagnosis; Revised Copy-Ready Prompt; Change Log; Placeholder Guide; Evaluation Cases; Pass/Fail Rubric; Remaining Risks.

Do not claim the rewrite is proven better without evaluation evidence. Avoid empty instructions such as “be smarter” or “give the best answer”; express improvements as observable behaviors.
```

**Expected deliverable:** An improved, copy-ready prompt plus a practical way to evaluate whether it actually performs better.

**Customization notes:** Include a few bad outputs if possible. Real examples make diagnosis more reliable than prompt wording alone.

---

## Prompt 013 — Validate a Deliverable Against a Strict Rubric

**Category:** Claude Power User Workflows

**Use case:** A report, specification, code patch, or other artifact must meet a defined checklist before handoff.

**Objective:** Perform a traceable pass/fail audit without grading the work generously or inventing missing evidence.

**Prompt:**
```text
You are an independent quality auditor. Your job is to evaluate the supplied artifact against the supplied rubric, not to defend the author or rewrite the criteria.

Artifact: [ARTIFACT_OR_FILES]
Authoritative rubric: [RUBRIC]
Relevant source requirements: [SOURCE_REQUIREMENTS]
Allowed validation tools: [AVAILABLE_TOOLS]

1. Parse the rubric into atomic criteria with stable IDs. Preserve any mandatory thresholds and exact wording that affects compliance.
2. For each criterion, identify the evidence required to pass and where that evidence appears in the artifact. Use precise locators when available.
3. Assign only these statuses: Pass, Fail, Partial, or Not Verifiable. Explain each status in one or two evidence-based sentences.
4. Distinguish a criterion that is genuinely unmet from one that cannot be assessed because evidence or tools are missing.
5. Check internal consistency, completeness, edge cases, source traceability, formatting requirements, and any task-specific safety constraints.
6. Do not infer that a feature works because it is described, that code runs because it looks plausible, or that a claim is true because it sounds reasonable.
7. Prioritize failures by severity and downstream consequence. Propose the smallest corrective action for each failure.
8. If the artifact can be changed in this session, do not modify it unless explicitly asked. This task is an audit only.
9. Recheck the final status table for unsupported passes and criteria that were accidentally omitted.

Output: Audit Scope; Criterion-by-Criterion Results (ID, status, evidence, issue, correction); Critical Failures; Not-Verifiable Items; Overall Readiness; Remediation Checklist.

Do not create a numerical score unless the rubric defines one or the scoring method is explicitly labeled as a proposed estimate. State what was inspected and what was not.
```

**Expected deliverable:** A rigorous, evidence-linked audit table and a prioritized remediation list.

**Customization notes:** Provide the actual rubric and artifact. If no rubric exists, ask Claude to propose one separately and label it as proposed before using it to grade.

---

## Prompt 014 — Analyze Documentation for Gaps and Contradictions

**Category:** Claude Power User Workflows

**Use case:** Technical documentation may be incomplete, stale, inconsistent, or out of sync with implementation.

**Objective:** Audit documentation coverage and produce actionable corrections tied to evidence.

**Prompt:**
```text
You are a technical documentation auditor comparing documentation against the implementation evidence supplied to you.

Documentation: [DOCS_FILES_OR_TEXT]
Implementation evidence: [CODE_FILES_CONFIGS_OR_API_SCHEMA]
Intended readers: [AUDIENCE]
Documentation purpose: [PURPOSE]

Do not assume the implementation is correct or that documentation is authoritative. Treat each as a source to compare. If only one side is supplied, limit conclusions accordingly.

1. Inventory the documents and implementation artifacts actually available. Record versions or dates when visible.
2. Map important documented behaviors to implementation evidence, including setup, configuration, API contracts, error handling, permissions, limits, and operational procedures where relevant.
3. Find missing steps, stale names, contradictory values, undocumented prerequisites, unclear examples, broken conceptual flows, and claims that cannot be verified.
4. Classify each finding as documentation omission, documentation/implementation mismatch, implementation ambiguity, or unverifiable claim.
5. For each finding, provide a source locator, user impact, severity, and proposed correction. Do not rewrite a disputed behavior as fact until its owner confirms the intended behavior.
6. Identify the smallest set of changes that would remove the most user confusion.
7. Draft corrected text only for facts supported by evidence. Put unresolved content in clearly marked questions or placeholders.
8. Check examples for consistency with visible interfaces, configuration keys, versions, and response shapes.

Output: Scope; Documentation Map; Gap and Contradiction Register; High-Priority Fixes; Proposed Replacement Text; Questions for Owners; Verification Checklist.

Do not invent endpoints, flags, defaults, environment variables, or screenshots. If execution is unavailable, do not claim examples were run.
```

**Expected deliverable:** A prioritized documentation audit and evidence-backed replacement text where the intended behavior is clear.

**Customization notes:** Include docs and the matching code, schema, or release notes. Tell Claude which version is deployed if that is known.

---

## Prompt 015 — Resolve Ambiguity with Minimal, High-Value Questions

**Category:** Claude Power User Workflows

**Use case:** A request is missing details and asking too many questions would slow progress, but guessing could be costly.

**Objective:** Identify only the clarifications that materially affect correctness, safety, or scope.

**Prompt:**
```text
You are a requirements facilitator. Determine whether the task can proceed safely with reasonable assumptions or requires clarification first.

Request: [REQUEST]
Known context: [CONTEXT]
Potential consequences of a wrong interpretation: [IMPACT_CONTEXT]

1. Identify the possible interpretations of the request that are plausible from the supplied wording.
2. For each ambiguity, estimate its consequence if guessed incorrectly: low, medium, or high. Explain the basis briefly.
3. Ask a question only if the answer could materially change the output, architecture, data handling, cost, permissions, or user-visible behavior.
4. Rank questions by decision value. Prefer one clear question that resolves multiple uncertainties over a long questionnaire.
5. For low-risk ambiguity, state a reasonable assumption and proceed with a reversible draft if that is useful.
6. For high-impact ambiguity, stop before execution and ask for clarification. This includes destructive operations, production changes, spending, security-sensitive decisions, and actions affecting other people or data.
7. If several options are easy to compare, present a short set of choices with the consequences of each. Do not use a choice list when a direct question is clearer.
8. After receiving answers, update the assumptions and scope rather than repeating resolved questions.

Output: Can Proceed?; Material Ambiguities; Highest-Value Question(s); Safe Assumptions; Stop Conditions; Provisional Next Step.

Do not ask for information already supplied. Do not manufacture certainty to avoid asking a necessary question. Keep the interaction proportionate to the task's risk.
```

**Expected deliverable:** A short, prioritized clarification strategy that minimizes unnecessary back-and-forth while preventing costly assumptions.

**Customization notes:** Describe the impact of mistakes. For low-risk drafting tasks, allow a provisional output; for consequential actions, require confirmation.

---

## Prompt 016 — Maintain an Explicit Assumption and Decision Ledger

**Category:** Claude Power User Workflows

**Use case:** A project accumulates assumptions and small decisions that can become hidden sources of defects.

**Objective:** Create a ledger that tracks each assumption's evidence, risk, owner, and validation path.

**Prompt:**
```text
You are a project analyst maintaining an assumption and decision ledger for a technical project.

Project materials: [NOTES_REQUIREMENTS_CODE_OR_DISCUSSION]
Project goal: [GOAL]
Known decisions: [DECISIONS_OR_NONE]

Extract only assumptions and decisions supported by the supplied material. Do not invent an owner, date, approval, or rationale. Mark absent values as unknown.

1. Identify assumptions: statements treated as true without sufficient confirmation. Include implicit assumptions that materially affect design or delivery.
2. Identify decisions: choices explicitly made or approved. Separate approved decisions from proposals and recommendations.
3. Assign each record a stable ID and type: Assumption, Decision, Constraint, or Open Question.
4. For assumptions, record statement, evidence, confidence, consequence if false, validation method, owner if known, and status.
5. For decisions, record context, chosen option, alternatives considered if present, rationale, consequences, approval evidence, and conditions that should trigger reconsideration.
6. Rank validation priority using consequence and uncertainty. Avoid false precision; explain the ranking method.
7. Identify assumptions that conflict with one another or with explicit constraints.
8. Recommend the next few validations that would reduce the greatest project risk.
9. Preserve history when a decision changes: show superseded decisions and the evidence for the update rather than deleting the old record.

Output: Ledger Summary; Assumption Register; Decision Register; Constraint Register; Conflicts; Validation Queue; Reconsideration Triggers.

Do not mark an assumption as verified merely because it appears in several notes. Repetition is not independent evidence. Do not treat a recommendation as an approved decision.
```

**Expected deliverable:** A maintainable ledger that makes uncertainty and decision ownership visible.

**Customization notes:** Supply project notes or a decision log. Update the ledger after major reviews so old assumptions do not silently persist.

---

## Prompt 017 — Orchestrate a Multi-Step Workflow with Checkpoints

**Category:** Claude Power User Workflows

**Use case:** A complex task must move through research, planning, production, and review without losing control of scope or approval.

**Objective:** Define a checkpoint-driven workflow that prevents downstream work from depending on unreviewed assumptions.

**Prompt:**
```text
You are a workflow architect designing a controlled multi-step process for the task below.

Goal: [WORKFLOW_GOAL]
Inputs: [INPUTS]
Available tools and integrations: [TOOLS_ACTUALLY_AVAILABLE]
Required deliverables: [DELIVERABLES]
Risk level and constraints: [RISKS_AND_CONSTRAINTS]

Design the workflow; do not execute external actions unless separately authorized. Do not assume tool access beyond what is explicitly available.

1. Break the goal into stages with clear inputs, outputs, owners where known, and entry/exit criteria.
2. Map dependencies and identify which stages can run independently and which require an approved prior result.
3. Define checkpoints where a human should review quality, scope, safety, or irreversible decisions.
4. For each stage, define validation tests, failure signals, retry limits, and what information must be preserved for recovery.
5. Specify what happens when a required input is missing, a tool fails, evidence conflicts, or a stage produces a partial result.
6. Prevent silent progression past failed mandatory checks. Distinguish warnings from blockers.
7. Define idempotency or duplicate-prevention measures for steps that may be retried or repeated.
8. Specify logging and audit records without collecting unnecessary sensitive data.
9. Define stop conditions and the conditions required to resume after a stop.
10. Walk through one normal scenario and at least two failure scenarios to test the workflow design.

Output: Workflow Overview; Stage Table; Dependency Map; Approval Checkpoints; Failure and Retry Policy; Audit Records; Example Runs; Stop/Resume Rules; Acceptance Checklist.

Do not describe a proposed workflow as implemented. Flag any stage that requires a capability or integration not currently available.
```

**Expected deliverable:** A checkpoint-driven workflow with explicit failure behavior, approvals, and recovery rules.

**Customization notes:** List the tools you actually have and identify irreversible actions. This prompt is for designing the workflow, not granting permission to execute it.

---

## Prompt 018 — Resolve a Technical Disagreement with a Neutral Evidence Review

**Category:** Claude Power User Workflows

**Use case:** Engineers or stakeholders disagree about a design, bug cause, or implementation strategy.

**Objective:** Compare competing claims fairly and identify evidence or experiments that can settle the disagreement.

**Prompt:**
```text
You are a neutral technical facilitator. Your role is to clarify the disagreement and evaluate the evidence, not to pick a side based on confidence, seniority, or rhetorical strength.

Question under dispute: [DISPUTED_QUESTION]
Position A and supporting evidence: [POSITION_A]
Position B and supporting evidence: [POSITION_B]
System constraints: [CONSTRAINTS]
Available logs, code, metrics, or documentation: [EVIDENCE]

1. Restate the precise point of disagreement in terms both sides could recognize.
2. Separate factual claims, assumptions, value judgments, and different interpretations of the goal.
3. Assess each claim against the available evidence. Identify evidence that supports, weakens, or does not address it.
4. Check whether the positions rely on different versions, environments, definitions, time periods, or success metrics.
5. Give each side its strongest reasonable argument before evaluating weaknesses. Do not create false balance when one claim is clearly contradicted by evidence.
6. State what can be concluded now, what remains uncertain, and what cannot be inferred from the current evidence.
7. Propose the smallest fair test, measurement, code inspection, or source check that could distinguish the competing explanations. Define expected outcomes for each hypothesis.
8. Identify any decision that is a matter of priorities rather than factual correctness, and recommend who should decide it.
9. Provide a neutral summary suitable for sharing with both sides.

Output: Shared Problem Statement; Claim Comparison; Evidence Table; Common Ground; Current Conclusion; Discriminating Test; Decision Owner or Next Step.

Do not invent measurements or attribute statements to people beyond the supplied text. If evidence is asymmetric, explain why rather than forcing a tie.
```

**Expected deliverable:** A neutral, evidence-based resolution brief and a concrete experiment or decision path.

**Customization notes:** Include the actual competing arguments and any relevant logs or data. Remove personal commentary that is unrelated to the technical issue.

---

## Prompt 019 — Prepare a Reliable Technical Handoff Between Teams

**Category:** Claude Power User Workflows

**Use case:** A project or component is moving from one team to another, and operational ownership must be clear.

**Objective:** Create a handoff package covering contracts, dependencies, operating procedures, known risks, and acceptance of ownership.

**Prompt:**
```text
You are a senior technical program engineer preparing a cross-team handoff for [COMPONENT_OR_PROJECT].

Sending team: [SENDING_TEAM]
Receiving team: [RECEIVING_TEAM]
Scope of transfer: [SCOPE]
Available technical artifacts: [ARTIFACTS]
Handoff deadline or milestone: [DATE_OR_UNKNOWN]

Use only supplied evidence. Do not imply the receiving team has accepted ownership until acceptance is explicitly recorded.

1. Define what is transferring and what remains outside the handoff boundary.
2. Document system purpose, architecture, interfaces, dependencies, data flows, environments, configuration, and external service assumptions that are actually known.
3. Identify service expectations, monitoring, alerts, runbooks, backup and recovery, incident escalation, and support boundaries. Mark missing operational procedures as gaps.
4. Record security responsibilities, access requirements, secret-handling procedures, data sensitivity, and approval boundaries. Never include actual secret values.
5. List known defects, technical debt, incidents, workarounds, limitations, upcoming changes, and unresolved decisions.
6. Provide reproducible setup and validation steps, including expected outputs where known. Do not invent commands or assert they were tested unless evidence exists.
7. Define the receiving team's acceptance checklist and the evidence required for each item.
8. Identify risks created by transferring incomplete knowledge or unclear ownership, with mitigation and responsible party where known.
9. Create a handoff meeting agenda focused on decisions and demonstrations rather than reading the document aloud.

Output: Handoff Scope; System and Interface Map; Operational Readiness; Security and Access; Known Issues; Setup and Validation; Responsibility Matrix; Acceptance Checklist; Open Risks; Handoff Agenda.

Mark every critical item as Confirmed, Missing, or Not Verified. Do not disguise missing runbooks, monitoring, or ownership as completed work.
```

**Expected deliverable:** A cross-team handoff package that makes scope, responsibilities, readiness, and gaps explicit.

**Customization notes:** Fill in team names and scope, then attach the runbooks, architecture docs, and relevant logs. Treat ownership acceptance as a separate explicit step.

---

## Prompt 020 — Perform a Final Deliverable Readiness Review

**Category:** Claude Power User Workflows

**Use case:** A technical deliverable is about to be handed to a client, published, merged, or released.

**Objective:** Verify completeness and evidence quality, identify release blockers, and report exactly what remains unverified.

**Prompt:**
```text
You are an independent release-readiness reviewer. Evaluate the deliverable against its original requirements and available verification evidence.

Deliverable: [DELIVERABLE_OR_FILES]
Original requirements and acceptance criteria: [REQUIREMENTS]
Required delivery format: [FORMAT]
Verification evidence: [TESTS_REVIEWS_CHECKS_OR_NONE]
Release constraints: [CONSTRAINTS]

Do not change the deliverable unless explicitly asked. Do not treat polished presentation as proof of correctness. Use only evidence available in this session or through tools actually accessible to you.

1. Confirm the scope of the review and list the exact files, sections, outputs, or test results inspected.
2. Map every original requirement to the corresponding artifact location and verification evidence.
3. Mark each requirement Pass, Fail, Partial, or Not Verified. Explain the status with concise evidence.
4. Check the deliverable for missing sections, unfinished placeholders, inconsistent terminology, broken references, formatting problems, unsupported claims, and mismatch with the requested format.
5. For code or technical artifacts, distinguish static inspection from executed tests. Report actual commands and outcomes only when they are available. Identify tests that were not run.
6. Review relevant security, privacy, compatibility, accessibility, operational, and recovery requirements; do not invent requirements but flag obvious risks that need owner review.
7. Identify blockers that should prevent release, non-blocking improvements, and issues requiring explicit owner acceptance.
8. Produce a short remediation queue ordered by severity and dependency. For each item, specify a completion test.
9. Re-run the checklist logically against the evidence after any corrections only if the corrected artifact is actually available for inspection.
10. Give a readiness verdict: Ready, Ready with Accepted Risks, or Not Ready. Explain the threshold and list the exact conditions behind the verdict.

Output: Review Scope; Requirement Traceability Matrix; Quality Findings; Verification Evidence; Security and Operational Notes; Release Blockers; Remediation Queue; Readiness Verdict; Final Completion Checklist.

Never say “all tests pass” unless test results prove it. Never mark an item complete because it was planned. If the evidence is insufficient, choose Not Verified and state what would verify it.
```

**Expected deliverable:** A release-readiness report with requirement traceability, honest test status, blockers, and a defensible final verdict.

**Customization notes:** Attach the final artifact and its original acceptance criteria. Supply CI output or review evidence if you want the audit to assess those checks.

---

# Batch 1 Completion Manifest

- **Completed:** Prompts 001–020.
- **Category:** 01 — Claude Power User Workflows.
- **Unfinished entries in this batch:** None.
- **Next batch:** Prompts 021–040 — AI Engineering & LLM Applications.
- **Important limitation:** This is a prompt-pack draft based on the supplied master brief. The prompts have been designed to be standalone and differentiated, but a final cross-batch duplication audit should be performed after all 200 prompts exist.
