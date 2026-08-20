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

# 4. Understanding the Atlas Workspace

Atlas v0.1 includes the established UI/application architecture developed through the UI milestones.

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

These are user-facing workspace capabilities.

They do not replace the canonical Project/Resource model.

---

# 5. Dashboard

The Dashboard provides a project-level presentation surface.

It is intended to show project information and summaries.

The Dashboard does not become the owner of Resources or relationships.

Users should therefore treat Dashboard information as a view of Project state rather than a separate Project model.

---

# 6. Explorer

The Explorer provides navigation through the Project and its Resources.

Users can use it to locate Resources and work with the established Resource presentation flow.

The Explorer does not create a second copy of the Project.

---

# 7. Inspector

The Inspector provides detailed Resource information.

It is intended for inspecting the selected Resource and its properties/metadata.

The Inspector is read-oriented presentation infrastructure and does not become a second Resource Registry or Resource Graph.

When a Resource is selected, the Inspector can present information from the canonical Resource state.

---

# 8. Toolbar

The Toolbar provides user access to the implemented editing actions.

The Resource editing capabilities established in v0.1 are:

```text
Create
Move
Rotate
Scale
Delete
Duplicate
```

The Toolbar is a presentation entry point.

The actual engineering mutation is performed through the established Application/Command boundary.

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

The Scene represents the 3D workspace/presentation structure.

A SceneNode is not an AtlasResource.

The Scene therefore provides a presentation representation of engineering objects without becoming a second engineering model.

Users can interact with the Scene while the canonical Atlas model remains authoritative.

---

# 11. Camera

The Camera controls the viewport's viewing state.

Camera state is presentation state.

Changing the camera does not change a Resource's engineering identity.

---

# 12. Navigation

Navigation controls how users move through the workspace.

Navigation state is separate from Project and Resource state.

Viewport navigation should therefore not be interpreted as an engineering modification.

---

# 13. Selection

Selection identifies a Resource for the current workspace context.

Selection is based on Atlas identity but is not itself canonical Resource ownership.

Selecting a Resource does not copy or transfer the Resource into the UI.

---

# 14. Gizmo

The Gizmo provides interactive spatial editing within the workspace.

Its role is presentation/application interaction.

The Gizmo does not own canonical Resource state.

When an editing operation is committed, the established application command boundary is responsible for changing canonical spatial state.

---

# 15. Creating a Resource

Atlas v0.1 supports Resource creation.

The user-facing workflow is:

```text
Choose Create
      ↓
Provide the required Resource creation information
      ↓
Specify the Resource classification
      ↓
Optionally provide the Resource name
      ↓
Submit the create operation
      ↓
Atlas creates the Resource
      ↓
Resource becomes part of the Project's canonical Resource Registry
```

The exact input fields and command surface are defined by the implemented application/UI layer.

Creation establishes the Resource's canonical identity.

A created Resource is not merely a visual Scene object.

---

# 16. Inspecting a Resource

A typical inspection workflow is:

```text
Select Resource
      ↓
Open / use Inspector
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

The user workflow is:

```text
Create or select Resource
      ↓
Choose an available Classification
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

The conceptual workflow is:

```text
Select Resource
      ↓
Choose Move
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

The workflow is:

```text
Select Resource
      ↓
Choose Rotate
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

The workflow is:

```text
Select Resource
      ↓
Choose Scale
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

The conceptual workflow is:

```text
Select Resource
      ↓
Choose Delete
      ↓
Confirm / submit the operation as required by the interface
      ↓
Atlas removes the canonical Resource
```

Deletion operates on the canonical Resource identified by AtlasID.

The implementation is designed to preserve project integrity and avoid accidentally deleting unrelated Resources.

---

# 23. Duplicating a Resource

Atlas v0.1 supports Resource Duplicate.

The workflow is:

```text
Select Resource
      ↓
Choose Duplicate
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

A relationship workflow conceptually follows:

```text
Identify source Resource
      ↓
Identify target Resource
      ↓
Create the supported relationship
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

The user-facing concept is:

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

When Atlas rejects invalid input, the user should treat the result as an indication that the requested operation violates an established contract.

Typical categories of invalid input include:

- invalid Resource identity,
- invalid object type,
- invalid spatial values,
- missing required data,
- invalid relationship data,
- invalid Resource state.

The exact error type and message depend on the specific API or operation.

Users should not assume that all failures have the same error format.

---

# 27. Saving a Project

Atlas v0.1 includes the established JSON serialization and Project Save/Load architecture.

The conceptual workflow is:

```text
Canonical Atlas Project
        ↓
Atlas serialization
        ↓
JSON representation
        ↓
Persistent project file
```

Saving serializes canonical project state.

Serialization is not a second Resource model.

---

# 28. Loading a Project

The corresponding workflow is:

```text
Project file
      ↓
Atlas deserialization
      ↓
Canonical Atlas Project
```

The established serialization architecture preserves the supported Project structures.

These include important information such as:

- project identity,
- metadata,
- classifications,
- Resources,
- Resource identity,
- properties,
- semantic information,
- lifecycle,
- relationships.

Relationship endpoints use stable Resource identity rather than recursively embedding duplicate Resource objects.

---

# 29. Import and Export

Atlas v0.1 includes the generic Import/Export boundary established by ENG-038.

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

---

# 30. Concrete File Formats and External Systems

The generic Import/Export architecture does **not** mean that every external engineering format is supported.

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

These must not be presented as available Atlas v0.1 workflows.

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

# 33. A Typical v0.1 Resource Workflow

A complete conceptual workflow is:

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

The exact UI sequence may vary according to the implemented application surface.

The underlying canonical ownership remains the same.

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

# 35. Understanding the 3D View

The 3D view is a workspace representation of Atlas state.

Users should distinguish:

```text
Engineering State
    ↓
Resource + Spatial State

Presentation
    ↓
Scene + SceneNode + Camera + Selection + Gizmo
```

Changing the viewport camera is not an engineering change.

Selecting an object is not transferring Resource ownership to the viewport.

A SceneNode is not itself an Atlas Resource.

---

# 36. User Workflow: Select and Edit

The basic editing workflow is:

```text
Explorer / Scene
      ↓
Select Resource
      ↓
Inspect Resource
      ↓
Choose editing operation
      ↓
Provide operation input
      ↓
Atlas validates
      ↓
Canonical state changes
      ↓
UI reflects the updated state
```

The UI is a presentation surface over the canonical model.

---

# 37. User Workflow: Inspect → Edit → Validate

A recommended v0.1 workflow is:

```text
1. Select Resource
2. Inspect identity/classification/properties
3. Perform the required edit
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

1. Confirm that the correct Resource is selected.
2. Confirm that the Resource still exists in the Project.
3. Confirm that the requested values are valid.
4. Check the operation's validation/error result.
5. Retry only after correcting the invalid input.
6. If the behavior contradicts the established contract, reproduce it with the smallest possible workflow.

For engineering-level investigation, consult the Developer Guide and engineering specifications.

---

# 42. User vs Developer Documentation

This guide explains user workflows.

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

---

# 44. Out-of-Scope Capabilities

The following are not verified Atlas v0.1 user capabilities:

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

# 47. Practical v0.1 Checklist

Before considering a Resource workflow complete:

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

> The UI shows and manipulates the Atlas model; it is not the Atlas model.

Resources, their identity, relationships, semantic information, lifecycle, validation, and canonical spatial state belong to the Atlas foundation.

The workspace, selection, camera, panels, SceneNodes, and other presentation structures exist to let users work with that foundation.

---

# 50. Atlas v0.1 Status

Atlas v0.1 has a verified technical foundation and release-readiness baseline.

This User Guide documents the user-visible workflows that are supported by that foundation and deliberately excludes capabilities that are not verified as implemented.

**Atlas v0.1 — User Guide**
