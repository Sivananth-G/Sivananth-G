# THEORY:
Overview of Chip Packaging and Design Flow

In the theory session, we were first introduced to a QFN-48 package, where the internal structure of an IC package and the components present inside a chip were discussed. The major components include:

Pads: Pads act as the interface between the external package and the internal circuitry of the chip. They are responsible for carrying electrical signals into and out of the IC.

Core: The core is the central region of the chip where the main digital logic resides. It contains fundamental building blocks such as logic gates, multiplexers, and flip-flops that implement the processor’s functionality.

Die: The die is the silicon substrate on which the core is fabricated. A single die may contain one or multiple cores depending on the design.

We also studied foundry IPs, which are pre-designed and thoroughly verified components provided by the foundry. These IPs are typically complex analog or mixed-signal blocks such as PLLs, ADCs, SRAMs, and similar modules.

In addition, we learned about macros, which are similar to foundry IPs but are composed purely of digital logic. These are reusable, pre-designed blocks created for common applications, such as GPIO, SPI, and other standard interfaces.

Introduction to OpenLANE and RTL-to-GDSII Flow

We were then introduced to OpenLANE, an open-source, fully automated RTL-to-GDSII flow. OpenLANE enables ASIC design without manual intervention by integrating several open-source tools such as Yosys, OpenROAD, Magic, and TritonRoute.

The complete RTL-to-GDSII flow involves the following steps:

Synthesis: The Verilog RTL is synthesized into a gate-level netlist. Static Timing Analysis (STA) is performed on this netlist before proceeding to floorplanning.

Floorplanning and Power Planning: The core area is defined, cells are arranged efficiently, and power/ground networks are created to ensure reliable power delivery across the chip.

Placement: Standard cells are placed within the core. This includes global placement for rough positioning and detailed placement for precise cell alignment.

Clock Tree Synthesis (CTS): The clock network is constructed using structures such as H-trees or X-trees to minimize clock skew and jitter.

Routing: Interconnections between cells are created using multiple metal layers while avoiding overlaps and congestion.

GDS-II Generation: Design Rule Checks (DRC) are performed, and the final layout is exported as a GDS-II file, which is used by the foundry for chip fabrication.

Throughout this flow, tools such as Yosys, ABC, ioplacer, PDN, RePlAce, TritonCTS, and Magic are used to automate and validate each design stage.
