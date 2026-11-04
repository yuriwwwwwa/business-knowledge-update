---
name: business-knowledge-update
description: Maintain a specified business knowledge base using the current requirement, final code changes, and tests. Invoke explicitly with a target knowledge-base path; includes a separate document quality optimization stage.
---

# Business Knowledge Update

Run only when explicitly requested. Maintain `{knowledge_path}` using the current requirement and actual code changes. `{knowledge_path}` is a user-supplied file or directory path for the knowledge documents, not a literal placeholder to create. Invocation: `$business-knowledge-update <knowledge_path>`. If the path cannot be determined from the request, ask for it before editing. Resolve the affected repositories and Git comparison scope from the current task; request missing context rather than assuming that an empty working-tree diff means no changes.

Write accurate, readable Chinese business knowledge that developers can understand and Agents can retrieve and reuse. Modify knowledge documents only; do not modify business code or publish remote documents without explicit instruction. Preserve the existing structure and style and limit changes to capabilities actually affected by this requirement.

## Stage 1: Extract business-rule changes

1. Read the current requirement, confirmed decisions, relevant Git diffs (including committed changes and working-tree changes within the task scope), final source, and relevant tests. Distinguish tests inspected from tests actually run and passing.
2. Search existing business terms, aliases, rule documents, and code mappings before drafting. Resolve different names through business semantics, data models, and implementation, not names alone.
3. Identify added, changed, and retired rules and the affected business capabilities. Map each proposed rule change to its requirement, code entry points, core implementation, and tests. Use final code and tests as implementation evidence and check against confirmed business requirements; a conflict is not permission to silently replace business intent with implementation behavior.
4. Mark conflicts, ambiguity, unsupported claims, and unconfirmed behavior as pending confirmation. Do not invent missing rules. Consult historical Yuque requirements only when needed to resolve a specific evidence gap; keep historical context distinct from current rules.

## Stage 2: Generate or update knowledge documents

1. Prefer updating existing terminology and rule documents. Create a document only for a genuinely independent business capability; do not duplicate equivalent knowledge.
2. Describe current effective behavior, applicability, triggers, actions, outcomes, priorities, exceptions, mutual exclusions, and boundaries. Within affected capabilities, preserve a complete account of current behavior, not just the latest delta. Do not expand into unrelated capabilities.
3. Maintain business terms and aliases, existing business IDs and rule IDs, terminology references, code entry points, core implementation paths, test locations, and valid links. Do not rename existing identifiers without explicit instruction. Follow existing rule-ID conventions when a new confirmed rule needs an identifier.
4. Replace superseded descriptions with verified current rules rather than accumulating iteration history. Keep verification scope, pending questions, and implementation evidence clearly separated from confirmed rules.

## Stage 3: Optimize document quality

Treat the output of Stage 2 as the semantic baseline. This stage changes language, organization, and Markdown only: do not add, delete, or alter any recorded business rule, condition, boundary, state, or outcome. Do not modify business code.

### Language

- Use accurate, natural, concise Chinese centered on business behavior and rules. Avoid code translation, execution logs, and analysis-report prose.
- Give each paragraph one clear topic; separate workflows, decision conditions, exception handling, and implementation details when they represent different topics.
- State scenarios, triggers, actions, and results explicitly, including exceptions, priorities, and mutual exclusions where applicable.
- Use consistent terminology and preserve names with specific business meanings; retain aliases and terminology indexes when useful.
- Avoid both incomplete compression and repeated explanations of the same rule.

### Structure

- Organize by business capability, business process, and rule topic, not code execution order, classes, or methods.
- Use precise headings with clear hierarchy; avoid vague headings or unrelated topics under one heading.
- Prefer paragraphs for context and behavior, tables for combinations of conditions, states, outcomes, or rule comparisons, and Mermaid for complex flows when useful.
- Group numerous rules by business scenario and explain dependencies, priorities, and exceptions instead of presenting context-free lists.
- Link IDs, terminology references, and code evidence to the corresponding rules without flooding prose with metadata.
- Group verification scope, pending questions, and implementation evidence separately from confirmed rules.
- Keep heading levels, paragraph spacing, lists, tables, code fences, Mermaid, and internal links consistent in Markdown.

### Knowledge quality and preservation

- Fully describe current behavior within the affected capability, highlighting easily misunderstood or duplicated rules and relationships and boundaries with other capabilities.
- Separate business rules from implementation. Retain technical details only when they support business meaning, troubleshooting, or implementation reuse.
- Keep useful information density; avoid requirement diaries, line-by-line source explanations, and overly broad summaries.
- Improve existing sections instead of forcing a universal template; adapt organization to the capability.
- Preserve all business IDs, rule IDs, terminology references, evidence associations, and effective links. Never promote pending content into confirmed facts or supplement behavior from experience.
- If the baseline is ambiguous, conflicting, or unsupported, preserve its factual content and list the issue separately; do not silently repair its meaning.

## Stage 4: Check rule consistency and report

1. Compare the updated documents with final source, relevant tests, and confirmed requirements. Verify that Stage 2 captures only evidenced changes and that Stage 3 preserves its semantic baseline.
2. Check semantic completeness, rule traceability, retained identifiers, terminology consistency, duplicate rules, and separation of confirmed rules from uncertainty.
3. Check local links and anchors, Markdown structure, and Mermaid syntax; inspect rendered output when a renderer is available. Do not claim remote links or rendering were verified if they were not checked.
4. Report updated document paths, affected business capabilities, rule changes, main structural improvements, and pending questions. Summarize checks and limitations without explaining every wording edit. If no update is needed, explain why.
