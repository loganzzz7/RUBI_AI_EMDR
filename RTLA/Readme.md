## Rubi Therapeutic Language Architecture (RTLA)

### Project Overview
The Rubi Therapeutic Language Architecture (RTLA) serves as the foundational clinical communication specification for an offline-capable Small Language Model (SLM) embedded within Rubi—an AI-guided immersive virtual reality platform for early trauma intervention. Designed to provide structured, evidence-informed support during the peritraumatic period (the hours and days immediately following a traumatic event), the system supports rather than replaces licensed clinical professionals.

The linguistic core integrates concepts from Eye Movement Desensitization and Reprocessing (EMDR), Accelerated Resolution Therapy (ART), and Psychological First Aid (PFA).

### Core Project Goal

The ultimate goal of this project is to construct a fully structured communication database consisting of **1,500 to 2,000 clinician-review phrases** distributed across 38 distinct therapeutic modules. Every phrase maps to a rigorous 22-field metadata schema to ensure strict engineering traceability, clinical safety, and explicit evidence provenance.

---

## Repository Architecture

The project is structured hierarchically by layer/phase. Each phase directory contains a markdown briefing document outlining the phase mechanics and a CSV database holding the targeted phrase library.

```text
rubi-rtla/
├── README.md                          # Overall project summary and architecture
├── layer_one_safety_architecture/
│   ├── phase_one_brief.md
│   ├── p1_m1_library.csv
│   ├── p1_m2_library.csv
│   ├── p1_m3_library.csv
│   ├── p1_m4_library.csv
│   ├── p1_m5_library.csv
│   ├── p1_m6_library.csv
│   ├── p1_m7_library.csv
│   ├── p1_m8_library.csv
│   ├── p1_m9_library.csv
│   └── p1_m10_library.csv
├── layer_two_therapeutic_alliance/
│   ├── phase_two_brief.md                 
│   └── phrase_two_library.csv             
├── layer_three_stabilization/
│   ├── phase_three_brief.md
│   └── phrase_three_library.csv
├── layer_four_trauma_processing/
│   ├── phase_four_brief.md                 
│   └── phrase_four_library.csv 
├── layer_five_session_closure/
│   ├── phase_five_brief.md
│   └── phrase_five_library.csv           
└── layer_six_human_escalation/
    ├── phase_six_brief.md
    └── phrase_six_library.csv
```

---

## Phrase Composition Allocation

### Phrase Library Target Distribution

The `phrase_library.csv` adheres to the following target distribution:

| Category | Allocation | Description / Target |
|:---------|:----------:|:---------------------|
| **Clinician-Approved Phrases** | **70%** | The core operating vocabulary used by the SLM during clinically safe conversations. These phrases should be evidence-based, medically accurate, and representative of expected production behavior. |
| **Linguistic Variants** | **15%** | Semantically equivalent rephrasings of approved phrases that improve linguistic diversity, reduce repetitive responses, and increase model robustness without changing clinical intent. |
| **Boundary Cases** | **10%** | Phrases containing minor clinical inaccuracies, ambiguous wording, or subtle guideline deviations used to evaluate classifier sensitivity near decision boundaries. |
| **Deliberately Unsafe Phrases** | **5%** | Clearly unsafe, misleading, or clinically inappropriate phrases included exclusively for negative evaluation, safety classifier validation, and robustness testing. These samples must never be used for production inference. |

> **CRITICAL CONFIGURATION NOTICE:** The 5% deliberately unsafe phrases and 10% boundary cases are **segregated** and serves as a strict restricted list to ensure the SLM never delivers them to an active user.

### Phrase Dataset Schema (`phrase_library.csv`)

Each row in `phrase_library.csv` represents a single therapeutic phrase and must contain the following metadata fields to ensure clinical traceability, safety validation, and engineering reproducibility.

| Field | Description |
|:------|:------------|
| **Phrase ID** | Unique identifier for each phrase (e.g., `P-2050001`). |
| **Module ID** | Parent RTLA module associated with the phrase (e.g., `L2.05`). |
| **Layer** | Architectural layer within the RTLA framework (Layers 1–6). |
| **Phase** | Session phase in which the phrase is intended to be used (e.g., Opening, Stabilization, Processing, Closing). |
| **Therapeutic Intent** | High-level therapeutic rationale describing the purpose of the phrase. |
| **Clinical Objective** | Specific clinical outcome or behavioral goal the phrase is designed to achieve. |
| **Exact Phrase** | The verbatim therapeutic text presented to the user. |
| **Population Flag** | Applicable population(s), such as `Adult`, `Youth`, `Military`, `Complex PTSD`, or `Humanitarian`. |
| **Language Complexity** | Intended reading complexity (e.g., Elementary, Middle School, High School, Adult). |
| **Estimated Reading Level** | Flesch–Kincaid grade level for readability assessment. |
| **Emotional Tone** | Primary communication tone (e.g., Calm, Warm, Directive, Neutral, Empathic). |
| **Therapeutic Function** | Functional role of the phrase (e.g., Validation, Reflection, Grounding, Instruction, Question, Consent, Safety, Psychoeducation). |
| **Evidence Level** | Clinical evidence supporting the phrase (e.g., Strong, Moderate, Emerging, Expert Consensus). |
| **Primary Source** | Clinical guideline, publication, or reference from which the phrase originates (e.g., WHO PFA, EMDRIA, SAMHSA). |
| **Source Type** | Origin classification, such as Direct Guideline Language, Adapted Clinical Language, Synthesized Best Practice, or Expert Consensus. |
| **Safety Rating** | Safety classification (`SAFE`, `REQUIRES HUMAN REVIEW`, or `UNSAFE`). |
| **Contraindications** | Situations or patient conditions in which the phrase should not be used. |
| **Known Failure Modes** | Potential risks, limitations, or unintended outcomes associated with the phrase. |
| **Recommended Follow-up** | Suggested subsequent phrase or therapeutic action following successful delivery. |
| **Transition Module** | Target RTLA module or state-machine transition triggered after the phrase is delivered. |
| **Reviewer Notes** | Clinician comments, validation notes, or review status. |
| **Version** | Semantic version identifier for phrase revision tracking (e.g., `1.0.0`). |

### Design Principles

Every phrase record should satisfy the following requirements:

- **Clinically traceable** through documented evidence and therapeutic intent.
- **Machine-readable** for deterministic state-machine routing.
- **Auditable** through versioning, reviewer notes, and source attribution.
- **Safety-classified** to support automated filtering and human escalation.
- **Population-aware** to ensure appropriate use across supported user groups.
- **Maintainable** through explicit transition paths and structured metadata.