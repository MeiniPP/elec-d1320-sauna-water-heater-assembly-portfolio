# ELEC-D1320: Automated Sauna Water Heater Assembly Simulation

A collaborative Visual Components simulation of a robotic cell for assembling a Finnish sauna water heater. The work was completed for Aalto University's ELEC-D1320 Robotics course in the Aalto Win 3D environment.

## Project overview

The assignment models a production flow from component delivery, through robotic handling and heater assembly, to an outfeed conveyor. The water heater body is represented as a hollow cuboid. Tube features are built from the Visual Components library object named `Tube Geometry`; the course material does not provide more specific part names for these tube features, so this README refers to them generically as tubes or tube fittings.

The layout is an offline digital cell simulation. It represents equipment, workpieces, material flow, robot motion and signals in Visual Components; no live connection to a physical production line or live factory data is included in the published materials.

## Virtual cell and robot models

The saved layout packages robot models including:

- ABB IRB 2600ID-8/2.0
- KUKA KR 22 R1610

The cell contains three conveyor objects: two serve the main component supply and handling flow, and a third carries the completed assembly out of the processing area. Conveyor sensors, a robot floor track, a safety area and end-of-arm tooling are also represented. Moving workpieces and tools use Visual Components' component hierarchy: parent-child relationships matter when parts move between conveyors, robot tools and assembly positions. Weld paths are associated with the relevant part hierarchy, so keeping the path's parent stable is important during simulated transfers.

## Robot programming and motion

The robot programs coordinate part pickup, transfer, placement and assembly operations. Motion types include:

- **Point-to-point (PTP):** approach, clearance, transfer and positioning moves between process locations.
- **Linear motion:** controlled straight-line motion where the tool must follow a defined path, including welding paths.

Base and tool frames define the work and end-effector coordinate systems used by robot programs. In the Delfoi welding workflow, the torch tool frame (TCP) is set at the torch tip so the programmed path follows the intended weld line; welding setup and execution were Joris's responsibility.

The layout also uses robot and sensor signals to coordinate cell actions and part handoffs. Motion planning accounts for robot reach, joint limits, workspace envelopes, the Safety Area and possible collisions with parts, equipment or another robot.

## Assembly and welding sequence

1. Heater body and tube components arrive through the conveyor system.
2. Robots pick, lift, transfer and place parts in the assembly area.
3. The heater body is held while tube features are tack-welded in position, then welded along the planned path.
4. The assembled heater is transferred to an outfeed conveyor beyond the safety area.

Welding was Joris's responsibility. The saved layout includes Delfoi Arc 4 path entries, consistent with the course's Delfoi welding add-on workflow. The welding sequence holds a tube feature against the heater body, applies a tack weld, then follows the planned weld path. Joris also recorded the demonstration video and helped proofread and correct my part.

## My contribution

I was responsible for all project work other than welding, including:

- Modeling and arranging the virtual workcell and heater assembly.
- Programming robot handling motions, including PTP and linear moves, pickup and placement sequences, and end-effector/base frames.
- Configuring robot communication and signal-based coordination with the conveyor sensors and other cell operations.
- Planning robot reach and workspace, and addressing collision and joint-limit constraints.

## Course and tools

- **Course:** ELEC-D1320 Robotics, Aalto University
- **Development environment:** Aalto Win 3D
- **Simulation:** Visual Components Premium OLP 4.9.2.25 (version identified in the saved model metadata)
- **Welding path workflow:** Delfoi Arc 4 / Visual Components welding add-on

## Public materials and verification

This repository is a portfolio summary only. The full `.vcmx` simulation and demonstration video remain in the private project repository because the simulation package contains eCatalog and vendor assets whose public redistribution permission has not been established. The course handout is not included.

The project files were inspected when preparing this summary, but the simulation was not launched as part of this documentation update. The public README records the team's reported division of work; it is not an independent verification of the simulation results.
