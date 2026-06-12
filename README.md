# Swarm Robotics — Kilobot Autonomous Navigation

**MSc Robotics Dissertation | University of Sheffield | 2024-2025**
**Supervisor: Dr. Morgan Jones**

---

## What This Project Does

This project implements a decentralised hybrid path planning framework for a swarm of 10 Kilobot robots navigating a shared environment. Each robot independently plans and executes its path while coordinating with neighbours through local communication.

The system combines two approaches:

- **A* Path Planning** on a 50x50 occupancy grid with obstacle inflation buffers for collision-safe routing
- **Opportunistic Path Seeding (OPS)** — a novel algorithm developed for this project that allows robots to share partial path information with neighbours, reducing redundant replanning across the swarm

A **Leader-Follower formation control** baseline was also implemented for comparison.

---

## Key Results

| Metric | Result |
|---|---|
| Goal completion rate | 100% across 30+ runs |
| Collisions | Zero in all test configurations |
| Redundant replanning reduction (OPS vs baseline) | 8% |
| Communication dropout tolerance | Up to 40% packet loss |
| Robots in fleet | N = 10 |
| Grid size | 50 x 50 occupancy grid |

---

## Tech Stack

- MATLAB R2024b
- A* path planning algorithm
- Occupancy grid mapping with Minkowski inflation
- Opportunistic Path Seeding (OPS) — novel algorithm
- Leader-Follower formation control
- Fault tolerance under intermittent communication

---

## Repository Structure

```
swarm-robotics-kilobot/
├── path_planner/
│   ├── astar_planner.m          - A* implementation on occupancy grid
│   ├── grid_setup.m             - Occupancy grid initialisation
│   └── obstacle_inflation.m     - Obstacle buffer expansion
├── algorithms/
│   ├── ops_algorithm.m          - Opportunistic Path Seeding (novel)
│   └── leader_follower.m        - Formation control baseline
├── simulation/
│   ├── simulation_runner.m      - Main simulation entry point
│   ├── robot_agent.m            - Individual robot behaviour
│   └── communication_model.m   - Packet loss simulation
├── results/
│   ├── validation_results.png   - Performance across 30+ runs
│   └── comparison_plot.png      - OPS vs baseline comparison
└── README.md
```

---

## How to Run

1. Open MATLAB R2024b
2. Add the project folder to your MATLAB path:
   ```matlab
   addpath(genpath('swarm-robotics-kilobot'))
   ```
3. Run the main simulation:
   ```matlab
   simulation_runner
   ```
4. Results will display in the MATLAB figure window and save to the `results/` folder

---

## Algorithm Overview

### A* Path Planning
Each robot maintains a local occupancy grid. Obstacles are inflated using a buffer zone to ensure safe clearance. A* searches for the optimal path from current position to goal.

### Opportunistic Path Seeding (OPS)
When a robot has computed a path segment, it broadcasts partial waypoints to nearby robots via local communication. Receiving robots can seed their own planners with this information, avoiding redundant computation in overlapping regions. This reduced replanning by 8% compared to fully independent planning.

### Leader-Follower Baseline
One robot acts as leader, navigating independently using A*. Follower robots maintain a fixed offset formation relative to the leader. Used as a performance comparison baseline.

---

## Related

- Patent No. 409171-001 — Automated Clay Sculpting Printer (separate mechatronics project)
- LinkedIn: [pratik-chodankar200114](https://www.linkedin.com/in/pratik-chodankar200114)
