# Optimized Visibility Graph with Obstacle Merging for UAV Path Planning

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Status](https://img.shields.io/badge/Status-Research-orange)
![Topic](https://img.shields.io/badge/Topic-Robotics%20%26%20Path%20Planning-lightgrey)

**An advanced hybrid path planning solution for Unmanned Aerial Vehicles (UAVs) operating in complex, dynamic environments.**

This repository implements a novel approach to the **Visibility Graph** algorithm. By introducing an **Obstacle Merging Mechanism**, we significantly reduce the number of graph nodes and edges, optimizing computational time without sacrificing path safety. 
This global planner is integrated with a local planner (MPC/Reactive) to handle dynamic threats (under developing).

---

## Table of Contents
- [Introduction](#-introduction)
- [Key Features](#-key-features)
- [Algorithm Overview](#-algorithm-overview)
  - [Obstacle Merging (Global)](#1-obstacle-merging-strategy)
  - [Local Avoidance](#2-local-planner)
- [Project Structure](#-project-structure)
- [Installation](#-installation)
- [Usage](#-usage)
- [Comparisons & Benchmarks](#-comparisons--benchmarks)
- [Contributing](#-contributing)

---

## Introduction

Standard Visibility Graph algorithms provide optimal shortest paths but suffer from $O(n^2)$ complexity, making them inefficient in environments with dense obstacle clusters. 

This project solves this by pre-processing the map to **merge nearby obstacles**. Instead of calculating visibility lines for every vertex of every obstacle, the algorithm treats clusters of obstacles as single simplified polygons. This "Merged Visibility Graph" is then used for global pathfinding, while a local planner handles real-time collision avoidance.

## Key Features

* **Optimized Performance:** Reduces computation time by merging adjacent obstacles, drastically cutting down the Visibility Graph size.
* **Hybrid Architecture:** Combines global static planning with local dynamic avoidance (MPC/Bug-based logic).
* **Benchmarking:** Includes implementations of comparison algorithms:
    * **RRT-Connect** (Rapidly-exploring Random Tree)
    * **DWA** (Dynamic Window Approach)
    * **Standard VGBOA** (Visibility Graph without merging)
* **Visualization:** Tools to visualize the merging process, the generated graph, and the UAV's flight trajectory.

---

## Algorithm Overview

### 1. Obstacle Merging Strategy
The core contribution of this research relies on simplifying the environment geometry:
1.  **Clustering:** The algorithm identifies obstacles located within a specific proximity threshold.
2.  **Hull Construction:** It generates a Convex Hull (or bounding polygon) around these clusters.
3.  **Graph Generation:** The Visibility Graph is built using only the vertices of these "merged" shapes, significantly reducing the search space.

### 2. Local Planner
While the global planner provides the general route, the local planner ensures the UAV:
* Adheres to kinematic constraints (Maximum Turning Angle).
* Applies fast reactive optimization framework to apply onboard of the drone to avoid collision and follow the predefined path ( under developing ) 

---

## Project Structure

```plaintext
.
├── Code file
│   ├── comparison algorithm      # Baselines for performance evaluation
│   │   ├── global planner
│   │   │   ├── RRT_Connect       # RRT Connect implementation
│   │   │   └── VGBOA.py          # Standard Visibility Graph (No merging)
│   │   └── local planner
│   │       └── DWA_...           # Dynamic Window Approach
│   │
│   └── proposed algorithm        # CORE SOLUTION
│       ├── global_planner.py     # Base planner logic
│       ├── new_global_planner.py # IMPROVED: Logic with Obstacle Merging
│       ├── new_mpc.py            # Model Predictive Control
│       ├── new_solution.py       #
│       ├── local_planner.py      # Local avoidance logic
│       ├── maximum_turning...    # Kinematic constraint helper
│       └── test.py               # Unit tests
├── requirements.txt              # Python dependencies
└── README.md                     # Documentation
```
## Installation
* **Clone the repository:**

```bash

git clone [https://github.com/anhbanhieucode/Advance-visibility-graph-and-bug-algorithm-for-UAV-in-dynamic-environment.git](https://github.com/anhbanhieucode/Advance-visibility-graph-and-bug-algorithm-for-UAV-in-dynamic-environment.git)
cd Advance-visibility-graph-and-bug-algorithm-for-UAV-in-dynamic-environment
```
* **Install dependencies:** It is recommended to use a virtual environment.

```bash

pip install numpy matplotlib scipy networkx
```
