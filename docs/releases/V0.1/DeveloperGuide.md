# Atlas v0.1 Developer Guide

**Version:** 0.1.0  
**Status:** Release Documentation Draft  
**Audience:** Developers, maintainers, AI coding agents, and integrators  
**Scope:** Atlas v0.1 implementation only

---

## 1. Purpose

This guide explains the Atlas v0.1 implementation as it exists in the repository.

It is intentionally implementation-derived. The guide describes established Atlas behavior, ownership boundaries, public concepts, and verified capabilities. It does not present future architecture as implemented functionality.

The primary engineering rule is:

> The repository implementation and its verified tests define what Atlas v0.1 actually does.

Engineering specifications explain the intended contracts, while implementation and tests establish the behavior that exists in the release baseline.

---

## 2. Atlas v0.1 at a Glance

Atlas v0.1 establishes a canonical engineering model centered on Resources and their relationships.

The core conceptual chain is:

```text
AtlasID
   ↓
AtlasResource
   ↓
AtlasProject
   ├── Resource Registry
   ├── Relationship Graph
   ├── Classification Registry
   └── Spatial State Registry
   ↓
Semantics / Classification
   ↓
Constraints / Validation
   ↓
Application Boundary
   ↓
Agents / AI and UI / Workspace boundaries
```

The important architectural property is not the diagram itself but ownership:

- Resources are canonical engineering entities.
- The Project owns project-level canonical state.
- The Registry owns Resource registration and lookup.
- The Graph represents explicit Resource relationships.
- Spatial state is kept separately from Resource identity.
- Validation observes canonical state.
- Application/UI/Agent layers operate around the canonical model rather than replacing it.

---

## 3. Repository Organization

The Atlas repository separates engineering specifications from release documentation.

Relevant locations are:

```text
docs/
├── Engineering/
│   └── Resources/
│       ├── ENG-001-...
│       ├── ...
│       └── ENG-060-...
│
└── Releases/
    └── V0.1/
        ├── master_plan.md
        ├── product_spec.md
        └── DeveloperGuide.md
```

The implemented Python package and tests are maintained under the Atlas package source/test tree:

```text
packages/atlas/
├── src/atlas/
└── tests/
```

The exact repository structure should be treated as authoritative when navigating the current checkout.

---

## 4. Source-of-Truth Hierarchy

When implementation and documentation are compared, use this order of authority:

1. Executable implementation.
2. Automated tests.
3. Completed engineering specifications.
4. ENG-059 architecture documentation.
5. ENG-060 release verification evidence.
6. Earlier conceptual/product documents.

A document must not claim that a capability exists merely because an earlier roadmap or specification proposed it.

If an implementation is absent, the capability is not part of the verified v0.1 API.

---

# 5. Core Architecture

## 5.1 Canonical Resource Model

`AtlasResource` is the base engineering entity used throughout Atlas.

The Resource model established in v0.1 includes canonical identity and engineering information such as:

- AtlasID
- classification
- name
- properties
- metadata
- semantic tags
- categories
- lifecycle state
- relationships through the established relationship model

Spatial transformation is not treated as Resource identity.

The v0.1 architecture therefore keeps Resource identity and spatial state as separate concerns.

---

## 5.2 AtlasID

`AtlasID` is the canonical engineering identity used to identify Atlas entities.

A Resource's AtlasID is not equivalent to:

- a UI widget ID,
- a scene-node ID,
- a selection identifier,
- a renderer object ID,
- or an AI-generated identifier.

Engineering operations use canonical Atlas identity.

This allows presentation and integration layers to change without changing the identity of the underlying engineering Resource.

---

## 5.3 AtlasProject

`AtlasProject` is the top-level project context.

The Project owns the canonical project-scoped structures required by v0.1.

These include:

```text
AtlasProject
├── Project identity
├── Project name
├── Project metadata
├── Classification Registry
├── Resource Registry
├── Relationship Graph
└── Spatial State Registry
```

The Project is the appropriate boundary for coordinated Resource operations.

A UI component, Agent, Scene, or renderer must not become a second Project container.

---

# 6. Resource Registry

## 6.1 Purpose

`AtlasResourceRegistry` is the canonical collection and lookup mechanism for project Resources.

Resources are indexed by their immutable AtlasID.

The Registry is responsible for Resource registration and lookup concerns.

It is not responsible for:

- UI presentation,
- rendering,
- validation-rule ownership,
- agent reasoning,
- or business workflows.

---

## 6.2 Registry Ownership

The Project owns the Resource Registry.

Conceptually:

```text
AtlasProject
      ↓
AtlasResourceRegistry
      ↓
AtlasResource
```

The Relationship Graph does not become a second Resource owner.

The UI does not maintain another Resource collection.

Agents do not maintain another Resource collection.

---

## 6.3 Registry Integrity

The verified v0.1 Registry boundary rejects invalid Resource objects rather than allowing arbitrary objects to reach AtlasID access.

Registry operations preserve canonical Resource identity and collection integrity.

Invalid registration must not silently create or partially register a Resource.

---

# 7. Relationships and Resource Graph

## 7.1 Canonical Relationship Model

Atlas represents Resource relationships explicitly.

The canonical relationship graph is project-scoped.

Conceptually:

```text
AtlasProject
      │
      ├── Resource Registry
      │       └── Resources
      │
      └── Resource Graph
              └── Relationships
```

The Graph manages relationships between Resources but does not replace the Registry as the Resource owner.

---

## 7.2 Relationship Integrity

A relationship must reference Resources that belong to the Graph's associated Resource Registry.

The verified validation boundary rejects invalid relationship objects and invalid Resource lookup objects with explicit type errors.

Relationship insertion must not silently create missing Resources.

Duplicate relationships are rejected according to the established Graph contract.

---

## 7.3 Graph Queries

The implemented Graph supports Resource-oriented relationship lookup and the established graph navigation/query capabilities from the earlier relationship milestones.

Developers should use the canonical Graph API rather than maintaining a second adjacency structure elsewhere.

---

# 8. Semantics and Classification

## 8.1 Classification

Atlas Resources have a classification.

Classifications are project-managed semantic definitions.

Classification is part of the Resource's canonical semantic identity/context, but the Classification Registry remains separate from the Resource Registry.

---

## 8.2 Semantic Tags

Semantic tags are part of the established Resource semantic model.

They provide semantic descriptors without replacing Resource identity or classification.

Tags are not a separate Resource identity system.

---

## 8.3 Categories

Categories are part of the established v0.1 semantic organization.

Categories provide another semantic organization mechanism while remaining separate from the canonical Resource identity.

---

## 8.4 Semantic Ownership

Semantic information remains associated with canonical Resources and project semantic structures.

The semantic layer must not create a competing Resource representation.

---

# 9. Properties and Constraints

## 9.1 Resource Properties

Atlas Resources support engineering properties.

The established property model includes fields such as:

- property ID
- name
- value
- data type
- unit
- description

Properties describe characteristics of a Resource.

They are distinct from:

- AtlasID,
- classification,
- relationship identity,
- and UI presentation state.

---

## 9.2 Constraints

Atlas v0.1 includes the established property-constraint architecture.

Constraints are evaluated through the canonical constraint/validation architecture.

Developers must not introduce a second constraint engine for a new feature.

If a future domain requires new constraint types, they should extend the established architecture rather than bypass it.

---

# 10. Validation

## 10.1 Canonical Validation Engine

Atlas uses the established `AtlasValidationEngine`.

The validation architecture includes:

```text
AtlasValidationEngine
AtlasValidationRule
AtlasValidationResult
AtlasValidationCategory
AtlasValidationSeverity
```

Validation rules are registered with the Validation Engine.

Validation evaluates a Resource and produces validation results.

---

## 10.2 Validation Is Observational

Validation does not mutate the canonical Resource.

The ENG-058 validation baseline explicitly verifies that validation preserves:

- AtlasID,
- name,
- classification,
- properties,
- tags,
- categories,
- lifecycle state.

Therefore developers must not use validation as an implicit mutation mechanism.

---

## 10.3 Validation Boundary

The canonical Validation Engine rejects objects that are not `AtlasResource`.

A second `validate()` implementation on `AtlasResource` must not be introduced as an alternative validation engine.

---

# 11. Spatial State

## 11.1 Separation from Resource Identity

Atlas v0.1 keeps spatial transformation state separate from the canonical Resource model.

The Project owns a spatial state registry.

Conceptually:

```text
AtlasID
   ↓
AtlasSpatialStateRegistry
   ├── Position
   ├── Rotation
   └── Scale
```

This allows Resource identity and spatial state to evolve independently.

---

## 11.2 Position

Resource Move operates through the canonical spatial state boundary.

The Move operation targets a Resource using AtlasID and updates its position state.

The operation does not create another Resource.

---

## 11.3 Rotation

Resource Rotate operates through canonical spatial state.

Rotation is represented independently of Resource identity.

---

## 11.4 Scale

Resource Scale operates through canonical spatial state.

Scale is represented independently of Resource identity.

The implemented command contract validates the expected `x`, `y`, and `z` scale components before mutation.

---

## 11.5 Spatial State Ownership

Spatial state belongs to the Project's canonical spatial state system.

It is not owned by:

- a SceneNode,
- a renderer object,
- a UI selection,
- a gizmo,
- or an AI agent.

---

# 12. Resource Lifecycle

The Resource lifecycle is established through the lifecycle model and the Resource operations implemented in v0.1.

The lifecycle must remain distinct from:

- UI lifecycle,
- Panel lifecycle,
- Scene lifecycle,
- Agent lifecycle,
- and renderer lifecycle.

Resource lifecycle state belongs to the Resource domain.

---

# 13. Resource Editing

Atlas v0.1 includes the Phase 11 Resource Editing capabilities.

```text
Create
Move
Rotate
Scale
Delete
Duplicate
```

Each operation uses the canonical Atlas application/domain architecture.

---

## 13.1 Create

Resource creation is exposed through the Application Command boundary.

The established command identity is:

```text
create_resource
```

The command accepts the implemented creation payload, including a classification and optional name.

Creation produces an `AtlasResource` and registers it in the canonical Resource Registry.

Creation also establishes the Resource's canonical spatial state entries used by later Move/Rotate/Scale operations.

---

## 13.2 Move

Resource Move is exposed through:

```text
move_resource
```

The command identifies the Resource by `AtlasID` and carries a position containing:

```text
x
y
z
```

Invalid Resource identities, invalid position containers, missing position components, non-numeric values, and non-finite numeric values are rejected by the established command contract.

The mutation is validated before canonical spatial state is changed.

Move does not:

- create a second Resource,
- replace the Resource object,
- change Resource identity,
- mutate unrelated Resource state,
- or require renderer/AI dependencies.

---

## 13.3 Rotate

Resource Rotate is exposed through:

```text
rotate_resource
```

Rotation is represented as `x`, `y`, and `z` spatial state.

Validation is completed before the spatial state mutation.

---

## 13.4 Scale

Resource Scale is exposed through:

```text
scale_resource
```

Scale is represented as `x`, `y`, and `z`.

The established application implementation validates the Resource identity and scale mapping before updating canonical spatial state.

---

## 13.5 Delete

Resource Delete is exposed through:

```text
delete_resource
```

Deletion operates on the canonical Resource identified by AtlasID.

Deletion must not accidentally delete unrelated Resources.

The established lifecycle/relationship contracts ensure that Resource removal preserves project integrity.

---

## 13.6 Duplicate

Resource Duplicate is exposed through the established duplication command/application contract.

Duplication creates a distinct Resource identity while preserving the established duplication semantics.

A duplicated Resource is not a second representation of the same engineering identity.

---

# 14. Application Boundary

## 14.1 Purpose

`AtlasApplication` is the thin application boundary between callers and the canonical Atlas domain model.

Conceptually:

```text
User / UI / Agent
        ↓
AtlasCommand
        ↓
AtlasApplication
        ↓
AtlasProject
        ↓
Canonical Atlas State
```

Commands express intent.

The Application coordinates execution.

The canonical domain remains responsible for canonical state and integrity.

---

## 14.2 Commands

`AtlasCommand` represents an application-level request.

Implemented v0.1 command names include the Resource editing commands established by ENG-052 through ENG-057.

The command layer must not become a second domain model.

---

## 14.3 Queries

The Application boundary also provides the established query surface for presentation/application consumers.

Queries should read canonical state rather than create a parallel engineering model.

---

## 14.4 Application Ownership Rule

`AtlasApplication` does not replace `AtlasProject`.

The Project remains the canonical owner of project state.

---

# 15. Agents and AI Boundary

Atlas v0.1 includes the established Agent Runtime and specialized agent architecture.

The implemented agent layer includes the runtime/orchestration structure and specialized agents established through the Phase 7 milestones.

The architecture includes:

```text
Orchestrator
     ↓
Agent Runtime
     ↓
Specialized Agents
├── Resource Agent
├── Registry Agent
├── Semantic Agent
├── Relationship Agent
└── Validation Agent
```

Agents operate on top of the deterministic Atlas foundation.

They do not create competing Resource, Registry, Graph, Semantic, or Validation systems.

---

## 15.1 Agent Responsibilities

Specialized agents coordinate with the canonical Atlas architecture.

Examples of established responsibility boundaries include:

- Resource Agent → Resource-domain operations
- Registry Agent → Resource discovery/query responsibilities
- Semantic Agent → semantic operations
- Relationship Agent → relationship operations
- Validation Agent → validation operations

The actual implementation remains authoritative for exact APIs and behavior.

---

## 15.2 AI Reasoning

Atlas v0.1 establishes Agent/AI boundaries but does not claim an autonomous general-purpose AI reasoning product.

Future LLM-powered planning, autonomous reasoning, or domain-specific AI behavior must not be documented as a guaranteed v0.1 capability unless it exists in the implementation and verified tests.

---

# 16. UI and Application Presentation

Atlas v0.1 includes the application-layer UI architecture and the verified presentation contracts developed through Phase 9 and Phase 10.

The application/presentation layer includes capabilities such as:

- Workspace
- Dashboard
- Explorer
- Inspector
- Toolbar
- Panels
- Scene
- Camera
- Navigation
- Selection
- Gizmo
- Basic Editing

These are application/presentation capabilities.

They do not replace the canonical Atlas model.

---

## 16.1 Workspace

`AtlasWorkspace` hosts presentation structures such as Panels, Views, Scene, and selection context.

Workspace state is not Resource state.

The Workspace stores Resource selection by AtlasID rather than becoming the owner of Resource objects.

---

## 16.2 Dashboard

The Dashboard is a project-level presentation surface.

It consumes canonical project information and produces presentation summaries.

The Dashboard does not own:

- a Resource Registry,
- a Relationship Graph,
- persistence,
- exchange,
- or AI-generated engineering truth.

---

## 16.3 Explorer

The Explorer provides project/resource navigation.

Its presentation state remains separate from the canonical Project.

It does not become a Project container.

---

## 16.4 Inspector

The Inspector is read-oriented presentation infrastructure.

It can inspect Resource information without owning or mutating the canonical Resource model.

The verified Inspector tests explicitly protect its read-only behavior and prevent it from owning a second Resource Registry or Graph.

---

## 16.5 Toolbar

The Toolbar provides presentation-level access to Application Commands.

It delegates to the existing command/application boundary rather than introducing another command system.

---

## 16.6 Panels

Panels are reusable presentation containers.

Panel lifecycle and Panel Registry state are separate from Resource lifecycle and Resource Registry state.

---

# 17. 3D Workspace Boundary

The v0.1 3D workspace architecture separates presentation state from canonical engineering state.

The conceptual separation is:

```text
Canonical Engineering Model
        ↓
AtlasProject / AtlasResource / AtlasRelationship

Application Behavior
        ↓
AtlasApplication

Workspace
        ↓
AtlasWorkspace

3D Presentation
        ↓
AtlasScene / AtlasSceneNode
```

A SceneNode is not an AtlasResource.

Scene state must not become a competing engineering model.

---

## 17.1 Scene

The Atlas Scene provides a deterministic presentation structure for the 3D workspace.

It does not own canonical engineering Resources.

---

## 17.2 Camera and Navigation

Camera and navigation are workspace/presentation concerns.

They do not mutate engineering truth merely because the viewport changes.

---

## 17.3 Selection

Selection uses AtlasID to identify the selected engineering Resource while keeping selection itself as UI/workspace state.

Selection does not transfer Resource ownership to the UI.

---

## 17.4 Gizmo

The Gizmo is presentation/workspace infrastructure.

It does not own Resources, the Project, the Graph, or the Registry.

Renderer-specific technologies are outside the canonical Atlas core.

---

# 18. Persistence

Atlas v0.1 includes the established JSON serialization and Project Save/Load capabilities.

The persistence architecture is intentionally separate from the canonical domain model.

Conceptually:

```text
AtlasProject
    ↓
AtlasJSONSerializer
    ↓
JSON representation
    ↓
File persistence
```

Serialization reads the canonical model.

It does not become a second canonical model.

---

## 18.1 JSON Serialization

ENG-036 established the Atlas JSON serialization baseline.

Verified serialization behavior includes preservation of important project structures such as:

- project identity,
- metadata,
- classifications,
- classification hierarchy,
- Resources,
- Resource identity,
- properties,
- semantic information,
- lifecycle,
- and relationships.

Relationship endpoints are represented by stable Resource identity rather than recursively embedding duplicate Resources.

---

## 18.2 Save / Load

ENG-037 provides the Project file boundary over the serializer.

Save/Load is Atlas-native persistence.

It must not duplicate serialization logic.

---

# 19. Import / Export Boundary

ENG-038 establishes a generic Import/Export boundary.

The v0.1 architecture separates:

```text
External Representation
        ↓
Importer
        ↓
Atlas Canonical Model
```

and:

```text
Atlas Canonical Model
        ↓
Exporter
        ↓
External Representation
```

The canonical Atlas model remains authoritative.

---

## 19.1 What v0.1 Does Not Implement Here

ENG-038 explicitly does not establish concrete adapters for:

- IFC
- BIM
- Revit
- CAD
- DWG
- DXF
- PDF
- Excel
- CSV
- GIS
- remote APIs
- synchronization
- provenance
- revision history
- change-impact analysis

These are outside the verified v0.1 generic exchange capability.

---

# 20. Testing Atlas

Atlas development follows a strict engineering workflow:

```text
Specification
    ↓
RED Test
    ↓
Smallest Correct Implementation
    ↓
GREEN
    ↓
Phase Regression
    ↓
Full Regression
    ↓
Checkpoint
```

Tests are part of the engineering contract.

A developer should not weaken a test merely to accommodate an implementation.

If implementation and intended architecture disagree, the contract must be reviewed first.

---

# 21. v0.1 Verification Baseline

The final ENG-060 release verification produced:

```text
Targeted verification:  1,536 passed
Full regression:        1,930 passed
Failures:               0
Version:                0.1.0
Repository:             clean
Release readiness:      GREEN
```

The targeted verification covered:

```text
Core / Resource / Graph / Lifecycle / Validation / UI
    494 passed

Agent / AI boundary
    284 passed

Semantics / Classification / Constraints
    241 passed

UI / Application boundary
    512 passed

ENG-058 core validation
    5 passed
```

Total:

```text
1,536 passed
0 failed
```

Full regression:

```text
1,930 passed
0 failed
```

Known Python 3.14 / pytest-asyncio deprecation warnings were present and did not produce test failures.

---

# 22. Extending Atlas Safely

New Atlas functionality should extend the established architecture.

## 22.1 Safe Extension

A future capability may introduce:

- new Resource classifications,
- new semantic concepts,
- new constraint/validation rules,
- new application commands,
- new agents,
- new UI surfaces,
- new integrations,
- new domain-specific capabilities.

The new capability should use existing canonical structures wherever appropriate.

---

## 22.2 Forbidden Parallel Foundations

Do not introduce:

- a second Resource model,
- a second Resource Registry,
- a second Relationship Graph,
- a second Spatial State system,
- a second Validation Engine,
- a second canonical identity,
- UI-owned canonical Resource state,
- Agent-owned canonical Resource state,
- renderer-owned engineering truth,
- or an alternative project state model.

These patterns fragment Atlas and make future domains harder to integrate.

---

# 23. What Is Canonical?

The following are canonical engineering state in v0.1:

```text
AtlasID
AtlasResource
AtlasProject
Resource Registry
Relationship Graph
Classification / Semantic state
Properties
Constraints
Validation definitions/results
Resource lifecycle
Spatial State Registry
```

These systems form the engineering foundation.

---

# 24. What Is Not Canonical?

The following are not canonical engineering identity/state merely because they reference Atlas:

```text
UI selection
Workspace state
Panel state
View state
SceneNode identity
Camera state
Navigation state
Gizmo state
Renderer objects
Agent internal state
AI reasoning state
Temporary presentation models
```

These layers may consume or present canonical information but must not silently replace it.

---

# 25. Determinism and Atomicity

Atlas v0.1 emphasizes deterministic behavior.

Where an operation validates input before mutation, invalid input must not partially change canonical state.

The Resource editing contracts explicitly test:

- invalid input rejection,
- Resource identity preservation,
- state isolation,
- non-creation of duplicate Resources,
- preservation of unrelated Resource state,
- and deterministic behavior.

This is particularly important at the Application boundary.

---

# 26. Error Handling

Developers should expect explicit errors for invalid boundary inputs.

Examples established by the implementation include:

- `TypeError` for invalid object types,
- `ValueError` for invalid values or state,
- `KeyError` where established lookup contracts require missing keys.

The exact exception behavior of a public API is determined by the implementation and its tests.

Do not assume a generic exception contract for APIs that have not been documented or tested.

---

# 27. Working with Atlas as a Developer

A developer adding a capability should first determine:

1. Which canonical state is affected?
2. Who owns that state?
3. Which existing subsystem already owns the responsibility?
4. Which AtlasID identifies the affected Resource?
5. Which Application boundary should expose the operation?
6. Which validation rules apply?
7. Which tests prove the intended behavior?
8. Whether the capability requires a new engineering specification.
9. Whether the feature can be implemented additively.
10. Whether the feature accidentally introduces a parallel canonical system.

The implementation should then follow the established RED → implementation → GREEN → regression workflow.

---

# 28. v0.1 Development Limitations

Atlas v0.1 is a foundation release.

The following should not be inferred from the existence of the foundation:

- autonomous engineering reasoning,
- production BIM interoperability,
- IFC support,
- Revit synchronization,
- CAD synchronization,
- GIS integration,
- document intelligence,
- provenance/history infrastructure,
- collaborative multi-user synchronization,
- cloud infrastructure,
- production renderer integration,
- autonomous AI agents,
- domain-specific building-code engines,
- or a complete end-user product.

Some of these have architectural extension boundaries; that does not mean the concrete capability is implemented in v0.1.

---

# 29. Future Evolution Rule

Future Atlas versions should build on the v0.1 foundation.

A new domain should be able to map into the canonical model:

```text
Resource
   ↓
Registry
   ↓
Relationship
   ↓
Semantics
   ↓
Validation / Constraints
   ↓
Spatial State where applicable
   ↓
Application
   ↓
Agents / AI
   ↓
UI / External Integration
```

without requiring a competing canonical representation.

If a future capability appears to require a second foundational system, that should trigger an architecture review before implementation.

---

# 30. Engineering Specification References

The Developer Guide is derived from the implemented v0.1 engineering sequence, especially:

```text
ENG-001  Atlas Resource
ENG-002  Resource Identity
ENG-003  Resource Classification
ENG-004  Resource Properties
ENG-005  Resource Relationships
ENG-006  Resource Semantics
ENG-007  Resource Lifecycle
ENG-008  Resource Validation
ENG-009  Resource Serialization
ENG-010  Atlas Resource Registry

ENG-025  Resource Categories
ENG-026  Resource Validation Runtime Model
ENG-027  Property Constraints
ENG-028  Agent Runtime
ENG-029  Orchestrator Agent
ENG-030  Resource Agent
ENG-031  Registry Agent
ENG-032  Semantic Agent
ENG-033  Relationship Agent
ENG-034  Validation Agent
ENG-035  Multi-Agent Coordination
ENG-035A Foundation Hardening

ENG-036  Atlas JSON Serialization
ENG-037  Project Save / Load
ENG-038  Import / Export
ENG-039  Atlas UI Architecture
ENG-040  Atlas UI Application Shell
ENG-041  Atlas Dashboard
ENG-042  Atlas Explorer
ENG-043  Atlas Inspector
ENG-044  Atlas Toolbar
ENG-045  Atlas Panels
ENG-046  Atlas Scene
ENG-047  Atlas Camera
ENG-048  Atlas Navigation
ENG-049  Atlas Selection
ENG-050  Atlas Gizmo
ENG-051  Atlas Basic Editing

ENG-052  Resource Create
ENG-053  Resource Move
ENG-054  Resource Rotate
ENG-055  Resource Scale
ENG-056  Resource Delete
ENG-057  Resource Duplicate
ENG-058  Atlas Core Validation Baseline
ENG-059  Atlas v0.1 Architecture Documentation Baseline
ENG-060  Atlas v0.1 Release Readiness Baseline
```

Where an earlier specification is conceptual and later implementation has refined the contract, the completed implementation and tests define the verified v0.1 behavior.

---

# 31. Architecture Documentation Reference

ENG-059 remains the authoritative v0.1 architecture baseline.

The Developer Guide is not a replacement for ENG-059.

The distinction is:

```text
ENG specifications
    → engineering contracts and history

ENG-059
    → authoritative architecture baseline

Developer Guide
    → developer-facing explanation of the implemented v0.1 system

Tests
    → executable behavioral evidence
```

These documents should remain mutually consistent.

---

# 32. Release Verification Reference

ENG-060 established the final technical release-readiness baseline.

The verified evidence is:

```text
1,536 targeted tests passed
1,930 full-regression tests passed
0 failures
Atlas version 0.1.0
ENG-060 specification present
working tree clean
release decision GREEN
```

This evidence verifies the implementation baseline documented by this guide.

It does not imply that future versions will retain the same test count.

---

# 33. Developer Guide Scope Boundary

This document deliberately does not document unsupported capabilities as if they were available.

When a developer needs functionality not described here, they should first inspect:

```text
src/atlas/
tests/
docs/Engineering/Resources/
```

and confirm whether the capability exists.

If it does not exist, it should be treated as future scope and introduced through an appropriate engineering specification.

---

# 34. Final Developer Principle

Atlas v0.1 should be understood as a canonical engineering foundation.

The most important rule for developers is:

> Extend the Atlas model; do not create another Atlas model beside it.

When implementing a new capability:

```text
Find canonical state
        ↓
Find its owner
        ↓
Use the existing boundary
        ↓
Validate before mutation
        ↓
Preserve AtlasID identity
        ↓
Test the architectural invariant
        ↓
Extend additively
```

That discipline is what allows Atlas v0.1 to serve as the foundation for future engineering domains without requiring a competing core architecture.

---

# 35. v0.1 Status

Atlas v0.1 has a verified technical foundation.

The release-readiness baseline recorded:

```text
Atlas v0.1.0
1,536 targeted tests passed
1,930 full regression tests passed
0 failures
GREEN technical release-readiness
```

This Developer Guide documents the implemented foundation and explicitly separates verified behavior from unsupported future capabilities.

**Atlas v0.1 — Developer Guide**
