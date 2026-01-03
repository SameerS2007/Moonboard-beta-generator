# Climbing Beta Generator (MVP)

## Overview

This project is an MVP prototype for a system that generates **step-by-step bouldering beta** from a single image of a climbing wall.

The long-term goal is to combine **computer vision**, **algorithmic planning**, and **visualization** to analyze climbing problems and suggest plausible solutions. This MVP intentionally focuses on the *reasoning core* of the system before adding machine learning.

At this stage, holds are **manually specified**, and the system outputs a **textual beta sequence** describing how a climber would move up the wall.

---

## MVP Scope (Locked)

**Input**

* A set of manually defined holds with 2D coordinates

**Output**

* A step-by-step textual beta (console output)

**Assumptions**

* Static moves only (no dynos)
* Average climber proportions
* One valid solution is sufficient
* No grading or difficulty estimation

---

## System Architecture (MVP)

```
Manual Hold Input
      
Graph Construction
      
Constraint-Based Path Planning
      
Textual Beta Generation
```

This MVP establishes the planning and reasoning foundation that later ML components will build upon.

---

## Hold Representation

Each hold is represented as:

```python
{
  "id": int,
  "x": float,  # normalized [0, 1]
  "y": float   # normalized [0, 1]
}
```

Coordinates are normalized relative to the image size to keep the system resolution-independent.

---

## Planning Model

The wall is treated as a **graph**:

* Nodes = holds
* Edges = reachable moves based on distance constraints

A valid move must satisfy:

* Euclidean distance ≤ max reach
* Positive height progression (generally upward)

The planner searches for a path from a designated **start hold** to a **finish hold** using a graph search algorithm (A*).

---

## Textual Beta Generation

Each transition between holds is converted into a natural-language instruction using templates:

Example:

```
1. Start on the lower left hold.
2. Move your right hand up to the next crimp.
3. Bring your feet up and reach for the finish.
```

---

## Planned Extensions

* Automatic hold detection using computer vision
* Hold type classification
* Visual stick-figure overlays
* Move difficulty scoring using ML
* Personalized climber profiles

---

## Technologies (Current & Planned)

**Current**

* Python 3
* NumPy

**Planned**

* PyTorch
* OpenCV
* YOLOv8

---

## Status

MVP in progress — planning logic under development.
