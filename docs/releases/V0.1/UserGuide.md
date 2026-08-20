# Atlas v0.1 User Guide

**Version:** 0.1.0  
**Status:** Release Documentation Draft  
**Audience:** Atlas users, evaluators, and operators  
**Scope:** Verified Atlas v0.1 behavior only

---

## 1. Purpose

This guide explains how to use the Atlas v0.1 capabilities that are implemented and verified in the repository.

It is written from the implemented Atlas behavior, automated tests, and the engineering specifications through ENG-062.

The guide deliberately does not describe future Atlas capabilities as though they are available in v0.1.

When a capability is not verified as implemented, it is marked **Out of Scope**.

---

# 2. What Is Atlas v0.1?

Atlas v0.1 provides a foundational engineering model for representing Resources and their relationships inside a Project.

At the user level, the important concepts are:

```text
Project
   ↓
Resources
   ├── Classification
   ├── Properties
   ├── Semantic information
   ├── Lifecycle state
   └── Spatial state
          ↓
     Relationships
          ↓
      Validation
```

Atlas v0.1 also provides established application, UI/workspace, persistence, import/export boundaries, agent, and validation capabilities.

The exact behavior of each capability is governed by the implemented system and its tests.

---

# 3. Important Atlas Concepts

## 3.1 Project

A Project is the main container for canonical Atlas state.

A Project owns the structures required to work with its Resources, including:

- Resource Registry
- Relationship Graph
- Classification Registry
- Spatial State Registry

Users should think of a Project as the working context in which Resources and their relationships exist.

---

## 3.2 Resource

A Resource represents an engineering entity in Atlas.

A Resource has canonical identity and information such as:

- AtlasID
- classification
- name
- properties
- tags
- categories
- lifecycle state

A Resource is the primary object users work with.

---

## 3.3 AtlasID

Every Resource has an AtlasID.

AtlasID is the Resource's canonical engineering identity.

Users should not confuse AtlasID with:

- UI selection state,
- a SceneNode,
- a renderer object,
- a panel identifier,
- or an AI/Agent identifier.

When Atlas refers to a Resource, AtlasID is the stable identity used by the engineering model.

---

## 3.4 Classification

A Resource can have a Classification.

Classification provides semantic meaning for the Resource.

For example, the implementation and existing examples use classifications such as:

```text
Wall
```

Classification is not the same thing as the Resource's AtlasID.

---

## 3.5 Properties

Resources can contain engineering properties.

Properties describe characteristics of a Resource.

The established property model supports information including:

- property identity,
- name,
- value,
- data type,
- unit,
- description.

---

## 3.6 Tags and Categories

Resources can also contain semantic tags and categories.

These provide additional organization and semantic information.

They do not replace the Resource's canonical identity.

---

## 3.7 Relationships

Atlas Resources can have explicit relationships with other Resources.

Relationships are part of the canonical Project graph.

A relationship is not merely a visual line drawn by the UI.

---

## 3.8 Spatial State

Atlas keeps Resource spatial state separately from Resource identity.

The spatial state includes:

```text
Position
Rotation
Scale
```

This allows users to move, rotate, and scale Resources without changing their AtlasID.

---

## 3.9 Validation

Atlas can validate Resource state through its canonical validation system.

Validation is observational: validating a Resource does not change the Resource.

If an invalid object is submitted at a validation boundary, the established implementation rejects it rather than silently accepting it.

---

# 4. Understanding the Atlas Application and Workspace Model

Atlas v0.1 includes the established application and framework-independent presentation architecture developed through the UI milestones.

The implemented workspace concepts include:

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

These are implemented Atlas application/presentation capabilities and contracts. They should not be interpreted as a claim that v0.1 provides a complete interactive graphical frontend or renderer.

The workspace is a presentation and interaction layer over the canonical Atlas model.

It does not replace:

- the canonical Resource model,
- the Resource Registry,
- the Relationship Graph,
- the Spatial State Registry,
- or the Validation architecture.

---

# 5. Dashboard

The Dashboard provides a project-level presentation surface.

It is intended to show project information and summaries.

The Dashboard does not become the owner of Resources or relationships.

Users should therefore treat Dashboard information as a view of Project state rather than a separate Project model.

---

# 6. Explorer

The Explorer provides navigation through the Project and its Resources.

It establishes the implemented Resource presentation/navigation flow.

The Explorer does not create a second copy of the Project.

A complete graphical frontend or production navigation experience is not implied by the existence of the Explorer application model.

---

# 7. Inspector

The Inspector provides detailed Resource information.

It is intended for inspecting the selected Resource and its properties/metadata.

The Inspector is a presentation surface and does not become a second Resource Registry or Resource Graph.

When a Resource is selected, the Inspector can present information from the canonical Resource state.

---

# 8. Toolbar

The Toolbar provides an application/presentation entry point for the implemented editing operations.

The Resource editing capabilities established in v0.1 are:

```text
Create
Move
Rotate
Scale
Delete
Duplicate
```

The Toolbar does not own the engineering mutation.

The actual engineering operation is performed through the established Application/Command boundary.

---

# 9. Panels

Panels provide reusable UI containers for the Atlas workspace.

Panel state is UI state.

It should not be confused with:

- Resource lifecycle,
- Resource Registry state,
- Project ownership,
- or canonical engineering state.

---

# 10. Scene

The Scene represents the framework-independent 3D workspace/presentation model.

A SceneNode is not an AtlasResource.

The Scene provides presentation structures without becoming a second engineering model.

The v0.1 Scene architecture is renderer-independent. It does not itself implement:

- a production renderer,
- WebGL/WebGPU/Three.js integration,
- raycasting,
- input event handling,
- persistence,
- exchange,
- or agent execution.

The canonical Atlas model remains authoritative.

---

# 11. Camera

The Camera represents viewport viewing state within the workspace model.

Camera state is presentation state.

Changing camera state does not change a Resource's engineering identity.

A production graphics viewport or renderer is outside the verified v0.1 foundation.

---

# 12. Navigation

Navigation represents workspace navigation state.

Navigation state is separate from Project and Resource state.

Changing navigation state does not itself constitute an engineering modification.

---

# 13. Selection

Selection identifies a Resource for the current workspace/application context.

Selection is based on Atlas identity but is not itself canonical Resource ownership.

Selecting a Resource does not copy or transfer the Resource into the UI.

---

# 14. Gizmo

The Gizmo provides presentation state associated with spatial editing workflows.

In v0.1, the Gizmo does not itself perform:

- SceneNode transformations,
- rendering,
- input event handling,
- raycasting,
- or engineering-state mutation.

Resource Move, Rotate, and Scale operations are implemented through the canonical Resource Editing and Application/Command contracts.

The Gizmo therefore should be understood as workspace/presentation infrastructure rather than a second transformation engine.

---

# 15. Creating a Resource

Atlas v0.1 supports Resource creation.

The conceptual application workflow is:

```text
Invoke the Create Resource application operation
      ↓
Provide the required Resource creation information
      ↓
Specify the Resource classification
      ↓
Optionally provide the Resource name
      ↓
Submit the operation
      ↓
Atlas creates the Resource
      ↓
Resource becomes part of the Project's canonical Resource Registry
```

The exact input fields and command surface are defined by the implemented application layer.

Creation establishes the Resource's canonical identity.

A created Resource is not merely a visual Scene object.

---

# 16. Inspecting a Resource

A typical inspection workflow is:

```text
Identify / select Resource through an available application surface
      ↓
Use the Inspector/application inspection surface
      ↓
Review Resource information
```

Information can include:

- AtlasID
- name
- classification
- properties
- tags
- categories
- lifecycle state

The Inspector presents canonical state; it does not become the owner of that state.

---

# 17. Classifying a Resource

Resources can be associated with a Classification managed by the Project.

The application-level workflow is:

```text
Create or identify Resource
      ↓
Choose an available Classification through the supported application surface
      ↓
Associate the Classification with the Resource
      ↓
Inspect the resulting Resource state
```

The Classification Registry remains distinct from the Resource Registry.

---

# 18. Working With Resource Properties

Properties describe characteristics of a Resource.

A user can inspect the established property information associated with a Resource through the available application/UI surfaces.

Properties are distinct from spatial transformation:

```text
Resource Properties
    ≠
Position / Rotation / Scale
```

Spatial transformation belongs to the canonical Spatial State system.

---

# 19. Moving a Resource

Atlas v0.1 supports Resource Move.

The application-level workflow is:

```text
Identify Resource
      ↓
Invoke the Move Resource application operation
      ↓
Specify position
      ↓
Validate the requested position
      ↓
Update canonical Spatial State
      ↓
Resource remains the same AtlasID
```

The position uses:

```text
x
y
z
```

The established Move command rejects invalid input, including invalid Resource identities and invalid/non-finite position values.

A failed Move must not partially mutate canonical spatial state.

---

# 20. Rotating a Resource

Atlas v0.1 supports Resource Rotate.

The application-level workflow is:

```text
Identify Resource
      ↓
Invoke the Rotate Resource application operation
      ↓
Specify rotation
      ↓
Validate
      ↓
Update canonical Spatial State
```

Rotation uses the established three-component spatial representation.

Rotation changes spatial state, not Resource identity.

---

# 21. Scaling a Resource

Atlas v0.1 supports Resource Scale.

The application-level workflow is:

```text
Identify Resource
      ↓
Invoke the Scale Resource application operation
      ↓
Specify scale
      ↓
Validate
      ↓
Update canonical Spatial State
```

Scale uses:

```text
x
y
z
```

The established command validates the Resource identity and scale mapping before changing canonical spatial state.

---

# 22. Deleting a Resource

Atlas v0.1 supports Resource Delete.

The conceptual application workflow is:

```text
Identify Resource
      ↓
Invoke the Delete Resource application operation
      ↓
Confirm / submit the operation as required by the available application surface
      ↓
Atlas removes the canonical Resource
```

Deletion operates on the canonical Resource identified by AtlasID.

The implementation is designed to preserve project integrity and avoid accidentally deleting unrelated Resources.

---

# 23. Duplicating a Resource

Atlas v0.1 supports Resource Duplicate.

The application-level workflow is:

```text
Identify Resource
      ↓
Invoke the supported Resource Duplicate operation
      ↓
Submit duplication operation
      ↓
Atlas creates a distinct Resource
```

The duplicated Resource has its own canonical identity.

Duplication must not create two UI representations that secretly share one engineering identity.

---

# 24. Working With Relationships

Atlas represents relationships explicitly.

The application-level relationship workflow conceptually follows:

```text
Identify source Resource
      ↓
Identify target Resource
      ↓
Invoke the supported relationship operation
      ↓
Atlas validates the relationship
      ↓
Relationship becomes part of the Project Graph
```

The Relationship Graph remains canonical.

A visual connection alone is not equivalent to a canonical Atlas relationship.

Invalid relationship objects are rejected by the established Graph boundary.

---

# 25. Validation Workflow

Atlas v0.1 includes canonical Resource validation.

The user/application-level concept is:

```text
Resource
   ↓
Validate
   ↓
Validation Results
```

Validation can report established validation outcomes using the implemented validation result, category, and severity structures.

Validation is observational.

Running validation does not modify:

- AtlasID
- name
- classification
- properties
- tags
- categories
- lifecycle state

---

# 26. Understanding Validation Failures

At the application/API boundary, invalid requests may include:

- invalid Resource identity,
- invalid spatial values,
- missing required data,
- invalid relationship data,
- invalid Resource state.

These requests are rejected according to the specific operation's established contract.

Invalid object types are also rejected at relevant engineering boundaries. This is primarily an API/application contract rather than a normal graphical-user error.

The exact error type and message depend on the specific API or operation.

---

# 27. Saving a Project

Atlas v0.1 includes the established JSON serialization and Project Save/Load architecture.

The conceptual workflow is:

```text
Canonical Atlas Project
        ↓
Atlas serialization
        ↓
UTF-8 JSON representation
        ↓
Persistent project file
```

Saving serializes canonical project state.

The established Save/Load contract includes preservation of supported project information such as:

- project identity,
- metadata,
- Resources,
- Resource identity,
- properties,
- semantic information,
- lifecycle,
- relationships,
- classifications and classification hierarchy.

Saving does not mutate the source Project.

The serialization architecture is not a second Resource model.

Existing project files are not overwritten unless overwrite is explicitly requested.

---

# 28. Loading a Project

The corresponding workflow is:

```text
Project file
      ↓
Atlas deserialization
      ↓
New canonical Atlas Project instance
```

The established Load contract reconstructs a separate Project instance from the serialized representation.

Supported Resource, relationship, classification, and project information is restored according to the serialization contract.

Missing or invalid project files are rejected rather than silently accepted.

The serializer is reused through the established Project persistence boundary rather than introducing a second persistence model.

---

# 29. Import and Export

Atlas v0.1 defines a generic Import/Export adapter boundary.

The architectural workflow is:

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

The generic boundary does **not** mean that every external engineering format is supported.

No concrete external engineering-format adapter is part of the verified v0.1 capability unless separately implemented and verified.

---

# 30. Concrete File Formats and External Systems

The following are outside the verified v0.1 concrete capability:

- IFC
- BIM exchange
- Revit
- CAD/DWG
- DXF
- PDF import intelligence
- Excel integration
- CSV integration
- GIS integration
- remote synchronization
- external-system synchronization

The existence of the generic Import/Export boundary must not be interpreted as support for these formats or systems.

---

# 31. Agents and AI

Atlas v0.1 contains the established Agent Runtime and specialized agent architecture.

For a normal user, the important distinction is:

```text
Atlas canonical state
        ↑
Application / Agent interaction
        ↑
AI or agent reasoning
```

Agents do not become the owner of canonical Resource state.

The v0.1 architecture does not guarantee autonomous general-purpose engineering reasoning.

---

# 32. What Users Should Expect From AI

Users should not assume that Atlas v0.1 can autonomously:

- design complete buildings,
- generate production BIM models,
- reason over every engineering discipline,
- enforce all building codes,
- synchronize with Revit,
- understand arbitrary CAD files,
- perform autonomous construction management,
- or act as a general-purpose engineering copilot.

Those capabilities are outside the verified v0.1 scope unless independently implemented and verified.

---

# 33. Typical v0.1 Resource Workflow (Conceptual)

A typical application-level workflow is:

```text
Create / Open Project
        ↓
Create Resource
        ↓
Assign Classification
        ↓
Inspect Properties
        ↓
Create Relationships
        ↓
Move / Rotate / Scale
        ↓
Validate
        ↓
Save
```

This sequence describes the canonical application-level workflow. It is **not** a claim that a complete graphical frontend currently exposes every step as a clickable UI workflow.

The exact application surface may vary according to the implemented interface.

---

# 34. Resource Identity During Editing

Editing a Resource does not normally replace its engineering identity.

For example:

```text
Move Wall-01
```

changes its spatial state.

It does not mean:

```text
Delete Wall-01
Create Wall-02
```

The same principle applies to Rotate and Scale.

AtlasID remains the canonical engineering identity.

---

# 35. Understanding the 3D Workspace Model

Atlas v0.1 defines a framework-independent 3D workspace model.

It represents Scene and SceneNode presentation state without requiring a renderer such as Three.js, WebGL, WebGPU, or another graphics framework.

The conceptual separation is:

```text
Engineering State
    ↓
Resource + Spatial State

3D Presentation Model
    ↓
Scene + SceneNode

Separate Workspace State
    ↓
Camera + Navigation + Selection + Gizmo
```

A production renderer, viewport implementation, picking/raycasting, and interactive graphics frontend are outside this v0.1 foundation.

Changing presentation state does not itself change canonical engineering identity.

---

# 36. User Workflow: Select and Edit (Conceptual)

The application-level editing workflow is:

```text
Explorer / available application surface
      ↓
Identify Resource
      ↓
Inspect Resource
      ↓
Invoke the required editing operation
      ↓
Provide operation input
      ↓
Atlas validates
      ↓
Canonical state changes
      ↓
Available presentation surface reflects the updated state
```

This describes the application/domain workflow and does not imply a specific renderer, mouse interaction model, or graphical frontend implementation.

---

# 37. User Workflow: Inspect → Edit → Validate

A recommended conceptual v0.1 workflow is:

```text
1. Identify Resource
2. Inspect identity/classification/properties
3. Perform the required application-level edit
4. Validate the resulting Resource
5. Review validation results
6. Save the Project
```

This workflow follows the established separation between editing, validation, and persistence.

---

# 38. Resource Isolation

Atlas v0.1 protects Resource isolation during editing.

An operation on one Resource should not silently mutate unrelated Resource state.

This is explicitly covered by the Resource Editing and Core Validation verification work.

Users can therefore reason about an operation as being scoped to its targeted canonical Resource and its intended associated state.

---

# 39. Deterministic User Operations

Atlas v0.1 emphasizes deterministic operation behavior.

Given the same valid input and equivalent canonical state, an operation should produce the established deterministic result.

Invalid operations are rejected rather than silently producing partial canonical changes.

---

# 40. Common User Errors

## Invalid Resource

If an operation references an invalid Resource identity, the operation is rejected.

## Invalid Spatial Input

Move, Rotate, or Scale operations reject invalid values according to their established contracts.

## Invalid Relationship

A malformed or invalid relationship is rejected by the Graph boundary.

## Invalid Validation Input

The canonical Validation Engine rejects non-Resource input.

## Missing Required Data

Operations with missing required information are rejected according to their command/API contracts.

---

# 41. Troubleshooting Approach

When an operation fails:

1. Confirm that the correct Resource is being targeted.
2. Confirm that the Resource still exists in the Project.
3. Confirm that the requested values are valid.
4. Check the operation's validation/error result.
5. Retry only after correcting the invalid input.
6. If the behavior contradicts the established contract, reproduce it with the smallest possible workflow.

For engineering-level investigation, consult the Developer Guide and engineering specifications.

---

# 42. User vs Developer Documentation

This guide explains user/application workflows.

The Developer Guide explains:

- internal architecture,
- APIs,
- extension rules,
- implementation boundaries,
- testing,
- and development workflow.

Engineering specifications under:

```text
docs/Engineering/Resources/
```

describe the engineering history and contracts.

Users should normally start with this guide rather than the engineering specifications.

---

# 43. v0.1 Scope

The verified Atlas v0.1 foundation includes:

```text
Resource Model
Resource Identity
Classification
Properties
Relationships
Semantics
Lifecycle
Validation
Serialization
Resource Registry
Categories
Constraints
Agent Runtime
Specialized Agents
JSON Serialization
Project Save / Load
Import / Export Boundary
UI Architecture
Application Shell
Dashboard
Explorer
Inspector
Toolbar
Panels
Scene
Camera
Navigation
Selection
Gizmo
Basic Editing
Create
Move
Rotate
Scale
Delete
Duplicate
Core Validation
```

The exact APIs and behavior are defined by the implementation and tests.

The UI and workspace entries above refer to their verified application/presentation models and contracts; they do not imply a complete production graphical frontend or renderer.

---

# 44. Out-of-Scope Capabilities

The following are not verified Atlas v0.1 user capabilities.

### Engineering interoperability

- IFC
- Revit
- BIM synchronization
- DWG/DXF
- production CAD interoperability
- GIS integration

### Advanced AI

- autonomous engineering design
- autonomous building-code compliance
- general-purpose engineering reasoning
- fully autonomous multi-step project execution

### Collaboration

- real-time multi-user editing
- cloud collaboration
- distributed synchronization

### History / Provenance

- dedicated provenance subsystem
- complete revision-history system
- automated change-impact history

### Production infrastructure

- production cloud deployment
- enterprise authentication/authorization
- production distributed storage
- production renderer integration

### Domain completeness

Atlas v0.1 is not a complete architecture, construction, interior-design, BIM, or project-management product.

It is the verified foundation on which such capabilities can be built.

---

# 45. v0.1 Release Verification

The ENG-060 release-readiness verification established:

```text
Targeted tests:
1,536 passed
0 failed

Full regression:
1,930 passed
0 failed

Version:
0.1.0

Technical release readiness:
GREEN
```

Known Python 3.14 / pytest-asyncio deprecation warnings did not constitute test failures.

These numbers represent the verified v0.1 baseline at release-readiness verification time.

---

# 46. User Safety and Data Integrity Principle

Users should treat Atlas canonical state as the authoritative engineering representation.

Presentation changes should not be assumed to be persisted engineering changes unless they pass through the established application/domain operation.

Similarly, an AI or Agent suggestion should not be treated as canonical engineering state merely because it was generated by an Atlas-connected component.

---

# 47. Practical v0.1 Checklist (Conceptual)

Use this as a conceptual v0.1 workflow checklist when operating through an available Atlas application surface:

```text
[ ] Project is available
[ ] Resource exists
[ ] Resource has the intended classification
[ ] Resource properties are correct
[ ] Relationships are established where required
[ ] Spatial state is correct
[ ] Validation has been performed where appropriate
[ ] Validation results have been reviewed
[ ] Project has been saved where persistence is required
```

The checklist does not imply that every item is exposed through a single graphical workflow.

---

# 48. When to Consult the Developer Guide

Use the Developer Guide when you need to know:

- why Atlas is structured a particular way,
- which class/API owns a capability,
- how to extend Atlas,
- how canonical state is represented,
- how tests protect architectural contracts,
- or how Agents/UI interact with the core.

Use the engineering specifications when you need the detailed engineering contract for a particular capability.

---

# 49. Final User Principle

Atlas v0.1 should be used with one fundamental distinction in mind:

> The application and presentation layers show and operate on the Atlas model; they are not the Atlas model.

Resources, their identity, relationships, semantic information, lifecycle, validation, and canonical spatial state belong to the Atlas foundation.

The workspace, selection, camera, panels, SceneNodes, Gizmo, and other presentation structures exist to let applications work with that foundation.

A complete production renderer, graphical frontend, external engineering-format ecosystem, autonomous engineering AI, collaboration platform, and other future capabilities are outside the verified v0.1 scope.

---

# 50. Atlas v0.1 Status

Atlas v0.1 has a verified technical foundation and release-readiness baseline.

This User Guide documents the user/application workflows that are supported by that foundation and deliberately excludes capabilities that are not verified as implemented.

**Atlas v0.1 — User Guide**
