#THEORY
##Maze Routing, Lee’s Algorithm, and Physical Routing Concepts
1. Overview of Routing and Lee’s Algorithm

Routing is the process of physically connecting different components of an integrated circuit—such as flip-flops, clocks, and standard cells—using metal interconnects. The goal is to create reliable signal paths while minimizing delay, congestion, and area usage.

Several routing algorithms exist, including:

Steiner Tree Algorithm

Line Search Algorithm

Lee’s Maze Routing Algorithm

Routing primarily aims to:

Find the shortest possible connection path

Reduce unnecessary bends and detours

Conform to Manhattan routing geometry (horizontal and vertical paths only)

From a computational perspective, routing involves path-finding between nodes, while in VLSI design it translates to placing metal wires on silicon layers. Lee’s Algorithm is especially suitable for grid-based routing problems commonly found in physical design.

##2. Working Principle of Lee’s Maze Routing Algorithm

Lee’s Algorithm operates on a grid that represents the available routing area and systematically explores all possible paths between a source and a target.

Step 1: Grid Initialization

The routing grid is classified into:

Obstacles: Blocked regions such as macros or reserved areas

Free cells: Available routing space

Source: Starting point of the connection

Target: Destination point

Step 2: Wave Propagation

Starting from the source, the algorithm expands outward in four directions—up, down, left, and right—assigning incremental cost values to each visited cell. Expansion continues until the target is reached or no valid paths remain.

Step 3: Path Backtracking

Once the destination is reached, the algorithm traces back from the target to the source by following the decreasing cost values, resulting in the shortest legal routing path.

Key constraints include:

Manhattan-only movement

Strict obstacle avoidance

No diagonal routing or overlap with blocked regions

##3. Design Rule Check (DRC)

All routing must comply with fabrication rules defined by the foundry, known as Design Rules.

Typical DRC requirements include:

Minimum wire width

Minimum spacing between wires

Minimum pitch between routing tracks

Legal via dimensions and spacing

The purpose of DRC is to ensure manufacturability, prevent electrical failures, and maintain signal integrity. Any violations detected after routing must be corrected before fabrication.

##4. Signal Shorts and Metal Layer Switching

Signal shorts can occur due to routing congestion and may cause functional or timing failures.

To resolve these issues:

Routes are moved to higher metal layers

Vias are inserted to transition between layers

All vias and layer transitions must satisfy metal-specific design rules, such as preferred routing directions (e.g., M1 vertical, M2 horizontal). While higher metal layers often require wider wires, they help alleviate congestion.

##5. Routing Stages in VLSI Design

Routing is generally divided into two phases:

Global Routing

Also called coarse or fast routing

Divides the layout into routing regions

Determines approximate routing paths and channel usage

Detailed Routing

Performs precise routing at the track level

Finalizes wire placement and via insertion

Ensures complete DRC compliance

Global routing defines the routing strategy, while detailed routing ensures correctness and manufacturability.

##6. TritonRoute: Detailed Routing Engine

TritonRoute is an open-source detailed router used in the OpenROAD flow and is invoked through the run_routing command.

Key Capabilities:

Routing Guide Compliance

Follows routing guides generated during earlier stages

Respects preferred routing directions per metal layer

Uses higher layers to resolve non-preferred routing

Inter-Region Connectivity

Divides the design into routing panels

Ensures legal routing across panels using bridging techniques

Layer-Aware Routing Strategy

Routes alternating panels sequentially

Improves routing efficiency and reduces congestion

##7. Optimization Using MILP

TritonRoute applies Mixed Integer Linear Programming (MILP) to optimize routing between Access Point Clusters (APCs).

The process includes:

Cost evaluation of access points

Construction of a Minimum Spanning Tree (MST)

Selection of lowest-cost routing paths

This approach minimizes wire length and congestion while ensuring optimal connectivity.

##8. Routing Execution and Final Output

Executing run_routing performs both global and detailed routing.

Key observations:

Uses iterative refinement (Strategy 0)

Initial DRC violations are gradually reduced to zero

Multiple optimization iterations are performed

Runtime typically ranges from 20 to 30 minutes, depending on design size

The final routed design is generated in DEF or GDS format and is ready for signoff and fabrication.



![image alt](https://github.com/Sivananth-G/VSDNASSCOM---Digital-VLSI-SoC-design-and-planning/blob/95e3b4191c1071abe4cb6e2e72d98b6c862275bc/Day5/Screenshot%202026-02-01%20161550.png)
![image alt](https://github.com/Sivananth-G/VSDNASSCOM---Digital-VLSI-SoC-design-and-planning/blob/95e3b4191c1071abe4cb6e2e72d98b6c862275bc/Day5/Screenshot%202026-02-01%20162520.png)
![image alt](https://github.com/Sivananth-G/VSDNASSCOM---Digital-VLSI-SoC-design-and-planning/blob/95e3b4191c1071abe4cb6e2e72d98b6c862275bc/Day5/Screenshot%202026-02-01%20162642.png)
![image alt](https://github.com/Sivananth-G/VSDNASSCOM---Digital-VLSI-SoC-design-and-planning/blob/95e3b4191c1071abe4cb6e2e72d98b6c862275bc/Day5/Screenshot%202026-02-01%20162707.png)
![image alt](https://github.com/Sivananth-G/VSDNASSCOM---Digital-VLSI-SoC-design-and-planning/blob/95e3b4191c1071abe4cb6e2e72d98b6c862275bc/Day5/Screenshot%202026-02-01%20162827.png)
![image alt](https://github.com/Sivananth-G/VSDNASSCOM---Digital-VLSI-SoC-design-and-planning/blob/95e3b4191c1071abe4cb6e2e72d98b6c862275bc/Day5/Screenshot%202026-02-01%20162905.png)
![image alt](https://github.com/Sivananth-G/VSDNASSCOM---Digital-VLSI-SoC-design-and-planning/blob/95e3b4191c1071abe4cb6e2e72d98b6c862275bc/Day5/Screenshot%202026-02-01%20162930.png)
![image alt](https://github.com/Sivananth-G/VSDNASSCOM---Digital-VLSI-SoC-design-and-planning/blob/95e3b4191c1071abe4cb6e2e72d98b6c862275bc/Day5/Screenshot%202026-02-01%20163038.png)
![image alt](https://github.com/Sivananth-G/VSDNASSCOM---Digital-VLSI-SoC-design-and-planning/blob/95e3b4191c1071abe4cb6e2e72d98b6c862275bc/Day5/Screenshot%202026-02-01%20164515.png)
![image alt](https://github.com/Sivananth-G/VSDNASSCOM---Digital-VLSI-SoC-design-and-planning/blob/95e3b4191c1071abe4cb6e2e72d98b6c862275bc/Day5/Screenshot%202026-02-01%20164537.png)
![image alt](https://github.com/Sivananth-G/VSDNASSCOM---Digital-VLSI-SoC-design-and-planning/blob/95e3b4191c1071abe4cb6e2e72d98b6c862275bc/Day5/Screenshot%202026-02-01%20164800.png)
![image alt](https://github.com/Sivananth-G/VSDNASSCOM---Digital-VLSI-SoC-design-and-planning/blob/95e3b4191c1071abe4cb6e2e72d98b6c862275bc/Day5/Screenshot%202026-02-01%20164840.png)
![image alt](https://github.com/Sivananth-G/VSDNASSCOM---Digital-VLSI-SoC-design-and-planning/blob/95e3b4191c1071abe4cb6e2e72d98b6c862275bc/Day5/Screenshot%202026-02-01%20165037.png)
![image alt](https://github.com/Sivananth-G/VSDNASSCOM---Digital-VLSI-SoC-design-and-planning/blob/95e3b4191c1071abe4cb6e2e72d98b6c862275bc/Day5/Screenshot%202026-02-01%20165124.png)
![image alt](https://github.com/Sivananth-G/VSDNASSCOM---Digital-VLSI-SoC-design-and-planning/blob/95e3b4191c1071abe4cb6e2e72d98b6c862275bc/Day5/Screenshot%202026-02-01%20165322.png)
![image alt](https://github.com/Sivananth-G/VSDNASSCOM---Digital-VLSI-SoC-design-and-planning/blob/95e3b4191c1071abe4cb6e2e72d98b6c862275bc/Day5/Screenshot%202026-02-01%20170317.png)
![image alt](https://github.com/Sivananth-G/VSDNASSCOM---Digital-VLSI-SoC-design-and-planning/blob/95e3b4191c1071abe4cb6e2e72d98b6c862275bc/Day5/Screenshot%202026-02-01%20170343.png)
