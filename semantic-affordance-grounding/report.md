# Homework 5 Report - Group 5

## Project Focus
This repository models the semantic grounding for Team 5's AI Capstone project. Our primary focus is the **Toy Blocks Collection** task for the baseline and an **Advanced Level** task involving the capture of a dynamic, moving target (simulated as a **Moving Mouse** block). The ontology provides a semantic layer that allows the robot to distinguish between static reference objects and dynamic targets, while inferring graspability based on object affordances.

## Namespace Policy
- **Shared Course Vocabulary (`cap:`):** `<https://hcis.io/ontology/aicapstone/2026/>`. We reuse these terms for baseline object types (Cup, Fork, Knife, Plate, ToyBlock, Basket) and task roles.
- **Team 5 Modeling Space (`g05:`):** `<https://hcis.io/ontology/aicapstone/2026/group05/>`. This namespace contains our authored individuals, task variants, and advanced classes like `MovingMouseBlock`.

## Modeling Summary
The ontology is designed with a strict layer separation to avoid common modeling pitfalls:

1.  **Object Types:** Reused course classes (`cap:Cup`, `cap:ToyBlock`) and new project-specific subclasses (`g05:BridgeBlock`, `g05:MovingMouseBlock`).
2.  **Task Roles:** Grounding objects into their functional context (e.g., `cap:CollectableObject`, `cap:TargetObject`).
3.  **Affordances:** Defining the "action possibilities." We introduced `g05:PrecisionGraspingAffordance` for static blocks and `g05:DynamicGraspingAffordance` for the moving mouse block.
4.  **Instances:** 10 task-relevant observed object individuals (individuals are never declared under the `cap:` namespace).

## Main Object Table

## Reasoning and Inference

## Query Results
