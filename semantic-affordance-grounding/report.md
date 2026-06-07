# Homework 5 Report - Group 5

## Project Focus
This repository models the semantic grounding for Team 5's AI Capstone project. Our primary focus is the **Toy Blocks Collection** task for the baseline and an **Advanced Level** task involving the capture of a dynamic, moving target (simulated as a **Moving Mouse** block). The ontology provides a semantic layer that allows the robot to distinguish between static reference objects and dynamic targets, while inferring graspability based on object affordances.

## Repository Contents
- `ontology/group-ontology.ttl`: Group-authored ontology containing Team 5 classes, properties, task instances, object instances, annotations, and reasoning axioms.
- `ontology/inferred-results.ttl`: Exported inferred ontology result after running the OWL reasoner.
- `ontology/imports/`: Imported course ontology resources, including the shared affordance vocabulary and SKOS alignment file.
- `queries/`: SPARQL queries for inferred graspable objects and task object roles.
- `results/`: Saved query output and screenshots showing the query results and inferred class hierarchy.
- `README.md`: Repository instructions, file links, expected output, and reasoning workflow summary.

## Namespace Policy
- **Shared Course Vocabulary (`cap:`):** `<https://hcis.io/ontology/aicapstone/2026/>`. We reuse these terms for baseline object types (Cup, Fork, Knife, Plate, ToyBlock, Basket) and task roles.
- **Team 5 Modeling Space (`g05:`):** `<https://hcis.io/ontology/aicapstone/2026/group05/>`. This namespace contains our authored individuals, task variants, and advanced classes like `MovingMouseBlock`.

## Modeling Summary
The ontology is designed with a strict layer separation to avoid common modeling pitfalls:

1.  **Object Types:** Reused course classes (`cap:Cup`, `cap:ToyBlock`) and new project-specific subclasses (`g05:BridgeBlock`, `g05:MovingMouseBlock`).
2.  **Task Roles:** Grounding objects into their functional context (e.g., `cap:CollectableObject`, `cap:TargetObject`).
3.  **Affordances:** Defining the "action possibilities." We introduced `g05:PrecisionGraspingAffordance` for static blocks and `g05:DynamicGraspingAffordance` for the moving mouse block.
4.  **Group Properties:** We introduced `g05:hasMass` as a datatype property for simulated object mass and `g05:requiresInterceptionOf` as an object property linking the dynamic capture task to the moving target that must be intercepted.
5.  **Instances:** 10 task-relevant observed object individuals (individuals are never declared under the `cap:` namespace).

## Main Object Table
| Instance | Type | Task Role | Affordance |
| --- | --- | --- | --- |
| `g05:blueCup01` | `cap:Cup` | `cap:TargetObject` | `cap:GraspingAffordance`, `cap:StackabilityAffordance` |
| `g05:pinkCup01` | `cap:Cup` | `cap:TargetObject` | `cap:GraspingAffordance`, `cap:StackabilityAffordance` |
| `g05:knife01` | `cap:Knife` | `cap:TargetObject` | `cap:GraspingAffordance` |
| `g05:fork01` | `cap:Fork` | `cap:TargetObject` | `cap:GraspingAffordance` |
| `g05:plate01` | `cap:Plate` | `cap:ReferenceObject` | `cap:SupportAffordance` |
| `g05:greenBlock01` | `g05:BridgeBlock` | `cap:CollectableObject`, `g05:HighPriorityTarget` | `g05:PrecisionGraspingAffordance` |
| `g05:blueBlock01` | `g05:CylinderBlock` | `cap:CollectableObject` | `cap:GraspingAffordance` |
| `g05:redBlock01` | `g05:TriangleBlock` | `cap:CollectableObject` | `cap:GraspingAffordance` |
| `g05:storageBox01` | `g05:StorageBox` | `cap:ContainerTarget` | `cap:ContainmentAffordance` |
| `g05:movingMouseBlock01` | `g05:MovingMouseBlock` | `cap:CollectableObject` | `g05:mouse01GraspAffordance` |

## Reasoning and Inference
The central reasoning target is `cap:GraspableObject`. Instead of manually asserting which objects are graspable, we use the following OWL 2 DL equivalent class axiom:

`cap:GraspableObject ≡ cap:PhysicalObject ⊓ ∃ cap:hasAffordance.cap:GraspingAffordance`

By making `g05:PrecisionGraspingAffordance` and `g05:DynamicGraspingAffordance` subclasses of the course `cap:GraspingAffordance`, the reasoner (HermiT 1.4.3) successfully classifies the specialized bridge block and the moving mouse block as graspable objects.

## Query Results
The SPARQL query `queries/graspable_objects.rq` was executed over the inferred model. The results confirm that the 8 objects intended for manipulation (including the new dynamic target) are correctly inferred as `cap:GraspableObject`, while the plate and storage box are excluded.

## Design Choices and Limitations
- **Dynamic Capture:** We modeled the "Mouse" as a subclass of `ToyBlock` but with a unique `DynamicGraspingAffordance` to represent the need for the robot to react to velocity and position over time.
- **Physical Grounding:** We utilized `g05:hasMass` to bridge the semantic model with the simulation physics in NVIDIA Isaac Sim.
- **Limitations:** Currently, the ontology assumes any object with a grasping affordance *is* graspable, regardless of its current distance or speed. A more advanced model could include state-dependent graspability (e.g., "Graspable only when within reach").

## Imported Resources
- `ontology/imports/course-affordance.ttl`: Shared course vocabulary.
- `ontology/imports/course-alignment.ttl`: SKOS alignment to CORA/SOMA robotics ontologies.
