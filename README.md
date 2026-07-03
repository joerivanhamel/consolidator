# Content Consolidation & Information Gain Engine (v1.3)

A structured, state-machine prompt designed to assist in consolidating multiple documents or web pages before setting up 301 redirects. This engine identifies unique information-gain deltas from secondary pages slated for decommissioning, filters them through intent guardrails to prevent content pollution, and outputs standardized integration blocks (SDIB) for consistent copy-pasting.

---

## Key Features

* **Strict State Machine Workflow**: Operates across 7 sequential, phase-gated states to ensure a highly structured analysis.
* **Zero-Trust Verification**: Enforces complete document reading by outputting verification cards with extractive verbatim quotes before processing.
* **Intent Guardrails**: Defines "Approved" and "Forbidden" content taxonomies to match the primary document's user intent (e.g., maintaining a transactional focus on product pages).
* **Standardized Delta Integration Blocks (SDIB)**: Outputs all approved modifications in an identical, highly rigid markdown structure, making it easy to merge outputs from multiple runs into a single master document.
* **JSON Metadata Payload**: Concludes with a clean, machine-readable JSON summary mapping the decommissioned sources and redirect scopes.

---

## State Architecture

The engine progresses strictly through the following states:

1. **[STATE 1: SOURCE_INGEST]** - Collects documents one at a time, beginning with the primary document and its intent type.
2. **[STATE 2: INGEST_VERIFY]** - Verifies whole-document ingestion via verbatim quote checks.
3. **[STATE 3: INTENT_GUARDRAILS]** - Establishes acceptable content taxonomies based on page intent.
4. **[STATE 4: DELTA_EXTRACTION]** - Identifies all unique facts, data points, or topics present only in the secondary documents.
5. **[STATE 5: DELTA_AUDIT]** - Audits each delta for redundancy, intent-fit, and format (categorized as `INTEGRATE`, `ADAPT`, or `DISCARD`).
6. **[STATE 6: RECONCILIATION_BLUEPRINT]** - Outputs integration instructions using the standardized SDIB schema.
7. **[STATE 7: COMPLETE]** - Emits the final JSON metadata payload and concludes the workflow.

---

## How to Use

1. **Copy the Prompt**: Copy the entire markdown content of the prompt from the `content-consolidation-delta-engine.md` file in this repository.
2. **Paste into an LLM**: Paste the prompt into a fresh conversation with a capable LLM (Claude 3.5 Sonnet, GPT-4o, or similar models).
3. **Follow the State Instructions**: The model will initiate **STATE 1** and prompt you for the primary document. Respond to the steps as requested, typing `Proceed` when prompted to advance the state machine.
4. **Compile the Output**: Copy the standardized `[CONSOLIDATION-DELTA]` blocks directly into your content management system or master editorial document.

---

## Standardized Output Schema (SDIB)

Every approved delta is formatted exactly as follows:

```markdown
### [CONSOLIDATION-DELTA: {Candidate_ID}]
*   **Source Document:** `{Document_Identifier}`
*   **Topic:** `{Brief_Subject_Name}`
*   **Reason for Integration:** `{Reason}`
*   **Integration Type:** `{INTEGRATE | ADAPT}`
*   **Verbatim Source Copy:**
    > {Verbatim copy directly from the secondary document}
*   **Draft/Adapted Copy:**
    > {Draft of adapted copy if required, or N/A}
*   **Suggested Target Location:** `{Suggested structural section in primary document}`
