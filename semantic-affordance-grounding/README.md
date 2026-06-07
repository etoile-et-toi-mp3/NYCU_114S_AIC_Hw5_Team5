# Homework 5: Ontology-based Semantic Grounding

**Team 5 Members:**
- 黃庭筠 (112550105)
- 蕭宇岑 (112550179)
- 陳璽安 (112550184)
- 傅永威 (112550107)
- 許書瑋 (112550191)
- 周佑康 (112550078)

## What This Repo Contains
This repository packages the homework ontology work for Team 5. The semantic focus is toy blocks collection from the final project, while the other baseline course objects are also modeled so the homework scope is complete.

## Selected Task
Our group has selected the **Toy Blocks Collection** task for the final project. We also model an **Advanced Level** extension that involves capturing a dynamic, moving target represented as a moving block that simulates a mouse.

## Repository Layout
- `ontology/group-ontology.ttl`: the main authored ontology
- `ontology/inferred-results.ttl`: inferred `cap:GraspableObject` memberships
- `ontology/imports/course-affordance.ttl`: local copy of the shared course vocabulary
- `ontology/imports/course-alignment.ttl`: SKOS alignment reference
- `queries/graspable_objects.rq`: query for inferred graspable objects
- `queries/task_objects.rq`: query for task objects and roles
- `results/graspable_objects_output.txt`: saved query result
- `report.md`: design report

## File Links
- [Group ontology](ontology/group-ontology.ttl)
- [Inferred results](ontology/inferred-results.ttl)
- [Course affordance import](ontology/imports/course-affordance.ttl)
- [Course alignment import](ontology/imports/course-alignment.ttl)
- [Graspable objects query](queries/graspable_objects.rq)
- [Task objects query](queries/task_objects.rq)
- [Graspable objects output](results/graspable_objects_output.txt)
- [Graspable objects screenshot](results/screenshots/graspable_objects_result.png)
- [Inferred graspable object class screenshot](results/screenshots/inferred_graspable_object_class.png)
- [Task objects screenshot](results/screenshots/task_objects_result.png)
- [Report](report.md)
- Source code: not used; reasoning was performed with Protégé 5.6.3 and HermiT 1.4.3.

## Main Object Table
| Instance | Type | Role | Affordance |
| --- | --- | --- | --- |
| `g05:blueCup01` | `cap:Cup` | `cap:TargetObject` | grasping, stackability |
| `g05:pinkCup01` | `cap:Cup` | `cap:TargetObject` | grasping, stackability |
| `g05:knife01` | `cap:Knife` | `cap:TargetObject` | grasping |
| `g05:fork01` | `cap:Fork` | `cap:TargetObject` | grasping |
| `g05:plate01` | `cap:Plate` | `cap:ReferenceObject` | support |
| `g05:greenBlock01` | `g05:BridgeBlock` | `cap:CollectableObject`, `g05:HighPriorityTarget` | precision grasping |
| `g05:blueBlock01` | `g05:CylinderBlock` | `cap:CollectableObject` | grasping |
| `g05:redBlock01` | `g05:TriangleBlock` | `cap:CollectableObject` | grasping |
| `g05:storageBox01` | `g05:StorageBox` / `cap:Basket` | `cap:ContainerTarget` | containment |
| `g05:movingMouseBlock01` | `g05:MovingMouseBlock` | `cap:CollectableObject` | dynamic grasping |

## Project Scope
The ontology models the baseline course object set and the team task:

- cup stacking: blue cup, pink cup
- cutlery arrangement: knife, fork, plate
- toy blocks collection: green bridge block, blue cylinder block, red triangle block, storage box
- **Advanced Task**: Dynamic target capture with `g05:movingMouseBlock01`

The task-level extension includes specialized object classes for the final project assets and a `g05:hasMass` property to ground simulated physics values.

## How The Ontology Works
The ontology separates:

- object type: `cap:Cup`, `cap:Knife`, `cap:Fork`, `cap:Plate`, `cap:ToyBlock`, `cap:Basket`, `g05:BridgeBlock`, etc.
- task role: `cap:TargetObject`, `cap:ReferenceObject`, `cap:ContainerTarget`, `cap:CollectableObject`, `g05:HighPriorityTarget`
- affordance: `cap:GraspingAffordance`, `cap:StackabilityAffordance`, `cap:SupportAffordance`, `cap:ContainmentAffordance`, `g05:PrecisionGraspingAffordance`
- instance: `g05:blueCup01`, `g05:knife01`, `g05:greenBlock01`, and so on
- inferred class: `cap:GraspableObject`

`cap:GraspableObject` is defined by OWL restriction, so the graspable objects are derived from object facts rather than manually asserted.

## Namespace Policy
- `cap:` is the shared course namespace.
- `g05:` is the team namespace for authored objects, affordance individuals, and task individuals.

## Query Instructions
The intended workflow is:

1. Load `ontology/group-ontology.ttl` together with the imported course files in an OWL 2 reasoner (e.g., Protégé with HermiT).
2. Run the reasoner to infer class memberships.
3. Export the inferred graph to `ontology/inferred-results.ttl`.
4. Run `queries/graspable_objects.rq` over the inferred model.
5. Save the result in `results/graspable_objects_output.txt`.

## Inference Generation
The file `ontology/inferred-results.ttl` was generated using the **HermiT 1.4.3** reasoner within **Protégé 5.6.3**. The reasoner processed the OWL existential restrictions to classify all physical objects with at least one grasping affordance as `cap:GraspableObject`.

## Expected Graspable Objects
The inferred graspable objects include:

- `g05:blueCup01`
- `g05:pinkCup01`
- `g05:knife01`
- `g05:fork01`
- `g05:greenBlock01` (Inferred via `g05:PrecisionGraspingAffordance` subclass of `cap:GraspingAffordance`)
- `g05:blueBlock01`
- `g05:redBlock01`
- `g05:movingMouseBlock01` (Inferred via `g05:DynamicGraspingAffordance` subclass of `cap:GraspingAffordance`)

The plate and storage box are intentionally modeled with support/container roles instead of grasping roles.
