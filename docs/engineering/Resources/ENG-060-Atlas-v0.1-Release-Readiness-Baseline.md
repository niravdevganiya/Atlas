ENG-060 — Atlas v0.1 Release Readiness Baseline
Document ID: ENG-060
Title: Atlas v0.1 Release Readiness Baseline
Version: 0.1.0
Status: Proposed
Phase: Phase 14 — Release
Previous: ENG-059 — Atlas v0.1 Architecture Documentation Baseline
Depends On: ENG-001 through ENG-059
Type: Release-readiness engineering task
Proposed Path: docs/Engineering/Resources/ENG-060-Atlas-v0.1-Release-Readiness-Baseline.md
1. Purpose
ENG-060 establishes the final release-readiness baseline for Atlas v0.1.0.
The objective is to verify that the Atlas v0.1 foundation implemented through ENG-059 is:
- architecturally consistent;
- functionally complete within the approved v0.1 scope;
- fully regression-tested;
- documented;
- repository-clean;
- version-consistent;
- free of known release-blocking defects;
- suitable for release as Atlas v0.1.0.
ENG-060 does not introduce a new Atlas capability.
It is the final engineering gate between the completed v0.1 development/documentation work and the v0.1 release.
2. Release Position
Atlas v0.1 is the foundational engineering representation built around:
Resource
    ↓
Registry
    ↓
Relationships
    ↓
Semantics
    ↓
Constraints / Validation
    ↓
Spatial State
    ↓
Lifecycle
    ↓
Application
    ↓
Agents
    ↓
UI / AI
The release candidate must preserve this architecture without introducing parallel foundational systems.
The release represents the validated v0.1 foundation, not the complete future Atlas product.
3. Release Scope
ENG-060 covers the capabilities established through:
ENG-001 → ENG-051
    Core Atlas foundation

ENG-052
    Resource Create

ENG-053
    Resource Move

ENG-054
    Resource Rotate

ENG-055
    Resource Scale

ENG-056
    Resource Delete

ENG-057
    Resource Duplicate

ENG-058
    Atlas Core Validation Baseline

ENG-059
    Atlas v0.1 Architecture Documentation Baseline
The release scope is therefore the complete validated Atlas v0.1 foundation established by these engineering specifications.
No additional capability is implicitly added by ENG-060.
4. Release Candidate Definition
An Atlas v0.1 release candidate is considered valid only when:
Architecture
      +
Implemented Scope
      +
Validation
      +
Regression
      +
Documentation
      +
Repository Integrity
      +
Version Integrity
      ↓
Release Candidate
A release candidate must represent the same architecture documented in ENG-059 and validated through ENG-058.
5. Architectural Release Invariants
The following are non-negotiable release invariants.
5.1 Single canonical Resource model
AtlasResource remains the single canonical engineering Resource model.
No parallel Resource representation may become authoritative.
5.2 Single canonical Registry
AtlasResourceRegistry remains the canonical Resource Registry.
No parallel authoritative Resource collection may exist.
5.3 AtlasID identity
AtlasID remains the canonical engineering identity of a Resource.
Identity must not be replaced by:
- Python object identity;
- SceneNode identity;
- UI identity;
- renderer identity;
- selection identity;
- agent identity.
5.4 Project ownership
AtlasProject remains the canonical owner of project-scoped Atlas state.
5.5 Canonical relationships
AtlasResourceGraph remains the canonical relationship representation.
5.6 Canonical spatial state
Position, Rotation, and Scale remain represented through the canonical project-scoped Spatial State architecture.
5.7 Canonical validation
AtlasValidationEngine remains the established validation architecture.
No second validation engine may be introduced.
5.8 UI / Scene boundary
UI and Scene systems remain presentation/workspace mechanisms.
They are not canonical engineering state.
5.9 Agent / AI boundary
Agents and AI remain consumers/operators around the canonical Atlas model.
They do not become canonical engineering state.
5.10 Additive architecture
The v0.1 release must not contain architectural changes that undermine additive future evolution.
6. Capability Completeness
ENG-060 must verify that all approved v0.1 Resource editing capabilities are present and regression-safe.
Capability	Engineering Specification	Release Status
Resource Create	ENG-052	Required
Resource Move	ENG-053	Required
Resource Rotate	ENG-054	Required
Resource Scale	ENG-055	Required
Resource Delete	ENG-056	Required
Resource Duplicate	ENG-057	Required
Core Validation	ENG-058	Required
Architecture Documentation	ENG-059	Required


No capability listed above may be silently removed, weakened, or replaced before release.
7. Resource Editing Release Contracts
The following contracts must remain valid.
7.1 Create
Create must:
- create a canonical Resource;
- assign a new AtlasID;
- register the Resource;
- preserve Project ownership;
- establish valid lifecycle state;
- preserve canonical state integrity.
7.2 Move
Move must:
- modify canonical Position;
- preserve AtlasID;
- preserve Resource semantic state;
- preserve relationships;
- preserve unrelated Resources;
- avoid UI-owned spatial state.
7.3 Rotate
Rotate must:
- modify canonical Rotation;
- preserve AtlasID;
- preserve Resource state;
- preserve relationships;
- preserve unrelated Resources.
7.4 Scale
Scale must:
- modify canonical Scale;
- preserve AtlasID;
- preserve Resource identity;
- reject invalid scale values according to the established contract;
- preserve relationships and unrelated state.
7.5 Delete
Delete must:
- remove the canonical Resource;
- remove its canonical spatial state;
- remove relationships involving the Resource according to the established contract;
- preserve unrelated Resources;
- preserve atomic invalid-operation behavior.
ENG-060 must not introduce tombstones, history, undo/redo, or transaction infrastructure.
7.6 Duplicate
Duplicate must:
- create a new canonical Resource;
- assign a new AtlasID;
- preserve the established copied Resource state;
- deep-copy mutable state where required;
- preserve independent spatial state;
- establish the correct lifecycle state;
- not clone relationships;
- preserve source Resource state;
- preserve unrelated Resource state.
Repeated duplication must continue to produce distinct Resources.
8. Validation Baseline
ENG-058 established the core validation baseline.
The known validation evidence is:
ENG-058 focused validation
5 passed
0 failed

Core cross-capability validation
494 passed
0 failed

Agent / AI boundary
284 passed
0 failed

Semantics / Classification / Constraints
241 passed
0 failed

UI / Application boundary
512 passed
0 failed
Combined targeted validation:
1,536 passed
0 failed
These results form the established v0.1 validation evidence.
ENG-060 must verify the final release candidate against the current repository state rather than assuming historical test results remain sufficient.
9. Final Regression
A final release regression must be executed against the release candidate.
The regression must cover:
- core Resource behavior;
- Registry;
- relationships;
- semantics;
- classification;
- constraints;
- lifecycle;
- spatial state;
- validation;
- application boundary;
- agents;
- AI boundaries;
- UI architecture;
- Resource editing operations.
The final regression must produce:
Passed:   > 0
Failed:   0
The exact final count must be recorded from actual test output.
ENG-060 must never fabricate or estimate test results.
10. Regression Warning Policy
Existing known Python 3.14 / pytest-asyncio deprecation warnings do not automatically constitute release blockers.
Known warning classes include:
asyncio.iscoroutinefunction
asyncio.get_event_loop_policy
Warnings must be distinguished from:
- test failures;
- exceptions;
- broken assertions;
- architectural violations;
- release-blocking dependency failures.
ENG-060 must record material release-relevant warnings but must not turn unrelated dependency modernization into an unplanned v0.1 redesign.
11. Architecture Consistency Verification
The final release candidate must be checked against ENG-059.
The verification must confirm:
- implementation agrees with documented architecture;
- canonical ownership remains unchanged;
- no duplicate foundational systems exist;
- application boundaries remain intact;
- UI remains non-canonical;
- agents remain non-canonical;
- validation remains observational;
- spatial state remains separate;
- Resource identity remains AtlasID-based.
Any contradiction between implementation and ENG-059 must be classified before release.
Possible classifications:
Documentation defect
Implementation defect
Test defect
Specification defect
Release blocker
No contradiction may be silently ignored.
12. Repository Integrity
The release candidate must be inspected for repository integrity.
Verification includes:
git status
git diff
git diff --stat
The repository must not contain:
- unintended source modifications;
- temporary debug files;
- generated artifacts accidentally committed;
- abandoned experiments;
- test output files;
- local environment files;
- credentials or secrets;
- duplicate architecture artifacts.
The final release state must be reproducible from the repository.
13. Documentation Integrity
ENG-059 is the authoritative v0.1 architecture documentation baseline.
ENG-060 must verify that:
- ENG-059 is present;
- ENG-059 is marked complete;
- the document reflects the validated architecture;
- no competing architecture document is presented as authoritative;
- required engineering specifications are present;
- release documentation does not contradict ENG-059.
Documentation is part of the release baseline.
14. Version Integrity
The release candidate must consistently identify:
Atlas v0.1.0
Version information must be checked across established project metadata and release-relevant documentation.
ENG-060 must not invent a new versioning mechanism.
If version metadata is already established by the repository, that mechanism remains authoritative.
15. Release Metadata
The release candidate must have a clear release identity containing at minimum:
Product: Atlas
Version: 0.1.0
Release scope: Atlas v0.1 foundation
Phase: Phase 14 — Release
Additional release metadata may be recorded if already supported by the repository.
No unnecessary release infrastructure should be introduced solely for ENG-060.
16. Release Blockers
The following are release blockers:
Architecture blockers
- duplicate canonical Resource model;
- duplicate Registry;
- duplicate Relationship Graph;
- duplicate Spatial State system;
- duplicate Validation Engine;
- broken AtlasID identity;
- Project no longer owning canonical state;
- UI becoming canonical;
- Agent/AI becoming canonical.
Functional blockers
- any approved v0.1 capability failing;
- Resource identity corruption;
- registry corruption;
- relationship corruption;
- spatial-state corruption;
- lifecycle corruption;
- validation contract failure;
- non-atomic invalid operation behavior.
Repository blockers
- uncommitted unintended production changes;
- missing required release files;
- accidental debug artifacts;
- secrets or credentials;
- unreproducible release state.
Documentation blockers
- ENG-059 contradicts implementation;
- release scope cannot be determined;
- required architecture documentation is missing.
17. Non-Blocking Issues
The following do not automatically block v0.1:
- known deprecation warnings;
- future-domain features not yet implemented;
- future UI improvements;
- future rendering improvements;
- future AI improvements;
- future persistence improvements;
- future collaboration;
- future provenance/history;
- future transaction systems;
- future web deployment;
- future integrations.
These belong to future engineering specifications unless they directly violate an existing v0.1 contract.
18. Release Scope Freeze
Once ENG-060 enters final verification, the v0.1 engineering scope is considered frozen.
New feature requests must not be added to the release candidate merely because they are desirable.
Examples:
"Add another Resource editing capability"
"Build the production UI"
"Add persistence"
"Add collaboration"
"Add provenance"
"Add history"
"Add AI automation"
These are future engineering work unless they are required to correct a release blocker against an already-approved v0.1 contract.
The purpose of the freeze is to protect the validated foundation from scope expansion.
19. Release Candidate Verification Matrix
Area	Verification
Resource model	Canonical and intact
AtlasID	Stable engineering identity
Project	Canonical state owner
Registry	Single canonical registry
Relationships	Single canonical graph
Semantics	Existing semantic architecture intact
Constraints	Existing constraint architecture intact
Validation	Single canonical validation architecture
Spatial State	Separate and project-scoped
Lifecycle	Create/Edit/Delete/Duplicate contracts intact
Application	Established command boundary intact
Agents	Non-canonical
AI	Non-canonical
UI	Non-canonical
Tests	Final regression GREEN
Documentation	ENG-059 authoritative
Repository	Clean and reproducible
Version	v0.1.0 consistent
Scope	Frozen
Release blockers	None


20. Release Verification Procedure
The final procedure is:
1. Confirm ENG-001 → ENG-059 completion state
        ↓
2. Inspect repository status
        ↓
3. Verify version metadata
        ↓
4. Verify ENG-059 documentation
        ↓
5. Run final focused release validation
        ↓
6. Run full Atlas regression
        ↓
7. Inspect final repository diff/status
        ↓
8. Review failures/warnings
        ↓
9. Evaluate release blockers
        ↓
10. Declare Release Candidate GREEN
Every verification result must be based on actual repository output.
21. Release Decision
ENG-060 has three possible outcomes.
GREEN — Release Ready
All release criteria pass.
Release Candidate
      ↓
GREEN
      ↓
Atlas v0.1.0 Release
RED — Release Blocked
One or more release-blocking defects exist.
The defect must receive a new narrowly scoped engineering correction before release.
No unrelated feature work may be added.
HOLD — Evidence Incomplete
The architecture may be sound, but required release evidence is missing.
The missing evidence must be obtained before release.
22. Release Artifact
The final release artifact must identify:
Atlas v0.1.0
and reference:
- validated v0.1 architecture;
- completed Resource editing capabilities;
- ENG-058 validation baseline;
- ENG-059 architecture documentation;
- final ENG-060 release verification.
The release artifact must not claim capabilities outside the approved v0.1 scope.
23. Release Statement
When ENG-060 is GREEN, the release statement is:
Atlas v0.1.0 represents the completed and validated foundational Atlas engineering architecture established through ENG-001 through ENG-060. The release provides a canonical Resource-based engineering representation with Registry, Relationships, Semantics, Constraints, Validation, Spatial State, Lifecycle, Application, Agent, and UI boundaries.

The statement must not imply that Atlas v0.1 is the final product or that future domain capabilities already exist.
24. Future Evolution After v0.1
Release of v0.1 does not freeze Atlas permanently.
It freezes the v0.1 foundation.
Future versions may extend Atlas with:
- additional engineering domains;
- richer Resource semantics;
- additional relationships;
- domain-specific constraints;
- richer spatial representations;
- persistence;
- provenance;
- history;
- collaboration;
- advanced agents;
- AI capabilities;
- richer UI;
- rendering;
- external integrations.
Each future capability must preserve the canonical foundation established by v0.1.
The governing principle remains:
Extend Atlas
    ≠
Replace Atlas
25. Non-Goals
ENG-060 does not implement:
- new Resource capabilities;
- new Resource models;
- new Registries;
- new Relationship systems;
- new Spatial State systems;
- new Validation Engines;
- new transaction systems;
- new provenance systems;
- new history systems;
- production web deployment;
- production UI;
- renderer redesign;
- AI architecture redesign;
- agent architecture redesign;
- persistence redesign;
- collaboration;
- new engineering domains.
ENG-060 is a release gate, not another development phase.
26. Completion Criteria
ENG-060 is complete only when:
- ENG-001 through ENG-059 release scope is accounted for.
- Atlas v0.1 architecture remains intact.
- All approved v0.1 capabilities remain present.
- Final validation passes.
- Final regression passes.
- No release-blocking defects remain.
- ENG-059 documentation is authoritative and consistent.
- Version identity is verified as 0.1.0.
- Repository integrity is verified.
- Release scope is frozen.
- Final release evidence is recorded.
- Release candidate is declared GREEN.
- v0.1.0 release checkpoint is created.
27. Completion Sequence
The final sequence is:
ENG-060 Specification
        ↓
Release Candidate Verification
        ↓
Final Validation
        ↓
Final Regression
        ↓
Repository Verification
        ↓
Documentation Verification
        ↓
Version Verification
        ↓
Release Blocker Review
        ↓
Release Candidate GREEN
        ↓
v0.1.0 Release
        ↓
Checkpoint
        ↓
ENG-060 COMPLETE
28. Final Release Principle
Atlas v0.1 must be released because its foundation is proven, not because every future capability has been implemented.
The release criterion is therefore:
The canonical Atlas foundation is implemented, internally consistent, validated, documented, reproducible, and free of release-blocking defects within the approved v0.1 scope.

Future capability is not a prerequisite for v0.1 release.
29. Deliverable
Authoritative specification:
docs/Engineering/Resources/ENG-060-Atlas-v0.1-Release-Readiness-Baseline.md
Document type: Release-readiness engineering specification
Version: 0.1.0
Phase: Phase 14 — Release
Engineering capability introduced: None
Purpose: Establish the final release gate for Atlas v0.1.0.
ENG-060 starting state
ENG-058  Core Validation       COMPLETE ✅
ENG-059  Architecture Docs    COMPLETE ✅
──────────────────────────────────────────
ENG-060  Release Readiness    PROPOSED  ← CURRENT
This is the last engineering specification before the v0.1 release decision.