# Introduction to FPGA computing for the HPC ecosystem

## Field Programmable Gate Array (FPGA) 

![](./images/matrix_fpga.png){ align=right width=300 }
An FPGA (Field-Programmable Gate Array) is an integrated circuit designed to be configured by the user after manufacturing. It consists of an array of programmable logic blocks and a hierarchy of reconfigurable interconnects, allowing users to create custom digital circuits. FPGAs are known for their flexibility, enabling rapid prototyping and implementation of complex functions in hardware, making them suitable for applications in telecommunications, automotive, aerospace, and various other fields where custom and High-Performance Computing is needed.


* FPGAs are a cheaper off-the-shelf alternative
* Grid of configurable logic composed of:
    - Logic Element (LEs) or Adaptive Logic Modules (ALMs)
    - Programmable switches
    - Digital Signal Processing blocks
    - RAM blocks
    - etc …

## Applications
![](./images/applications.png)


## FPGA vendors
![](./images/vendors.png){ align=right width=400 }

* Two major FPGA vendors:
  	- Intel [Altera](https://www.intel.com/content/www/us/en/newsroom/news/intel-launches-altera-standalone-fpga-operation.html#gs.cytki0)
  	- Xillinx [AMD](https://www.amd.com/en/products/adaptive-socs-and-fpgas/fpga.html)

* Intel acquired Altera in 2015

* Xillinx is solely focusing on the FPGA market while Intel is a sum of many parts

* Both profiles are very interesting for heterogeneous computing

* Among the others:
  	- Lattice Semiconductor
  	- QuickLogic
  	- Microchip Technology
  	- Achronix
  	- Efinix



## FPGA cards

FPGA Development Boards and HPC (High-Performance Computing) FPGA Cards serve different purposes and have distinct characteristics:

1. **FPGA Development Boards** are primarily designed for learning, prototyping, and small-scale projects. They typically feature user-friendly interfaces, a variety of I/O options, and often include additional components like sensors, buttons, and displays. These boards are intended for engineers, students, and hobbyists to develop and test FPGA-based designs.

2. **HPC FPGA Cards**, on the other hand, are specialized for High-Performance Computing tasks. These cards are optimized for integration into data centers and High-Performance Computing environments. They focus on maximizing computational power, energy efficiency, and data throughput. HPC FPGA cards are usually designed to be mounted in servers or workstations, and they often support advanced features like high-speed memory interfaces and network connectivity.

!!! tip "Difference Between FPGA Development Boards and HPC FPGA Cards"
    === "FPGA Development Boards"
        * **Purpose**: Primarily used for prototyping, learning, and development purposes.
        * **Design**: These boards typically come with various interfaces (like HDMI, USB, Ethernet) and peripherals (like buttons, LEDs, and sensors) to facilitate easy testing and development.
        * **Flexibility**: They offer a broad range of input/output options to support diverse projects and experiments.
        * **Cost**: Generally more affordable than HPC FPGA cards due to their focus on versatility and accessibility.
        * **Target Audience**: Suitable for students, hobbyists, and engineers working on initial project phases or small-scale applications.
        * **Progranning languages**: VHDL, Verilog, System Verilog.
        * **Specifications**: 
            - Logic Cells: 33,280 
            - Block RAM: 1,800 Kbits
            - External memory: None

        ![](./images/basys-3-0.png)
        

    === "HPC FPGA Cards"
        * **Purpose**: Designed for High-Performance Computing (HPC) applications, focusing on accelerating compute-intensive tasks.
        * **Design**: Typically more powerful, with higher logic capacity, memory, and bandwidth capabilities. They often come with specialized cooling solutions and are designed to be mounted in server racks.
        * **Performance**: Optimized for tasks such as data center operations, machine learning, financial modeling, and large-scale scientific computations.
        * **Cost**: Generally more expensive due to their advanced features and high-performance capabilities.
        * **Target Audience**: Aimed at professionals in industries requiring significant computational power, such as data scientists, researchers, and engineers in High-Performance Computing sectors.
        * **Progranning languages**: <u>HLS</u>: C/C++, python --  <u>HDL</u>: VHDL, Verilog, System Verilog.
        * **Specifications**:
            - Logic Cells: 2,073,000 
            - Block RAM: 239.5 Mb
            - External memory: 16GB HBM2

        ![](https://www.bittware.com/files/520N-MX-800px.svg)

## HDL vs HLS

* <u>**Hardware Description Language**</u> require a more detailed specification of the hardware, providing a gate-level or Register Transfer Level (RTL) description. They require knowledge of the specific hardware constructs, like registers, flip-flops, etc. 

    - <u>Productivity</u>: typically takes more time as developers have to manually describe the low-level hardware details. This can result in more control and optimization but is generally more time-consuming.
    - <u>Flexibility & Optimization</u>: allow developers to describe hardware at a more granular level, there is usually greater opportunity for manual optimization of the design.
    - <u>Learning curve</u> require a deeper understanding of hardware concepts. Thus, there's a steeper learning curve, but it can provide more expertise in hardware design.
    - <u>Use cases</u> is used for more traditional hardware design, where control over implementation details and optimizations is critical.

* <u>**High-Level Synthesis**</u> allows designers to describe hardware using high-level programming languages like C, C++, or SystemC. This means that HLS works at a higher level of abstraction, where developers can describe algorithms or logic without specifying the exact hardware details speeding up design. C/C++ code/kernels are translated to HDL using an offline compiler.  

    - <u>Productivity</u>: offer faster development time since engineers can write code using familiar programming paradigms. Automated synthesis tools then translate the high-level code into RTL, allowing quicker prototyping.
    - <u>Flexibility & Optimization</u>:  can accelerate development but it often provides less control over the final hardware implementation. This might result in less efficient utilization of FPGA resources or higher latency compared to hand-crafted RTL code.
    - <u>Learning curve</u> has a lower learning curve for software engineers or those familiar with C/C++. This makes it more accessible to developers who might not have a hardware background.
    - <u>Use cases</u> is often preferred for algorithm development, data flow designs, and when a software prototype exists that needs to be converted into hardware.


## HLS and Kernel-based programming: from OpenCL to SYCL

### <u>OpenCL: a Low-level API</u>

![](https://www.khronos.org/assets/uploads/apis/2020-opencl-api-overview-2_3.jpg)

* [OpenCL](https://www.khronos.org/opencl/) is widely used throughout the industry

* Kernel-based programming 

* Many silicon vendors ship OpenCL with their processors, including GPUs, DSPs and FPGAs

![](./images/fpga_opencl.png)

### <u>SYCL: a High-level C++ abstraction</u>

![](./images/sycl_desc.png){ align=right width=350 }

* Full coverage for all OpenCL features

* Interop to enable existing OpenCL code with SYCL

* Single-source compilation

* Automatic scheduling of data movement




## Parallelism model for FPGA

* The differences between Instruction Set Architecture (ISA) for CPUs and Spatial Architecture for FPGAs lie in how they process instructions and handle computation:

### 1. **Instruction Set Architecture (ISA) for CPUs:**
   - **Sequential Execution:** CPUs operate using an Instruction Set Architecture (ISA), where a series of instructions (opcodes) are executed sequentially. The CPU fetches, decodes, and executes each instruction in a linear order.
   - **Control Flow Dominated:** CPUs are designed for a wide range of tasks and rely on control flow (e.g., branches, loops) to manage the sequence of operations. They are optimized for tasks with complex control logic.
   - **Fixed Architecture:** The CPU has a fixed architecture, with specific functional units like ALUs (Arithmetic Logic Units), registers, and cache memory. The same hardware is reused for different instructions.
   - **Pipelining and Caching:** CPUs use techniques like pipelining (executing multiple instructions at different stages simultaneously) and caching (storing frequently accessed data) to improve performance.

### 2. **Spatial Architecture for FPGAs:**
   - **Parallel Execution:** FPGAs use spatial architecture, where computation is distributed across a reconfigurable fabric of logic blocks and interconnects. Multiple operations can occur simultaneously in different parts of the FPGA.
   - **Data Flow Dominated:** FPGAs are optimized for data flow processing, where data is passed through a pipeline of operations. This makes them ideal for tasks that benefit from parallelism, like signal processing or machine learning inference.
   - **Customizable Architecture:** The architecture of an FPGA is not fixed; it can be customized by the user to implement specific hardware designs. This allows for the creation of custom data paths and processing units tailored to the task at hand.
   - **No Instruction Set:** Unlike CPUs, FPGAs do not execute instructions in a traditional sense. Instead, they are programmed using hardware description languages (HDLs) like VHDL or Verilog to define how the hardware should behave.

### In a nutshell:
- **ISA for CPUs**: Sequential, control-flow-oriented, with a fixed architecture using a predefined set of instructions. Suitable for general-purpose tasks.
- **Spatial Architecture for FPGAs**: Parallel, data-flow-oriented, with a customizable architecture that can be tailored for specific high-performance tasks. Suitable for specialized, parallelizable workloads.

!!! note "Difference between **Instruction Set** architecture and **Spatial** architecture"
    === "Instruction Set Architecture"
        * Made for general-purpose computation: hardware is constantly reused 
        * Workflow constrained by a set of pre-defined units (Control Units, ALUs, registers)
        * Data/Register size are fixed
        * Different instruction executed in each clock cycle : **temporal** execution  
        ![](./images/isa.png)

    === "Spatial Architecture"
        * Keep only what it needs -- the hardware can be reconfigured
        * Specialize everything by unrolling the hardware: **spatial** execution
        * Each operation uses a different hardware region
        * The design can take more space than the FPGA offers 

        <figure markdown>
        ![](./images/spatial_arch.png){ width=70% }
        </figure>

* The most obvious source of **parallelism** for FPGA is **pipelining** by inserting registers to store each operation output and keep all hardware unit busy. 

* Pipelining parallelism has therefore many stages. 

* If you don't have enough work to fill the pipeline, then the efficiency is very low.

* The authors of the [DPC++ book](https://link.springer.com/book/10.1007/978-1-4842-5574-2) have illustrated it perfectly in Chapter 17.

!!! warning "Vectorization"
    Vectorization is also possible but is not the main source of parallelism but help designing efficient pipeline. Since hardware can be reconfigured at will. The offline compiler can design N-bits Adders, multipliers which simplify greatly vectorization. In fact, the offline compiler vectorizes your design automatically if possible.

## Pipelining for FPGA

!!! abstract "Pipelining (see FPGA Optimization Guide for Intel® oneAPI Toolkits)"
    * Pipelining is a design technique used in synchronous digital circuits to increase maximum frequency (fMAX).
    * This technique involves adding registers to the critical path, reducing the amount of logic between each register.
    * Reducing logic between registers decreases execution time, enabling an increase in fMAX.
    * **The critical path** is the path between two consecutive registers that has the highest latency, meaning it’s where operations take the longest to complete.
    * Pipelining is especially effective for processing a stream of data.
    * In a pipelined circuit, different stages can process different data inputs within the same clock cycle.
    * This design improves data processing throughput.

    ![](./images/pipeline.png)

!!! abstract "Maximum Frequency (fMAX)"
    * The **fMAX** of a digital circuit is its highest possible clock frequency, determining the maximum rate for updating register outputs. 
    * This speed is constrained by the physical propagation delay of the signal across the combinational logic between consecutive register stages.
    * The delay is affected by the complexity of the combinational logic in the path, and the path with the greatest number of logic elements and highest delay sets the speed limit for the entire circuit, often known as the **critical path**. 
    * The fMAX is the reciprocal of this critical path delay, and having a high fMAX is desirable as it leads to better performance when there are no other restrictions.
    ![](./images/fmax.png)

!!! abstract "Throughput"
    * The **Throughput** in a digital circuit refers to the speed at which data is handled.
    * When there are no other limiting factors, a higher fMAX leads to increased throughput, such as more samples per second.
    * Often synonymous with performance, throughput is frequently used to gauge the effectiveness of a circuit.
    ![](./images/throughput.png)

!!! abstract "Latency"
    * The **Latency** measures the duration to complete operations in a digital circuit, and it can be assessed for individual tasks or the whole circuit.
    * It can be measured in time units like microseconds or clock cycles, with the latter often preferred. i
    * Measuring latency in clock cycles separates it from the circuit's clock frequency, making it easier to understand the real effects of modifications on the circuit's performance.
    ![](./images/latency.png)

!!! abstract "Occupancy"
    * The **occupancy** of a datapath at a specific moment signifies the fraction of the datapath filled with valid data.i
    * When looking at a circuit's execution of a program, the occupancy is the mean value from the beginning to the end of the program's run.
    * Parts of the datapath that are unoccupied are commonly called bubbles, akin to a CPU's no-operation (no-ops) instructions, which don't influence the final output.
    * Minimizing these bubbles leads to greater occupancy. If there are no other hindrances, optimizing the occupancy of the datapath will boost throughput.
    <figure markdown>
        ![](./images/occupancy.png)
       <figcaption>Occupancy: 2/5=40%</figcaption>
    </figure>

### Pipelining with ND-range kernels

* ND-range kernels are based on a hierachical grouping of work-items
* A work-item represents a single unit of work 
* Independent simple units of work don't communicate or share data very often
* Useful when porting a GPU kernel to FPGA

<figure markdown>
![](./images/ndrange.png) 
  <figcaption><a href=https://link.springer.com/book/10.1007/978-1-4842-5574-2>DPC++ book</a> -- Figure 17-15 </figcaption>
</figure>

* FPGAs are different from GPU (lots of threads started at the same time)
* Impossible to replicate a hardware for a million of work-items
* Work-items are injected into the pipeline
* A deep pipeline means lots of work-items executing different tasks in parallel

<figure markdown>
![](./images/ndrange_pipeline.png)
  <figcaption><a href=https://link.springer.com/book/10.1007/978-1-4842-5574-2>DPC++ book</a> -- Figure 17-16 </figcaption>
</figure>

### Pipelining with single-work item (loop)

* When your code can't be decomposed into independent works, you can rely on loop parallelism using FPGA
* In such a situation, the pipeline inputs is not work-items but loop iterations
* For single-work-item kernels, the developer does not need to do anything special to preserve the data dependency 
* Communications between kernels is also much easier

<figure markdown>
![](./images/loop_pipeline.png)
  <figcaption><a href=https://link.springer.com/book/10.1007/978-1-4842-5574-2>DPC++ book</a> -- Figure 17-21 </figcaption>
</figure>


* FPGA can efficiently handle loop execution, often maintaining a fully occupied pipeline or providing reports on what changes are necessary to enhance occupancy.
* It's evident that if loop iterations were substituted with work-items, where the value created by one work-item would have to be transferred to another for incremental computation, the algorithm's description would become far more complex.

## MeluXina Bittware 520N-MX FPGAs


<center>
![fpgas](./images/node_fpga.png){align=right width=40%}
</center>


Each of the 20 MeluXina FPGA compute nodes comprise two **BittWare 520N-MX** FPGAs based on the [**Intel Stratix 10 FPGA chip**](https://www.intel.com/content/www/us/en/products/details/fpga/stratix/10/docs.html). Designed for compute acceleration, the 520N-MX are PCIe boards featuring Intel’s Stratix 10 MX2100 FPGA with integrated HBM2 memory. The size and speed of HBM2 (16GB at up to 512GB/s) enables acceleration of memory-bound applications. Programming with high abstraction C, C++, and OpenCLis possible through an specialized board support package (BSP) for the Intel OpenCL SDK. For more details see the dedicated [BittWare product page](https://www.bittware.com/fpga/520n-mx/).

<center>
[![fpgas](images/520N-MX-Block-Diagram-fpgas.svg)](images/520N-MX-Block-Diagram-fpgas.svg){: style="height:250px;width:"}

Intel Stratix 520N-MX Block Diagram.
</center>

The Bittware 520N-MX cards have the following specifications:

1. **FPGA**: Intel Stratix 10 MX with MX2100 in an F2597 package, 16GBytes on-chip High Bandwidth Memory (HBM2) DRAM, 410 GB/s (speed grade 2).
2. Host interface:    x16 Gen3 interface direct to FPGA, connected to PCIe hard IP.
3. Board Management Controller
    * FPGA configuration and control
    * Voltage, current, temperature monitoring
    * Low bandwidth BMC-FPGA comms with SPI link
4. Development Tools
    * Application development: supported design flows - Intel FPGA OpenCL SDK, Intel High-Level Synthesis (C/C++) & Quartus Prime Pro (HDL, Verilog, VHDL, etc.)
    * FPGA development BIST - Built-In Self-Test with source code (pinout, gateware, PCIe driver & host test application)

The FPGA cards are not directly connected to the MeluXina ethernet network. The FPGA compute nodes are linked into the high-speed (infiniband) fabric, and the host code can communicate over this network for distributed/parallel applications.





More details on FPGA can be found in the presentation below:

[![](./images/01-Introduction to FPGA computing for the HPC ecosystem.png)](./pdfs/01-Introduction to FPGA computing for the HPC ecosystem.pdf)
