# FPGA Architecture: Principles and Progression

> FPGA 架构 : 规则和进展

## Abstract

> 摘要

Since their inception more than thirty years ago, field-programmable gate arrays (FPGAs) have been widely used to implement a myriad of applications from different domains.

> 自三十多年前问世以来，现场可编程门阵列(fpga)已被广泛用于实现来自不同领域的无数应用。

As a result of their low-level hardware reconfigurability, FPGAs have much faster design cycles and lower development costs compared to custom-designed chips.

> 由于其低级硬件可重构性，与定制设计的芯片相比，fpga具有更快的设计周期和更低的开发成本。

The design of an FPGA architecture involves many different design choices starting from the high-level architectural parameters down to the transistor-level implementation details, with the goal of making a highly programmable device while minimizing the area and performance cost of reconfigurability.

> FPGA架构的设计涉及许多不同的设计选择，从高级架构参数到晶体管级实现细节，其目标是制造高度可编程的器件，同时最大限度地减少可重构性的面积和性能成本。

As the needs of applications and the capabilities of process technology are constantly evolving, FPGA architecture must also adapt.

> 随着应用需求和工艺技术能力的不断发展，FPGA架构也必须适应。

In this article, we review the evolution of the different key components of modern commercial FPGA architectures and shed the light on their main design principles and implementation challenges

> 在本文中，我们回顾了现代商用FPGA架构的不同关键组件的演变，并阐明了它们的主要设计原则和实现挑战

## Introduction

> 介绍

Field-programmable gate arrays (FPGAs) are reconfigurable computer chips that can be programmed to implement any digital hardware circuit.

> 现场可编程门阵列(fpga)是可重新配置的计算机芯片，可以通过编程来实现任何数字硬件电路。

As depicted in Fig. 1, FPGAs consist of an array of different types of programmable blocks (logic, IO, and others) that can be flexibly interconnected using pre-fabricated routing tracks with programmable switches between them.

> 如图1所示，fpga由一系列不同类型的可编程块(逻辑、IO等)组成，这些可编程块可以使用预制路由轨道灵活地互连，并在它们之间具有可编程开关。

The functionality of all the FPGA blocks and the configuration of the routing switches are controlled using millions of static random access memory (SRAM) cells that are programmed (i.e. written) at runtime to realize a specific function.

> 所有FPGA块的功能和路由开关的配置都使用数百万个静态随机存取存储器(SRAM)单元来控制，这些单元在运行时被编程(即写入)以实现特定功能。

The user describes the desired functionality in a hardware description language (HDL) such as Verilog or VHDL, or possibly uses high-level synthesis to translate C or OpenCL to HDL.

> 用户用硬件描述语言(HDL)描述所需的功能，如Verilog或VHDL，或者可能使用高级合成将C或OpenCL转换为HDL。

The HDL design is then compiled using a complex computer-aided design (CAD) flow into the bitstream file used to program all the FPGA’s configuration SRAM cells.

> 然后使用复杂的计算机辅助设计(CAD)流将HDL设计编译成比特流文件，用于对FPGA的所有配置SRAM单元进行编程。

---

Compared to building a custom application-specific integrated circuit (ASIC), FPGAs have a much lower nonrecurring engineering cost and shorter time-to-market.

> 与定制专用集成电路(ASIC)相比，fpga具有更低的非重复性工程成本和更短的上市时间。

A pre-fabricated off-the-shelf FPGA can be used to implement a complete system in a matter of weeks, skipping the physical design, layout, fabrication, and verification stages that a custom ASIC would normally go through.

> 预制的现成FPGA可用于在几周内实现完整的系统，跳过定制ASIC通常会经历的物理设计，布局，制造和验证阶段。

They also allow continuous hardware upgrades to support new features or fix bugs by simply loading a new bitstream after deployment in-field, thus the name field-programmable.

> 它们还允许持续的硬件升级以支持新功能或通过在现场部署后加载新的比特流来修复错误，因此称为现场可编程。

This makes FPGAs a compelling solution for medium and small volume designs, especially with the fast-paced product cycles in today’s markets.

> 这使得fpga成为中小批量设计的一个令人信服的解决方案，特别是在当今市场快节奏的产品周期中。

The bit-level reconfigurability of FPGAs enables implementation of the exact hardware needed for each application (e.g. datapath bit-width, pipeline stages, number of parallel compute units, memory subsytem, etc.) instead of the fixed one-size-fits-all architecture of general-purpose processors (CPUs) or graphics processing units (GPUs).

> fpga的位级可重构性能够实现每个应用所需的精确硬件(例如，数据路径位宽度，管道阶段，并行计算单元的数量，内存子系统等)，而不是通用处理器(cpu)或图形处理单元(gpu)的固定的通用架构。

Consequently, they can achieve higher efficiency than CPUs or GPUs by implementing instruction-free streaming hardware [1] or a processor overlay with an application-customized pipeline and instruction set [2].

> 因此，它们可以实现比cpu或gpu更高的效率，通过实现无指令流硬件[1]或处理器覆盖与应用程序定制的管道和指令集[2]。

---

These advantages motivated the adoption of FPGAs in many application domains including wireless communi-cations, embedded signal processing, networking, ASIC prototyping, high-frequency trading, and many more [3]–[7].

> 这些优点促使fpga在许多应用领域采用，包括无线通信、嵌入式信号处理、网络、ASIC原型设计、高频交易等[3]-[7]。

They have also been recently deployed on a large scale in datacenters to accelerate search engines [8], packet processing [9], and machine learning [10] workloads, among others.

> 它们最近也被大规模部署在数据中心，以加速搜索引擎[8]、数据包处理[9]和机器学习[10]等工作负载。

However, the flexibility of FPGA hardware comes with an efficiency cost vs. ASICs.

> 然而，与asic相比，FPGA硬件的灵活性带来了效率成本。

Kuon and Rose [11] show that circuits using only the FPGA’s programmable logic blocks average 35× larger and 4× slower than corresponding ASIC implementations.

> Kuon和Rose[11]表明，仅使用FPGA的可编程逻辑块的电路平均比相应的ASIC实现大35倍，慢4倍。

A more recent study [12] shows that for full-featured designs which heavily utilize the other FPGA blocks (e.g. RAMs and DSPs), this area gap is reduced but is still 9×.

> 最近的一项研究[12]表明，对于大量利用其他FPGA块(例如ram和dsp)的全功能设计，该面积差距减少了，但仍然是9倍。

FPGA architects seek to reduce this efficiency gap as much as possible while maintaining the programmability that makes FPGAs useful across a wide range of applications.

> FPGA架构师试图尽可能地减少这种效率差距，同时保持可编程性，使FPGA在广泛的应用中有用。

---

In this article, we introduce key principles of FPGA architecture, and highlight the progression of these devices over the past 30 years.

> 在本文中，我们介绍了FPGA架构的关键原理，并重点介绍了这些器件在过去30年中取得的进展。

Fig. 1 shows how FPGAs evolved from simple arrays of programmable logic and IO blocks to complex heterogeneous multi-die systems with embedded block RAMs, digital signal processing (DSP) blocks, processor subsystems, diverse high-performance external interfaces, system-level interconnect, and more.

> 图1显示了fpga如何从简单的可编程逻辑和IO模块阵列演变为具有嵌入式块ram、数字信号处理(DSP)模块、处理器子系统、各种高性能外部接口、系统级互连等的复杂异构多模系统。

First, we give a brief overview of the CAD flows and methodology used to evaluate new FPGA architecture ideas.

> 首先，我们简要概述了用于评估新的FPGA架构思想的CAD流程和方法。

We then detail the architecture challenges and design principles for each of the key components of an FPGA.

> 然后，我们详细介绍了FPGA每个关键组件的架构挑战和设计原则。

We highlight key innovations in the design and implementation of each of these components over the past three decades along with areas of ongoing research.

> 我们重点介绍了过去三十年来这些组件在设计和实现方面的关键创新以及正在进行的研究领域。

## FPGA Architecture Evaluation

> FPGA 架构评估

As shown in Fig. 2, the FPGA architecture evaluation flow consists of three main components: a suite of benchmark applications, an architecture model, and a CAD system.

> 如图2所示，FPGA架构评估流程由三个主要部分组成:一套基准测试应用程序、一个架构模型和一个CAD系统。

Unlike an ASIC built for a specific functionality, an FPGA is a general-purpose platform designed for many use cases, some of which may not even exist when the FPGA is architected.

> 与为特定功能构建的ASIC不同，FPGA是为许多用例设计的通用平台，其中一些用例在FPGA架构时甚至不存在。

Therefore, an FPGA architecture is evalu-ated based on its efficiency when implementing a wide variety of benchmark designs that are representative of the key FPGA markets and application domains.

> 因此，在实现各种代表关键FPGA市场和应用领域的基准设计时，基于FPGA架构的效率进行评估。

Typically, each FPGA vendor has a carefully selected set of bench-mark designs collected from proprietary system imple-mentations and various customer applications.

> 通常，每个FPGA供应商都有一组精心挑选的基准设计，这些设计来自专有系统实现和各种客户应用程序。

There are also several open-source benchmark suites such as the classic MCNC20 [13], the VTR [14], and the Titan23 [15] suites which are commonly used in academic FPGA archi-tecture and CAD research.

> 还有一些开源基准套件，如经典的MCNC20 [13]， VTR[14]和Titan23[15]套件，这些套件通常用于学术FPGA架构和CAD研究。

While early academic FPGA re-search used the MCNC suite of designs, these circuits are now too small (thousands of logic primitives) and simple (only IOs and logic) to represent modern FPGA use cases.

> 虽然早期的FPGA学术研究使用了MCNC设计套件，但这些电路现在太小(数千个逻辑原语)且简单(只有IOs和逻辑)，无法代表现代FPGA用例。

The VTR and particularly the Titan suite are larger and more complex, making them more representative, but as FPGA capacity and application complexity continues to grow new benchmark suites are regularly needed.

> VTR，特别是Titan套件更大更复杂，使它们更具代表性，但随着FPGA容量和应用程序复杂性的不断增长，经常需要新的基准套件。

---

The second part of the evaluation flow is the FPGA ar-chitecture model.

> 评估流程的第二部分是FPGA架构模型。

The design of an FPGA involves many different decisions from architecture-level organization (e.g. number and type of blocks, distribution of wire seg-ment lengths, size of logic clusters and logic elements) down to transistor-level circuit implementation (e.g. pro-grammable switch type, routing buffer transistor sizing, register implementation).

> FPGA的设计涉及许多不同的决策，从架构级组织(例如，块的数量和类型，线段长度的分布，逻辑簇和逻辑元件的大小)到晶体管级电路实现(例如，可编程开关类型，路由缓冲晶体管尺寸，寄存器实现)。

It also involves different imple-mentation styles; the logic blocks and programmable routing are designed and laid out as full-custom circuits, while most hardened blocks (e.g. DSPs) mix standard-cell and full-custom design for the block core and peripher-als, respectively.

> 它还涉及到不同的实现风格;逻辑块和可编程路由被设计和布局为全定制电路，而大多数硬化块(例如dsp)分别混合了标准单元和全定制设计的块核心和外设。

Some blocks (RAM, IO) even include sig-nificant analog circuitry.

> 一些块(RAM, IO)甚至包括重要的模拟电路。

All these different components need to be carefully modeled to evaluate the FPGA archi-tecture in its entirety.

> 所有这些不同的组件都需要仔细建模，以全面评估FPGA架构。

This is typically captured using an architecture description file that specifies the organiza-tion and types of the different FPGA blocks and the rout-ing architecture, in addition to area, timing and power models obtained from circuit-level implementations for each of these components.

> 这通常是使用架构描述文件捕获的，该文件指定了不同FPGA块和路由架构的组织和类型，以及从每个这些组件的电路级实现中获得的面积、时序和功率模型。

---

Finally, a re-targetable CAD system such as VTR [14] is used to map the selected benchmark applications on the specified FPGA architecture.

> 最后，使用可重新定位的CAD系统(如VTR[14])将选定的基准测试应用映射到指定的FPGA架构上。

Such a CAD system consists of a sequence of complex optimization algorithms that synthesizes a benchmark written in an HDL into a circuit netlist, maps it to the different FPGA blocks, places the mapped blocks at specific locations on the FPGA, and routes the connections between them using the specified programmable routing architecture.

> 这样的CAD系统由一系列复杂的优化算法组成，这些算法将用HDL编写的基准合成为电路网表，将其映射到不同的FPGA块，将映射的块放置在FPGA上的特定位置，并使用指定的可编程路由架构路由它们之间的连接。

The implementation produced by the CAD system is then used to evaluate several key metrics.

> 由CAD系统产生的实现，然后用于评估几个关键指标。

Total area is the sum of the areas of the FPGA blocks used by the application, along with the programmable routing included with them.

> 总面积是应用程序使用的FPGA块面积的总和，以及其中包含的可编程路由。

A timing analyzer finds the critical path(s) through the blocks and routing to determine the maximum frequencies of the application’s clock(s).

> 时序分析仪通过块和路由查找关键路径，以确定应用程序时钟的最大频率。

Power consumption is estimated based on resources used and signal toggle rates.

> 功耗是根据使用的资源和信号切换率估计的。

FPGAs are never designed for only one application, so these metrics are averaged across all the benchmarks.

> fpga从来都不是为一个应用程序设计的，所以这些指标在所有基准测试中都是平均的。

Finally, the overall evaluation blends these average area, delay, and power metrics appropriately depending on the archi-tecture goal (e.g. high performance or low power).

> 最后，总体评估根据架构目标(例如高性能或低功耗)适当地混合这些平均面积、延迟和功耗指标。

Other metrics such as CAD tool runtime and whether or not the CAD tools fail to route some benchmarks on an architec-ture are also often considered

> 其他指标，如CAD工具运行时，以及CAD工具是否不能在体系结构上路由一些基准，也经常被考虑

---

As an example, a key set of questions in FPGA architecture is: What functionality should be hardened (i.e. implemented as a new ASIC-style block) in the FPGA architecture? How flexible should this block be? How much of the FPGA die area should be dedicated to it? Ideally, an FPGA architect would like the hardened functionality to be usable by as many applications as possible at the least possible silicon cost.

> 例如，FPGA架构中的一组关键问题是:在FPGA架构中应该加强哪些功能(即作为新的asic风格块实现)?这个块应该有多灵活?有多少FPGA芯片面积应该专门用于它?理想情况下，FPGA架构师希望能够以尽可能低的硅成本为尽可能多的应用程序提供强化功能。

An application that can make use of the hard block will benefit by being smaller, faster and more power-efficient than when implemented solely in the programmable fabric.

> 与仅在可编程结构中实现相比，可以利用硬块的应用程序将受益于更小、更快和更节能。

This motivates having more programmability in the hard block to capture more use cases; however, higher flexibility generally comes at the cost of larger area and reduced efficiency of the hard block.

> 这促使在硬块中具有更多的可编程性，以捕获更多的用例;然而，更高的灵活性通常是以更大的面积和降低的硬块效率为代价的。

On the other hand, if a hard block is not usable by an application circuit, its silicon area is wasted; the FPGA user would rather have more of the usable general-purpose logic blocks in the area of the unused hard block.

> 另一方面，如果一个硬块不能被应用电路使用，它的硅面积就被浪费了;FPGA用户希望在未使用的硬块区域中有更多可用的通用逻辑块。

The impact of this new hard block on the programmable routing must also be considered—does it need more inter-connect or lead to slow routing paths to and from the block? To evaluate whether a specific functionality should be hard-ened or not, both the cost and gain of hardening it have to be quantified empirically using the flow described in this section.

> 这种新的硬块对可编程路由的影响也必须考虑——它是否需要更多的互连，还是导致往返块的路由路径变慢?为了评估一个特定的功能是否应该加固，加固的成本和收益都必须使用本节中描述的流程进行量化。

FPGA architects may try many ideas before landing on the right combination of design choices that adds just the right amount of programmability in the right spots to make this new hard block a net win.

> FPGA架构师可能会尝试许多想法，然后才能找到合适的设计选择组合，在合适的位置添加适量的可编程性，从而使这个新的硬块成为最终的赢家。

---

In the following section, we detail many different components of FPGAs and key architecture questions for each.

> 在下一节中，我们将详细介绍fpga的许多不同组件以及每个组件的关键架构问题。

While we describe the key results without detailing the experimental methodology used to find them, in general they came from a holistic architecture evaluation flow similar to that in Fig. 2

> 虽然我们描述了关键结果，但没有详细说明用于找到它们的实验方法，但通常它们来自于与图2类似的整体架构评估流程

## FPGA Architecture Evolution

> FPGA 架构演变

### A. Programmable Logic

> 可编程逻辑

The earliest reconfigurable computing devices were programmable array logic (PAL) architectures.

> 最早的可重构计算设备是可编程阵列逻辑(PAL)架构。

PALs consisted of an array of and gates feeding another array of or gates, as shown in Fig. 3, and could implement any Boolean logic expression as a two-level sum-of-products function.

> 如图3所示，PALs由一组“和”门组成，为另一组“和”门提供能量，并且可以将任何布尔逻辑表达式实现为两级积和函数。

PALs achieve configurability through programmable switches that select the inputs to each of the and/or gates to implement different Boolean expressions.

> pal通过可编程开关实现可配置性，可编程开关选择每个和/或门的输入，以实现不同的布尔表达式。

The design tools for PALs were very simple since the delay through the device is constant no matter what logic function is implemented.

> pal的设计工具非常简单，因为无论实现什么逻辑功能，通过器件的延迟都是恒定的。

However, PALs do not scale well; as device logic capacity increased, the wires forming the and/or arrays became increasingly longer and slower and the number of programmable switches required grew quadratically.

> 然而，pal不能很好地扩展;随着器件逻辑容量的增加，构成和/或阵列的导线变得越来越长、越来越慢，所需的可编程开关数量呈二次增长。

---

Subsequently, complex programmable logic devices (CPLDs) kept the and/or arrays as the basic logic elements, but attempted to solve the scalability challenge by integrating multiple PALs on the same die with a crossbar interconnect between them at the cost of more complicated design tools.

> 随后，复杂可编程逻辑器件(cpld)将和/或阵列作为基本逻辑元件，但试图通过在同一芯片上集成多个pal，并在它们之间使用交叉棒互连来解决可扩展性的挑战，这是以更复杂的设计工具为代价的。

Shortly after, Xilinx pioneered the first lookup-table-based (LUT-based) FPGA in 1984, which consisted of an array of SRAM-based LUTs with programmable interconnect between them.

> 不久之后，Xilinx在1984年率先推出了第一个基于查找表(基于lut)的FPGA，该FPGA由一系列基于sram的lut组成，它们之间具有可编程的互连。

This style of reconfigurable devices was shown to scale very well, with LUTs achieving much higher area efficiency compared to the and/or logic in PALs and CPLDs.

> 这种可重构器件的可扩展性非常好，与pal和cpld中的和/或逻辑相比，lut实现了更高的面积效率。

Consequently, LUT-based architectures became increasingly dominant and today LUTs form the fundamental logic element in all commercial FPGAs.

> 因此，基于lut的架构变得越来越占主导地位，今天lut形成了所有商用fpga的基本逻辑元件。

Several research attempts [16]–[18] investigated replacing LUTs with a different form of configurable and gates: a full binary tree of and gates with programmable output/input inversion known as an and-inverter cone (AIC).

> 一些研究尝试[16]-[18]研究了用不同形式的可配置和门替换lut:具有可编程输出/输入反转的和门的完整二叉树，称为和逆变锥(AIC)。

However, when thoroughly evaluated in [19], AIC-based FPGA architectures had significantly larger area than LUT-based ones, with delay gains only on small benchmarks that have short critical paths.

> 然而，当在[19]中进行全面评估时，基于aic的FPGA架构的面积明显大于基于lut的架构，延迟增益仅在具有短关键路径的小型基准测试上。

---

A K-LUT can implement any K-input Boolean function by storing its truth table in configuration SRAM cells.

> K-LUT可以通过将其真值表存储在配置SRAM单元中来实现任何k输入布尔函数。

K input signals are used as multiplexer select lines to choose an output from the 2^K values of the truth table.

> K个输入信号用作多路选择线，从真值表的2^K值中选择一个输出。

Fig. 4(a) shows the transistor-level circuit implementation of a 4-LUT using pass-transistor logic.

> 图4(a)显示了使用通管逻辑的4- lut的晶体管级电路实现。

In addition to the output buffer, an internal buffering stage (shown between the second and third stages of the LUT in Fig. 4(a)) is typically implemented to mitigate the quadratic increase in delay when passing through a chain of pass-transistors.

> 除了输出缓冲器之外，通常还实现一个内部缓冲级(如图4(a)中LUT的第二和第三级之间)，以减轻通过通管链时延迟的二次增长。

The sizing of the LUT’s pass-transistors and the internal/output buffers is carefully tuned to achieve the best area-delay product.

> LUT的通路晶体管和内部/输出缓冲器的尺寸经过仔细调整，以实现最佳的区域延迟产品。

Classic FPGA literature [20] defines the basic logic element (BLE) as a K-LUT coupled with an output register and bypassing 2:1 multiplexers as shown in Fig. 4(c).

> 经典FPGA文献[20]将基本逻辑元件(BLE)定义为与输出寄存器耦合的K-LUT，并绕过2:1多路复用器，如图4(c)所示。

Thus, a BLE can either implement just a flip-flop (FF) or a K-LUT with registered or unregistered output.

> 因此，BLE既可以实现触发器(FF)，也可以实现具有注册输出或未注册输出的K-LUT。

As illustrated in Fig. 4(d), BLEs are typically clustered in logic blocks (LBs), such that an LB contains N BLEs along with local interconnect.

> 如图4(d)所示，ble通常聚集在逻辑块(LB)中，这样一个LB包含N个ble以及本地互连。

The local interconnect in the logic block consists of multiplexers between signal sources (BLE outputs and logic block inputs) and destinations (BLE inputs).

> 逻辑块中的本地互连由信号源(BLE输出和逻辑块输入)和目的(BLE输入)之间的多路复用器组成。

These multiplexers are often arranged to form a local full [21] or partial [22] crossbar.

> 这些多路复用器通常被布置成形成局部全交叉[21]或部分交叉[22]。

At the circuit level, these multiplexers are usually built as two levels of pass transistors, followed by a two-stage buffer as shown in Fig. 4(b); this is the most efficient circuit design for FPGA multiplexers in most cases [23].

> 在电路层面，这些多路复用器通常被构建为两级通路晶体管，然后是一个两级缓冲器，如图4(b)所示;在大多数情况下，这是FPGA多路复用器最有效的电路设计[23]。

Fig. 4(d) also shows the switch and connection block multiplexers forming the programmable routing that allows logic blocks to connect to each other; this routing is discussed in detail in Section III-B.

> 图4(d)还示出形成允许逻辑块彼此连接的可编程路由的开关和连接块多路复用器;此路由在第III-B节中有详细讨论。

---

Over the years, the size of both LUTs (K) and LBs (N) have gradually increased as device logic capacity has grown.

> 多年来，随着器件逻辑容量的增长，lut (K)和lb (N)的大小都在逐渐增加。

As K increases, more functionality can be packed into a single LUT, reducing not only the number of LUTs needed but also the number of logic levels on the critical path, which increases performance.

> 随着K的增加，可以将更多的功能打包到单个LUT中，这不仅减少了所需LUT的数量，还减少了关键路径上的逻辑级别数量，从而提高了性能。

In addition, the demand for inter-LB routing decreases as more connections are captured into the fast local intercon-nect by increasing N.

> 此外，随着N的增加，更多的连接被捕获到快速的本地互连中，对lb间路由的需求也会减少。

On the other hand, the area of the LUT increases exponentially with K (due to the 2K SRAM cells) and its speed degrades linearly (as the multiplexer constitutes a chain of K pass transistors with periodic buffering).

> 另一方面，LUT的面积随K呈指数增长(由于2K SRAM单元)，其速度线性下降(因为多路复用器构成具有周期性缓冲的K通晶体管链)。

If the LB local interconnect is implemented as a crossbar, its size increases quadratically and its speed degrades linearly with the number of BLEs in the LB, N.

> 如果LB本地互连采用交叉互连方式，则随着LB中LB的数量N，其大小呈二次增长，速度呈线性下降。

Ahmed and Rose [24] empirically evaluated these trade-offs and concluded that LUTs of size 4–6 and LBs of size 3–10 BLEs offer the best area-delay product for an FPGA architecture, with 4-LUTs leading to a better area but 6-LUTs yielding a higher speed.

> Ahmed和Rose[24]经验性地评估了这些权衡，并得出结论，大小为4-6的lut和大小为3-10的lb为FPGA架构提供了最佳的区域延迟产品，4- lut可以带来更好的面积，但6- lut可以产生更高的速度。

Historically, the first LUT-based FPGA from Xilinx, the XC2000 series in 1984, had an LB that contained only two 3-LUTs (i.e. N = 2, K = 3 ).

> 从历史上看，赛灵思的第一个基于lut的FPGA，即1984年的XC2000系列，其LB仅包含两个3- lut(即N = 2, K = 3)。

LB size gradually increased over time and by 1999, Xilinx’s Virtex family included four 4-LUTs and Altera’s Apex 20K family included ten 4-LUTs in each LB.

> 随着时间的推移，LB尺寸逐渐增加，到1999年，Xilinx的Virtex系列包括4个4- lut, Altera的Apex 20K系列在每个LB中包括10个4- lut。

---

The next major change in architecture came in 2003 from Altera, with the introduction of fracturable LUTs in their Stratix II architecture [25].

> 架构的下一个重大变化出现在2003年，Altera在其Stratix II架构中引入了可断裂lut[25]。

Ahmed and Rose in [24] showed that an LB with ten 6-LUTs achieved 14% higher performance than a LB with ten 4-LUTs, but at a 17% higher area.

> Ahmed和Rose在[24]中表明，具有10个6- lut的LB比具有10个4- lut的LB的性能高14%，但面积高17%。

Fracturable LUTs seek to combine the best of both worlds, achieving the performance of a larger LUT with the area-efficiency of smaller LUTs.

> 可压裂LUT寻求将两者的优点结合起来，实现更大LUT的性能和更小LUT的面积效率。

A major factor in the area increase with traditional 6-LUTs is under-utilization: Lewis et al. found that 64% of the LUTs in benchmark applications used fewer than 6 inputs, wasting some of a 6-LUT’s functionality [26].

> 传统6- lut面积增加的一个主要因素是利用率不足:Lewis等人发现，基准应用程序中64%的lut使用少于6个输入，浪费了6- lut的一些功能[26]。

A fracturable {K, M}-LUT can be configured as a single LUT of size K or can be fractured into two LUTs of size up to K – 1 that collectively use no more than K + M distinct inputs.

> 一个可断裂的{K, M}-LUT可以被配置为大小为K的单个LUT，也可以被分割成两个大小不超过K - 1的LUT，它们总共使用不超过K + M个不同的输入。

Fig. 5(a) shows that a 6-LUT is internally composed of two 5-LUTs plus a 2:1 multiplexer.

> 图5(a)示出6-LUT内部由两个5- lut加一个2:1多路复用器组成。

Consequently, almost no circuitry (only the red added output) is necessary to allow a 6-LUT to instead operate as two 5-LUTs that share the same inputs.

> 因此，几乎没有电路(只有红色添加的输出)是必要的，以允许6-LUT而不是作为两个5- lut，共享相同的输入操作。

However, requiring the two 5-LUTs to share all their inputs will limit how often both can be simultaneously used.

> 然而，要求两个5- lut共享其所有输入将限制两者同时使用的频率。

Adding extra routing ports as shown in Fig. 5(b) increases the area of the fracturable 6-LUT, but makes it easier to find two logic functions that can be packed together into it.

> 如图5(b)所示，增加额外的路由端口增加了可断裂的6-LUT的面积，但更容易找到两个可以打包在一起的逻辑功能。

The adaptive logic module (ALM) in the Stratix II architecture implemented a {6, 2}-LUT that had 8 input and 2 output ports.

> Stratix II架构中的自适应逻辑模块(ALM)实现了具有8个输入和2个输出端口的{6,2}-LUT。

Thus, an ALM can implement a 6-LUT or two 5-LUTs sharing 2 inputs (and therefore a total of 8 distinct inputs).

> 因此，ALM可以实现一个6-LUT或两个共享2个输入的5- lut(因此总共有8个不同的输入)。

Pairs of smaller LUTs could also be implemented without any shared inputs, such as two 4-LUTs or one 5-LUT and one 3-LUT.

> 对较小的lut也可以在没有任何共享输入的情况下实现，例如两个4- lut或一个5-LUT和一个3-LUT。

With a frac-turable 6-LUT, larger logic functions are implemented in 6-LUTs reducing the logic levels on the critical path and achieving performance improvement.

> 使用可断裂的6-LUT，可以在6-LUT中实现更大的逻辑功能，从而降低关键路径上的逻辑级别并实现性能改进。

On the other hand, smaller logic functions can be packed together (each using only half an ALM), improving area-efficiency.

> 另一方面，更小的逻辑功能可以封装在一起(每个只使用半个ALM)，提高了面积效率。

The LB in Stratix II not only increased the performance by 15%, but also reduced the logic and routing area by 2.6% compared to a baseline 4-LUT-based LB [26].

> 与基于4- lut的基准LB相比，Stratix II中的LB不仅提高了15%的性能，而且减少了2.6%的逻辑和路由面积[26]。

---

Xilinx later adopted a related fracturable LUT ap-proach in their Virtex-5 architecture.

> Xilinx后来在他们的Virtex-5架构中采用了一种相关的可断裂LUT方法。

Like Stratix II, a Virtex-5 6-LUT can be decomposed into two 5-LUTs.

> 与Stratix II一样，Virtex-5 6-LUT可以分解为两个5- lut。

How-ever, Xilinx chose to minimize the extra circuitry added for fracturability as shown in Fig. 5(a)—no extra input routing ports or steering multiplexers are added.

> 然而，如图5(a)所示，Xilinx选择将增加的额外电路最小化——没有增加额外的输入路由端口或转向多路复用器。

This results in a lower area per fracturable LUT, but makes it more difficult to pack two smaller LUTs together as they must use no more than 5 distinct inputs [27].

> 这导致每个可压裂LUT的面积更小，但使两个较小的LUT组合在一起变得更加困难，因为它们必须使用不超过5个不同的输入[27]。

While sub-sequent architectures from both Altera/Intel and Xilinx have also been based on fracturable 6-LUTs, a recent Mi-crosemi study [28] revisited the 4-LUT vs. 6-LUT efficien-cy trade-off for newer process technologies, CAD tools and designs than those used in [24].

> 虽然Altera/Intel和Xilinx的后续架构也基于可断裂的6-LUT，但最近Mi-crosemi的一项研究[28]重新审视了4-LUT与6-LUT的效率权衡，以采用比[24]中使用的新工艺技术、CAD工具和设计。

It shows that a LUT structure with two tightly coupled 4-LUTs, one feeding the other, can achieve performance close to plain 6-LUTs along with the area and power advantages of 4-LUTs.

> 结果表明，两个紧密耦合的4-LUT相互馈送的LUT结构可以获得接近普通6-LUT的性能，同时具有4-LUT的面积和功率优势。

In terms of LB size, FPGA architectures from Altera/Intel and Xilinx converged on the use of relatively large LBs with ten and eight BLEs respectively, for several genera-tions.

> 在LB尺寸方面，来自Altera/Intel和Xilinx的FPGA架构在使用相对较大的LB方面进行了几代融合，分别为10个和8个LB。

However, the recently announced Versal architec-ture from Xilinx further increases the number of BLEs per LB to thirty two [29].

> 然而，赛灵思最近宣布的Versal架构进一步将每LB的ble数量增加到32个[29]。

The reasons for this large increase are two-fold.

> 这种大幅增长的原因有两个方面。

First, inter-LB wire delay is scaling poorly with process shrinks, so capturing more connections within an LB’s local routing is increasingly beneficial.

> 首先，随着进程的缩小，LB间的线延迟的可伸缩性很差，因此在LB的本地路由中捕获更多的连接越来越有益。

Second, ever-larger FPGA designs tend to increase CAD tool runtime, but larger LBs can help mitigate this trend by simplifying placement and inter-LB routing.

> 其次，越来越大的FPGA设计往往会增加CAD工具的运行时间，但更大的lb可以通过简化放置和lb间路由来帮助缓解这种趋势。

---

Another important architecture choice is the number of FFs per BLE.

> 另一个重要的架构选择是每个BLE的ff数量。

Early FPGAs coupled a (non-fracturable) LUT with a single FF as shown in Fig. 4(c).

> 早期的fpga将(不可断裂的)LUT与单个FF耦合在一起，如图4(c)所示。

When they moved to fracturable LUTs, both Altera/Intel and Xilinx architectures added a second FF to each BLE so that both outputs of the fractured LUT could be registered as shown in Fig. 5(a) and 5(b).

> 当他们转移到可断裂LUT时，Altera/Intel和Xilinx架构都在每个BLE上添加了第二个FF，以便可以记录断裂LUT的两个输出，如图5(a)和5(b)所示。

In the Stratix V architecture, the number of FFs was further increased from two to four per BLE in order to accommodate increased demand for FFs as designs became more deeply pipelined to achieve higher performance [30].

> 在Stratix V架构中，每个BLE的FFs数量进一步从2个增加到4个，以适应随着设计更加深入流水线化以实现更高性能而增加的对FFs的需求[30]。

Low-cost multiplexing circuitry allows sharing the existing inputs between the LUTs and FFs to avoid adding more costly routing ports.

> 低成本的多路复用电路允许在lut和ff之间共享现有输入，以避免增加更昂贵的路由端口。

Stratix V also implements FFs as pulse latches instead of edge-triggered FFs.

> Stratix V还将FFs实现为脉冲锁存器，而不是边缘触发FFs。

As shown in Fig. 6(b), this removes one of the two latches that would be present in a master-slave FF (Fig. 6(a)), reducing the register delay and area.

> 如图6(b)所示，这消除了主从FF中存在的两个锁存器中的一个(图6(a))，减少了寄存器延迟和面积。

A pulse latch acts as a cheaper FF with worse hold time as it latches the data input during a very short pulse instead of a clock edge as in conventional FFs.

> 脉冲锁存器作为一个更便宜的FF，但保持时间更差，因为它在一个非常短的脉冲期间锁存数据输入，而不是像传统FF那样的时钟边缘。

If a pulse genera-tor was built for each FF, the overall area per FF would increase rather than decrease.

> 如果为每个FF建立一个脉冲发生器，则每个FF的总面积将增加而不是减少。

Instead, Stratix V contains only two configurable pulse generators per LB; each of the 40 pulse latches in an LB selects which generator provides its pulse input.

> 相反，Stratix V每LB只包含两个可配置的脉冲发生器;LB中的40个脉冲锁存器中的每一个都选择哪个发生器提供其脉冲输入。

The FPGA CAD tools can also program the pulse width in these generators, allowing a limited amount of time borrowing between source and destination registers.

> FPGA CAD工具还可以对这些发生器中的脉冲宽度进行编程，从而允许在源寄存器和目标寄存器之间借用有限的时间。

Longer pulses further degrade hold time, but generally any hold violations can be solved by the FPGA routing algorithm using longer wiring paths to delay signals.

> 较长的脉冲会进一步降低保持时间，但通常情况下，任何保持违规都可以通过使用较长的布线路径来延迟信号的FPGA路由算法来解决。

Xilinx also uses pulse latches as its FFs in its Ultrascale+ architecture [31].

> Xilinx在其Ultrascale+架构中也使用脉冲锁存器作为其ff[31]。

---

Arithmetic operations (add and subtract) are very common in FPGA designs: Murray et al. found that 22% of the logic elements in a suite of FPGA designs were implementing arithmetic [32].

> 算术运算(加减运算)在FPGA设计中非常常见:Murray等人发现，一套FPGA设计中有22%的逻辑元件实现了算术运算[32]。

While these operations can be implemented with LUTs, each bit of arithmetic in a ripple carry adder requires two LUTs (one for the sum output and one for the carry).

> 虽然这些操作可以用lut实现，但纹波进位加法器中的每个算术位都需要两个lut(一个用于求和输出，一个用于进位输出)。

This leads to both high logic utilization and a slow critical path due to connecting many LUTs in series to compute carries for multi-bit additions.

> 这将导致高逻辑利用率和缓慢的关键路径，因为将许多lut串联连接到用于多位添加的计算载体。

Consequently, all modern FPGA architectures include hardened arithmetic circuitry in their logic blocks.

> 因此，所有现代FPGA架构都在其逻辑块中包含强化的算术电路。

There are many variants, but all have several common points.

> 有很多变体，但都有几个共同点。

First, to avoid adding expensive routing ports, the arithmetic circuits re-use the LUT routing ports or are fed by the LUT outputs.

> 首先，为了避免添加昂贵的路由端口，算术电路重用LUT路由端口或由LUT输出提供。

Second, the carry bits are propagated on special, dedicated interconnect with little or no programmability so that the crucial carry path is fast.

> 其次，进位在特殊的专用互连上传播，具有很少或没有可编程性，因此关键的进位路径是快速的。

The lowest cost arithmetic circuitry hardens ripple carry structures and achieves a large speed gain over LUTs (3.4× for a 32-bit adder in [32]).

> 成本最低的算术电路可以硬化纹波进位结构，并在lut上实现较大的速度增益([32]中32位加法器的速度增益为3.4倍)。

Hardening more sophisticated structures like carry skip adders further improves speed (an additional 20% speed-up at 32-bits in [33]).

> 强化更复杂的结构，如进位跳加器，进一步提高了速度(在[33]中32位时额外提高了20%的速度)。

The latest Versal architecture from Xilinx hardens the carry logic for 8-bit carry look-ahead adders (i.e. the addition can only start on every eighth BLE), while the sum, propagate and generate logic is all implemented in the fracturable 6-LUTs feeding the carry logic as shown in Fig. 7(a) [29].

> 赛灵思最新的Versal架构强化了8位进位前瞻加法器的进位逻辑(即加法只能在每8个BLE开始)，而求和、传播和生成逻辑都是在可断裂的6- lut中实现的，如图7(a)所示[29]。

This organization allows implementing 1-bit of arithmetic per logic element.

> 这种组织允许每个逻辑元素实现1位算术。

On the other hand, the latest Intel Agilex architecture can implement 2-bits of arithmetic per logic element, with dedicated interconnect for the carry between logic elements as shown in Fig. 7(b).

> 另一方面，最新的英特尔Agilex架构可以实现每个逻辑元件2位运算，逻辑元件之间的进位具有专用互连，如图7(b)所示。

It achieves that by hardening 2-bit carry-skip adders that are fed by the four 4-LUTs contained within a 6-LUT [34].

> 它通过强化由6-LUT中包含的四个4- lut馈送的2位进位跳加器来实现这一点[34]。

The study by Murray et al. [32] shows that the combination of fracturable LUTs and 2 bits of arithmetic (similar to that adopted in Altera/Intel FPGAs) is particularly efficient compared to architectures with non-fracturable LUTs or 1 bit of arithmetic per logic element.

> Murray等人的研究[32]表明，与不可断裂lut或每个逻辑元件1位算术的架构相比，可断裂lut和2位算术的组合(类似于Altera/Intel fpga中采用的算法)特别高效。

It also concludes that having dedicated arithmetic circuits (i.e. hardening adders and carry chains) inside the FPGA logic elements increases average performance by 75% and 15% for arithmetic microbenchmarks and general benchmark circuits, respectively.

> 它还得出结论，在FPGA逻辑元件中有专用的算术电路(即硬化加法器和进位链)，算术微基准和一般基准电路的平均性能分别提高了75%和15%。

---

Recently, deep learning (DL) has become a key work-load in many end-user applications, with its core opera-tion being multiply-accumulate (MAC).

> 近年来，深度学习(DL)已成为许多终端用户应用的关键工作负载，其核心操作是乘法累加(MAC)。

Generally, MACs can be implemented in DSP blocks as will be described in Section III-E; however low-precision MACs with 8-bit or narrower operands (which are becoming increasingly popular in DL workloads) can also be implemented ef-ficiently in the programmable logic [9].

> 一般来说，mac可以在DSP块中实现，如第III-E节所述;然而，具有8位或更窄操作数的低精度mac(在DL工作负载中越来越流行)也可以在可编程逻辑中高效实现[9]。

LUTs are used to generate the partial products of a multiplier array fol-lowed by an adder tree to reduce the partial products and perform the accumulation.

> lut用于生成乘法器数组的部分乘积，然后使用加法器树来减少部分乘积并执行累加。

Consequently, multiple recent studies [35]–[37] have investigated increasing the density of hardened adders in the FPGA’s logic fabric to enhance its performance when implementing arithmetic-heavy applications such as DL acceleration.

> 因此，最近的多项研究[35]-[37]研究了在FPGA的逻辑结构中增加硬化加法器的密度，以提高其在实现算术繁重的应用(如DL加速)时的性能。

The work in [36] and [37] proposed multiple different logic block architectures that incorporate 4 bits of arithmetic per logic element arranged in one or two carry chains with different configurations, instead of just 2 bits of arithmetic in an Intel Stratix-like ALM.

> [36]和[37]中的工作提出了多种不同的逻辑块架构，其中每个逻辑元素包含4位算术，排列在一个或两个具有不同配置的进位链中，而不是在类似Intel stratix的ALM中仅包含2位算术。

These proposals do not require increas-ing the number of the (relatively expensive) routing ports in the logic clusters when implementing multiplications due to the high degree of input sharing in a multiplier ar-ray (i.e. for an N-bit multiplier, only 2 N inputs are needed to generate N2 partial products).

> 这些建议在实现乘法时不需要增加逻辑集群中(相对昂贵的)路由端口的数量，因为乘法器ar射线中的输入共享程度很高(即对于N位乘法器，只需要2n个输入就可以生成N2个部分乘积)。

The most promising of these proposals increases the density of MAC operations by .1 7 # while simultaneously improving their speed.

> 这些建议中最有希望的是将MAC操作的密度提高了0.1 7 #，同时提高了它们的速度。

It also reduces the required logic and routing area by 8% for general benchmarks, highlighting that more arithmetic density is beneficial for applications beyond DL.

> 对于一般基准测试，它还将所需的逻辑和路由面积减少了8%，突出表明更多的算术密度对DL以外的应用程序是有益的。

### B. Programmable Routing

> 可编程路由

Programmable routing commonly accounts for over 50% of both the fabric area and the critical path delay of applications [38], so its efficiency is crucial.

> 可编程路由通常占应用程序的fabric面积和关键路径延迟的50%以上[38]，因此其效率至关重要。

Programmable routing is composed of pre-fabricated wiring segments and programmable switches.

> 可编程路由由预制接线段和可编程交换机组成。

By programming an appropriate sequence of switches to be on, any function block output can be connected to any input.

> 通过编程适当的开关序列，任何功能块输出都可以连接到任何输入。

There are two main classes of FPGA routing architecture.

> FPGA路由架构主要有两类。

Hierarchical FPGAs are inspired by the fact that designs are inherently hierarchical: higher-level modules instantiate lower level modules and connect signals between them.

> 分层fpga的灵感来自于设计本质上是分层的:高层模块实例化低层模块并在它们之间连接信号。

Communication is more frequent between modules that are near each other in the design hierarchy, and hierarchical FPGAs can realize these connections with short wires that connect small regions of a chip.

> 在设计层次中彼此靠近的模块之间的通信更加频繁，而分层fpga可以通过连接芯片小区域的短导线来实现这些连接。

As shown in Fig. 8, to communicate to more distant regions of a hierarchical FPGA, a connection (highlight-ed in red) passes through multiple wires and switches as it traverses different levels of the interconnect hierarchy.

> 如图8所示，为了与层次FPGA的较远区域进行通信，连接(以红色突出显示)在穿越互连层次的不同级别时通过多条线和交换机。

This style of architecture was popular in many earlier FPGAs, such as Altera’s 7K and Apex 20K families, but it leads to very long wires at the upper levels of the interconnect hierarchy which became problematic as process scaling made such wires increasingly resistive.

> 这种风格的架构在许多早期的fpga中很流行，例如Altera的7K和Apex 20K系列，但它导致互连层次的上层非常长的电线，随着过程缩放使这些电线变得越来越电阻，这成为问题。

A strictly hierarchical routing architecture also results in some blocks that are physically close together (e.g. the blue blocks in Fig 8) which still require several wires and switches to connect.

> 严格的分层路由架构也会导致一些物理上靠近在一起的块(例如图8中的蓝色块)，这些块仍然需要几根电线和交换机连接。

Consequently it is primarily used today for smaller FPGAs, such as the FlexLogix FPGA IP cores that can be embedded in larger SoC designs [39].

> 因此，它今天主要用于较小的FPGA，如FlexLogix FPGA IP核，可以嵌入到较大的SoC设计中[39]。

---

The other type of FPGA interconnect is island-style, as depicted in Fig. 9.

> 另一种类型的FPGA互连是岛式的，如图9所示。

This architecture was pioneered by Xilinx and is inspired by the fact that a regular two-dimensional layout of horizontal and vertical directed wire segments can be efficiently laid out.

> 这种架构是由赛灵思首创的，其灵感来自于水平和垂直定向线段的规则二维布局，可以有效地布局。

As shown in Fig. 9, island-style routing includes three components: routing wire segments, connection blocks (multiplexers) that connect function block inputs to the routing wires, and switch blocks (programmable switches) that connect routing wires together to realize longer routes.

> 如图9所示，岛式布线包括三部分:布线线段、连接块(将功能块输入连接到布线线段的多路复用器)和将布线线段连接在一起以实现更长的路由的交换块(可编程交换机)。

The placement engine in FPGA CAD tools chooses which function block implements each element of a design in order to minimize the required wiring.

> FPGA CAD工具中的放置引擎选择哪个功能块实现设计的每个元素，以尽量减少所需的布线。

Consequently, most connections between function blocks span a small distance and can be implemented with a few routing wires as illustrated by the red connection in Fig. 9.

> 因此，功能块之间的大多数连接跨越很小的距离，可以用几根布线线实现，如图9中红色连接所示。

---

Creating a good routing architecture involves managing many complex trade-offs.

> 创建一个好的路由体系结构需要管理许多复杂的权衡。

It should contain enough programmable switching and wire segments that the vast majority of circuits can be implemented; however, too many wires and switches waste area.

> 它应该包含足够的可编程开关和电线段，绝大多数电路可以实现;然而，太多的电线和开关浪费了面积。

A routing architecture should also match the needs of applications: ideally short connections will be made with short wires to minimize capacitance and layout area, while long connections can use longer wiring segments to avoid the extra delay of passing through many routing switches.

> 路由架构还应符合应用程序的需求:理想情况下，短连接将使用短导线，以尽量减少电容和布局面积，而长连接可以使用更长的布线段，以避免通过许多路由交换机的额外延迟。

Some of the routing architecture parameters include: how many routing wires each logic block input or output can connect to (Fc),  how many other routing wires each wire can connect to (Fs), the lengths of the routing wire segments, the routing switch pattern, the electrical design of the wires and switches themselves, and the number of routing wires per channel [20].

> 一些路由架构参数包括:每个逻辑块输入或输出可以连接到多少条路由线(Fc)，每条线可以连接到多少条其他路由线(Fs)，路由线段的长度，路由开关模式，导线和开关本身的电气设计，以及每个通道的路由线数量[20]。

In Fig. 9 for example, Fc = 3, Fs = 3, the channel width is 4 wires, and some routing wires are of length 1, while others are of length 2.

> 以图9为例，Fc = 3, Fs = 3，通道宽度为4根线，有的走线长度为1，有的走线长度为2。

Fully evaluating these trade-offs for target applications and at a specific process node requires experimentation using a full CAD flow as detailed in Section II.

> 全面评估目标应用程序和特定过程节点的这些权衡需要使用第2节中详细介绍的完整CAD流进行实验。

---

Early island-style architectures incorporated only short wires that traversed a single logic block between programmable switches.

> 早期的岛式架构只包含在可编程开关之间穿过单个逻辑块的短线。

Later research showed that this resulted in more programmable switches than necessary, and that making all wiring segments span four logic blocks before terminating reduced application delay by 40% and routing area by 25% [40].

> 后来的研究表明，这导致可编程交换机数量超过必要数量，并且在终止之前使所有接线段跨越四个逻辑块可减少40%的应用延迟和25%的路由面积[40]。

Modern architectures include multiple lengths of wiring segments to better match the needs of short and long connections, but the most plentiful wire segments remain of moderate length, with four logic blocks being a popular choice.

> 现代架构包括多种长度的接线段，以更好地满足短连接和长连接的需求，但最丰富的接线段仍然是中等长度，四个逻辑块是一个流行的选择。

Longer distance connections can achieve lower delay using longer wire segments, but in recent process nodes wires that span many (e.g. 16) logic blocks must use wide and thick metal traces on upper metal layers to achieve acceptable resistance [41].

> 较长距离的连接可以使用较长的导线段实现较低的延迟，但在最近的工艺节点中，跨越许多(例如16)逻辑块的导线必须在上层金属层上使用宽而厚的金属走线，以实现可接受的电阻[41]。

The amount of such long-distance wiring one can include in a metal stack is limited.

> 在金属堆中可以包含的这种长距离布线的数量是有限的。

To best leverage such scarce wiring, Intel’s Stratix FPGAs allow long wire segments to be connected only to short wire segments, rather than function block inputs or outputs [42].

> 为了最好地利用这种稀缺的布线，英特尔的Stratix fpga允许长线段仅连接到短线段，而不是功能块输入或输出[42]。

This creates a form of routing hierarchy within an island-style FPGA, where short connections use only the shorter wires, but longer connections pass through short wires to reach the long wire network.

> 这在岛式FPGA中创建了一种路由层次结构，其中短连接仅使用较短的导线，而较长的连接通过短导线到达长导线网络。

Another area where hierarchical FPGA concepts are used within island-style FPGAs is within the logic blocks.

> 在岛式FPGA中使用分层FPGA概念的另一个领域是在逻辑块中。

As illustrated in Fig. 4(d), most logic blocks now group multiple BLEs together with local routing.

> 如图4(d)所示，大多数逻辑块现在将多个ble与本地路由组合在一起。

This means each logic block is a small cluster in a hierarchical FPGA; island-style routing interconnects the resulting thousands of logic clusters.

> 这意味着每个逻辑块是分层FPGA中的一个小集群;岛式路由将产生的数千个逻辑集群相互连接。

---

There has been a great deal of research into the op-timal amount of switching, and how to best arrange the switches.

> 关于开关的最优量以及开关的最佳排列方式，人们进行了大量的研究。

While there are many detailed choices, a few principles have emerged.

> 虽然有许多详细的选择，但已经出现了一些原则。

The first is that the connectiv-ity between function block pins and wires ( Fc ) can be relatively low: typically only 10% or less of the wires that pass by a pin will have switches to connect to it.

> 首先是功能块引脚和导线(Fc)之间的连接性相对较低:通常只有10%或更少的导线通过引脚将有开关连接到它。

Simi-larly, the number of other wires that a routing wire can connect to at its end ( Fs ) can also be low, but it should be at least 3 so that a signal can turn left, right, or go straight at a wire end point.

> 同样，布线线在其末端(f)可以连接的其他导线的数量也可以很低，但至少应该是3，以便信号可以向左、向右或在导线末端直走。

The local routing in a logic cluster (described in Section III-A) allows some block inputs and some block outputs to be swapped during routing.

> 逻辑集群中的本地路由(在章节III-A中描述)允许在路由期间交换一些块输入和一些块输出。

By leveraging this extra degree of flexibility and considering all the options presented by the multi-stage programmable routing network, the routing CAD tool can achieve high completion rates even with low Fc and Fs values.

> 通过利用这种额外的灵活性，并考虑到多阶段可编程路由网络提供的所有选项，即使在低Fc和f值的情况下，路由CAD工具也可以实现高完成率。

Switch patterns that give more options to the routing CAD tool also help routability; for example, the Wilton switch pattern ensures that following a different sequence of channels lets the router reach different wire segments near a destination block [43].

> 为路由CAD工具提供更多选项的开关模式也有助于可达性;例如，威尔顿交换机模式确保遵循不同的通道序列，使路由器能够到达目标块附近的不同线段[43]。

---

There are also multiple options for the electrical design of programmable switches, as shown in Fig. 10.

> 可编程开关的电气设计也有多种选择，如图10所示。

Early FPGAs used pass gate transistors controlled by SRAM cells to connect wires.

> 早期的fpga使用由SRAM单元控制的通栅晶体管来连接导线。

While this is the smallest switch possible in a conventional CMOS process, the delay of routing wires connected in series by pass transistors grows quadratically, making them very slow for large FPGAs.

> 虽然这是传统CMOS工艺中最小的开关，但通过通路晶体管串联连接的布线延迟呈二次增长，这使得它们对于大型fpga来说非常慢。

Adding some tri-state buffer switches costs area, but improves speed [40].

> 添加一些三状态缓冲开关会消耗区域，但会提高速度[40]。

Most recent FPGAs primarily use a multiplexer built out of pass gates followed by a buffer that cannot be tri-stated, as shown in detail in Fig. 4(b).

> 大多数最新的fpga主要使用由通门构建的多路复用器，然后是一个不能三态的缓冲区，如图4(b)所示。

The pass transistors in this direct drive switch can be small as they are lightly loaded, while the buffer can be larger to drive the significant capacitance of a routing wire segment.

> 这种直接驱动开关中的通路晶体管可以很小，因为它们负载很轻，而缓冲器可以更大，以驱动布线线段的重要电容。

Such direct drive switches create a major constraint on the switch pattern: a wire can only be driven at one point, so only function block outputs and routing wires near that point can feed its routing multiplexer inputs and hence be possible signal sources.

> 这种直接驱动开关对开关模式造成了一个主要的限制:导线只能在一个点上驱动，因此只有在该点附近的功能块输出和布线导线才能馈送其路由多路复用器输入，因此可能是信号源。

Despite this constraint, both academic and industrial work has concluded that direct drive switches improve both area and speed due to their superior electrical characteristics [42], [44].

> 尽管存在这一限制，学术和工业工作都得出结论，直接驱动开关由于其优越的电气特性而提高了面积和速度[42]，[44]。

The exception is expensive or rare wires such as long wires implemented on wide metal traces on upper metal layers or the interposer-crossing wires discussed later in Section III-G.

> 例外情况是昂贵或稀有的电线，如在上层金属层上的宽金属线上实施的长电线或稍后在第III-G节中讨论的介面交叉电线。

These wires often have multiple tri-state buffers that can drive them, as the cost of these larger programmable switches is merited to allow more flexible usage of these expensive wires.

> 这些导线通常有多个三态缓冲器来驱动它们，因为这些较大的可编程开关的成本值得允许更灵活地使用这些昂贵的导线。

---

A major challenge for FPGA routing is that the delay of long wires is not improving with process scaling, which means that the delay to cross the chip is stagnating or increasing even as clock frequencies rise.

> FPGA路由的一个主要挑战是，长导线的延迟并没有随着进程的扩展而改善，这意味着即使时钟频率上升，跨芯片的延迟也会停滞不前或增加。

This has led FPGA application developers to increase the amount of pipelining in their designs, thereby allowing multiple clock cycles for long routes.

> 这使得FPGA应用程序开发人员在其设计中增加了流水线的数量，从而允许长路由的多个时钟周期。

To make this strategy more effective, some FPGA manufacturers have integrated registers within the routing network itself.

> 为了使这种策略更有效，一些FPGA制造商在路由网络本身中集成了寄存器。

Intel’s Stratix 10 device allows each routing driver (i.e. multiplexer followed by a buffer) to be configured as a pulse latch as shown in 6(b), thereby acting as a register with low delay but relatively poor hold time.

> 英特尔的Stratix 10设备允许每个路由驱动程序(即多路复用器后面跟着一个缓冲区)配置为如图6(b)所示的脉冲锁存器，从而作为一个低延迟但相对较差保持时间的寄存器。

This allows deep pipelining of interconnect without using expensive logic resources, at the cost of a modest area and delay increase to the routing driver [45].

> 这允许在不使用昂贵的逻辑资源的情况下对互连进行深度流水线，代价是路由驱动程序的适度面积和延迟增加[45]。

Hold time concerns mean that using pulse latches in immediately consecutive Stratix 10 routing switches is not possible, so Intel refined this approach in their next-generation Agilex devices by integrating actual registers (with better hold time) on only one-third of the interconnect drivers (to mitigate the area cost) [34].

> 保持时间问题意味着在立即连续的Stratix 10路由交换机中使用脉冲锁存器是不可能的，因此英特尔在其下一代Agilex设备中改进了这种方法，仅在三分之一的互连驱动程序上集成实际寄存器(具有更好的保持时间)(以减轻面积成本)[34]。

Rather than integrating registers throughout the interconnect, Xilinx’s Versal devices instead add by-passable registers only on the inputs to function blocks.

> 赛灵思的Versal器件没有在整个互连中集成寄存器，而是只在功能块的输入端添加可旁路寄存器。

Unlike Intel’s interconnect registers, these input registers are full-featured, with clock enable and clear signals [46].

> 与英特尔的互连寄存器不同，这些输入寄存器功能齐全，具有时钟使能和清晰信号[46]。

### C. Programmable IO

> 可编程 IO

FPGAs include unique programmable IO structures to allow them to communicate with a very wide variety of other devices, making FPGAs the communications hub of many systems.

> fpga包括独特的可编程IO结构，允许它们与各种各样的其他设备通信，使fpga成为许多系统的通信枢纽。

For a single set of physical IOs to programmably support many different IO interfaces and standards is challenging, as it requires adaptation to different voltage levels, electrical characteristics, timing specifications, and command protocols.

> 让一组物理IOs以可编程方式支持许多不同的IO接口和标准是具有挑战性的，因为它需要适应不同的电压水平、电气特性、时序规范和命令协议。

Both the value and the challenge of programmable IO are highlighted by the large area devoted to IOs on FPGAs.

> 可编程IO的价值和挑战都是通过fpga上的IOs的大量领域来突出的。

For example, Altera’s Stratix II (90 nm) devices support 28 different IO standards and devote 20% (largest device) to 48% (smallest device) of their die area to IO-related structures.

> 例如，Altera的Stratix II (90nm)器件支持28种不同的IO标准，并将20%(最大器件)至48%(最小器件)的芯片面积用于IO相关结构。

---

As Fig. 11 shows, FPGAs address this challenge using a combination of approaches [47]–[49].

> 如图11所示，fpga使用多种方法[47]-[49]解决了这一挑战。

First, FPGAs use IO buffers that can operate across a range of voltages.

> 首先，fpga使用可以跨电压范围工作的IO缓冲器。

These IOs are grouped into banks (commonly on the order of 50 IOs per bank), where each bank has a separate Vddio rail for the IO buffer.

> 这些IO被分组到bank中(通常每个bank有50个IO)，其中每个bank有一个独立的Vddio rail用于IO缓冲区。

This allows different banks to operate at different voltage levels; e.g.

> 这允许不同的银行在不同的电压水平下工作;如。

IOs in one bank could be operating at 1.8 V while those in a different bank operate at 1.2 V.

> 一家银行的IOs可以在1.8 V的电压下运行，而另一家银行的IOs可以在1.2 V的电压下运行。

Second, each IO can be used separately for single-ended standards, or pairs of IOs can be programmed to form the positive and negative line for differential IO standards.

> 其次，每个IO可以单独用于单端标准，也可以对IO进行编程，形成差分IO标准的正负线。

Third, IO buffers are implemented with multiple parallel pull-up and pull-down transistors so that their drive strengths can be programmably adjusted by enabling or disabling different numbers of pull-up/pull-down pairs.

> 第三，IO缓冲器由多个并行上拉和下拉晶体管实现，因此它们的驱动强度可以通过启用或禁用不同数量的上拉/下拉对来可编程地调整。

By programming some pull-up or pull-down transistors to be enabled even when no output is being driven, FPGA IOs can also be programmed to implement different on-chip termination resistances to minimize signal reflections.

> 通过编程一些上拉或下拉晶体管，即使在没有输出驱动的情况下也能启用，FPGA io也可以编程来实现不同的片上终端电阻，以最小化信号反射。

Programmable delay chains provide a fourth level of configurability, allowing fine delay adjustments of signal timing to and from the IO buffer.

> 可编程延迟链提供了第四级可配置性，允许对信号时序进行精细的延迟调整。

---

In addition to electrical and timing programmability, FPGA IO blocks contain additional hardened digital circuitry to simplify capturing and transferring IO data to the fabric.

> 除了电气和定时可编程性外，FPGA IO模块还包含额外的强化数字电路，以简化捕获和将IO数据传输到结构。

Generally some or all of this hardened circuitry can be bypassed by SRAM-controlled muxes, allowing FPGA users to choose which hardened functions are desirable for a given design and IO protocol.

> 通常，sram控制的复用器可以绕过部分或全部强化电路，从而允许FPGA用户选择给定设计和IO协议所需的强化功能。

Part ➄ of Fig. 11 shows a number of common digital logic options on the IO input path: a capture register, double to single-data rate conversion registers (used with DDR memories), and serial-to-parallel converters to allow transfer to the fabric at a lower frequency.

> 图11部分的规定显示了IO输入路径上的一些常见数字逻辑选项:捕获寄存器、双数据速率到单数据速率转换寄存器(与DDR存储器一起使用)，以及允许以较低频率传输到结构的串行到并行转换器。

Most FPGAs now also contain by-passable higher-level blocks that connect to a group of IOs and implement higher-level protocols like DDR memory controllers.

> 现在，大多数fpga还包含可绕过的高级块，这些块连接到一组IOs，并实现DDR内存控制器等高级协议。

Together these approaches allow the general-purpose FPGA IOs to service many different protocols, at speeds up to 3.2 Gb/s.

> 这些方法使通用FPGA io能够以高达3.2 Gb/s的速度服务于许多不同的协议。

---

The highest speed IOs implement serial protocols, such as PCIe and Ethernet, that embed the clock in data transitions and can run at 28 Gb/s or more.

> 最高速度的IOs实现串行协议，如PCIe和以太网，将时钟嵌入到数据传输中，可以以28 Gb/s或更高的速度运行。

To achieve these speeds, FPGAs include a separate group of differential-only IOs with less voltage and electrical programmability; they can only be used as serial transceivers [50].

> 为了实现这些速度，fpga包括一组单独的纯差分IOs，具有较低的电压和电气可编程性;它们只能用作串行收发器[50]。

Just as for the general-purpose IOs, these serial IOs have a sequence of high-speed hardened circuits between them and the fabric, some of which can be optionally bypassed to allow end-users to customize the exact interface protocol.

> 就像通用io一样，这些串行io在它们和结构之间有一系列高速硬化电路，其中一些可以选择性地绕过，以允许最终用户自定义确切的接口协议。

---

Overall, FPGA IO design is very challenging, due to the dual (and competing) demands to make the IO not only very fast but also programmable.

> 总的来说，FPGA IO设计是非常具有挑战性的，因为双重(和竞争)的要求，使IO不仅非常快，而且可编程。

In addition, distributing the very high data bandwidths from IO interfaces requires wide soft buses in the fabric, which creates additional challenges as discussed later in Section III-F.

> 此外，从IO接口分配非常高的数据带宽需要在结构中使用宽的软总线，这就产生了额外的挑战，稍后将在第III-F节中讨论。

### D. On-Chip Memory

> 片上内存

The first form of on-chip memory elements in FPGA architectures was FFs integrated in the FPGA’s logic blocks as described in Section III-A.

> FPGA架构中的片上存储元件的第一种形式是集成在FPGA逻辑块中的ff，如第III-A节所述。

However, as FPGA logic capacity grew, they were used to implement larger systems which almost always require memory to buffer and re-use data on chip, making it highly desirable to have denser on-chip storage since building large RAMs out of registers and LUTs is over 100# less dense than an (ASIC-style) SRAM block.

> 然而，随着FPGA逻辑容量的增长，它们被用于实现更大的系统，这些系统几乎总是需要内存来缓冲和重用芯片上的数据，这使得具有更密集的片上存储变得非常理想，因为从寄存器和lut中构建大型ram的密度比(asic风格)SRAM块的密度低100多#。

At the same time, the RAM needs of applications implemented on FPGAs are very diverse, including (but not limited to) small coefficient storage RAMs for FIR filters, large buffers for network packets, caches and register files for processor-like modules, read-only memory for instructions, and FIFOs of myriad sizes to decouple computation modules.

> 同时，在fpga上实现的应用程序的RAM需求非常多样化，包括(但不限于)用于FIR滤波器的小系数存储RAM，用于网络数据包的大缓冲区，用于处理器类模块的缓存和寄存器文件，用于指令的只读存储器，以及用于解耦计算模块的无数大小的fifo。

This means that there is no single RAM configuration (capacity, word width, number of ports) used universally in FPGA designs, making it challenging to decide on what kind(s) of RAM blocks should be added to an FPGA such that they are efficient for a broad range of uses.

> 这意味着在FPGA设计中没有普遍使用的单一RAM配置(容量，字宽，端口数量)，这使得决定应该将哪种类型的RAM块添加到FPGA中以使其有效地用于广泛的用途变得具有挑战性。

The first FPGA to include hard functional blocks for memory (block RAMs or BRAMs) was the Altera Flex 10 K in 1995 [51].

> 第一个包含内存硬功能块(块ram或bram)的FPGA是1995年的Altera Flex 10 K[51]。

It included columns of small (2 kb) BRAMs that connect to the rest of the fabric through the programmable routing.

> 它包括小的(2kb) bram列，这些bram通过可编程路由连接到fabric的其余部分。

FPGAs have gradually incorporated larger and more diverse BRAMs and it is typical for ~25% of the area of a modern FPGA to be dedicated for BRAMs [52].

> FPGA逐渐纳入了更大、更多样化的bram，通常现代FPGA约25%的面积用于bram[52]。

---

An FPGA BRAM consists of an SRAM-based memory core, with additional peripheral circuitry to make them more configurable for multiple purposes and to connect them to the programmable routing.

> FPGA BRAM由一个基于sram的存储核心组成，并带有额外的外围电路，使它们更可配置用于多种用途，并将它们连接到可编程路由。

An SRAM-based BRAM is typically organized as illustrated in Fig. 12.

> 基于sram的BRAM通常组织如图12所示。

It consists of a two-dimensional array of SRAM cells to store bits, and a considerable amount of peripheral circuitry to orchestrate access to these cells for read/write operations.

> 它由一个用于存储位的二维SRAM单元阵列和相当数量的外围电路组成，以协调对这些单元的读/写操作的访问。

To simplify timing of the read and write operations, all modern FPGA BRAMs register all their inputs.

> 为了简化读取和写入操作的时序，所有现代FPGA bram都对其所有输入进行寄存器。

During a write operation, the column decoder activates the write drivers, which in turn charge the bitlines (BL and )BL according to the input data to-be-written to the memory cells.

> 在写操作期间，列解码器激活写驱动程序，它依次根据要写入内存单元的输入数据对位行(BL和)BL进行收费。

Simultaneously, the row decoder activates the wordline of the row specified by the input write address, connecting one row of cells to their bitlines so they are overwritten with new data.

> 同时，行解码器激活由输入写地址指定的行的字行，将一行单元格连接到它们的位行，以便用新数据覆盖它们。

During a read operation, both the BL and BL are pre-charged high and then the row decoder activates the wordline of the row specified by the input read address.

> 在读取操作期间，BL和BL都被预充高值，然后行解码器激活由输入读地址指定的行的字行。

The contents of the activated cells cause a slight difference in the voltage between BL and ,BL which is sensed and amplified by the sense amplifier circuit to produce the output data [52].

> 激活细胞的内容物使BL和BL之间的电压产生微小的差异，这种差异被感测放大电路感测放大，产生输出数据[52]。

---

The main architectural decisions in designing FPGA BRAMs are choosing their capacity, data word width, and number of read/write ports.

> 设计FPGA bram的主要架构决策是选择其容量、数据字宽和读/写端口数量。

More capable BRAMs cost more silicon area, so architects must carefully balance BRAM design choices while taking into account the most common use cases in application circuits.

> 功能更强大的BRAM需要更多的硅面积，因此架构师必须仔细平衡BRAM设计选择，同时考虑到应用电路中最常见的用例。

The area occupied by the SRAM cells grows linearly with the capacity of the BRAM, but the area of the peripheral circuitry and the number of routing ports grows sub-linearly.

> SRAM单元所占用的面积随着BRAM容量的增加呈线性增长，但外围电路的面积和路由端口的数量呈次线性增长。

This means that larger BRAMs have lower area per bit, making large on-chip buffers more efficient.

> 这意味着更大的bram具有更低的每比特面积，使大型片上缓冲区更有效。

On the other hand, if an application requires only small RAMs, much of the capacity of a larger BRAM may be wasted.

> 另一方面，如果应用程序只需要较小的ram，则较大的ram的大部分容量可能会被浪费。

Similarly, a BRAM with a larger data width can provide higher data bandwidth to downstream logic.

> 同样，具有更大数据宽度的BRAM可以为下游逻辑提供更高的数据带宽。

However, it costs more area than a BRAM with the same capacity but a smaller word width, as the larger data word width necessitates more sense amplifiers, write drivers and programmable routing ports.

> 然而，它比具有相同容量但字宽较小的BRAM占用更多的面积，因为更大的数据字宽需要更多的感测放大器，写入驱动程序和可编程路由端口。

Finally, increasing the number of read/write ports to a BRAM increases the area of both the SRAM cells and the peripheral circuitry, but again increases the data bandwidth the BRAM can provide and allows more diverse uses.

> 最后，增加读写端口到BRAM的数量增加了SRAM单元和外围电路的面积，但再次增加了BRAM可以提供的数据带宽，并允许更多样化的用途。

For example, FIFOs (which are ubiquitous in FPGA designs) require both a read and a write port.

> 例如，fifo(在FPGA设计中无处不在)需要一个读端口和一个写端口。

The implementation details of a dual-port SRAM cell is shown at the bottom of Fig. 12.

> 双端口SRAM单元的实现细节如图12底部所示。

Implementing a second port to the SRAM cell (port B highlighted in red) adds two transistors, increasing the area of the SRAM cells by 33%.

> 实现第二个端口到SRAM单元(端口B以红色突出显示)增加了两个晶体管，使SRAM单元的面积增加了33%。

In addition, the second port also needs an additional copy of the sense amplifiers, write drivers and row decoders (the “Read/Write Circuitry B” and “Row Decoder B” blocks in Fig. 12).

> 此外，第二个端口还需要一个附加的感测放大器、写入驱动器和行解码器(图12中的“读/写电路B”和“行解码器B”块)。

If both ports are read/write (r/w), we also have to double the number of ports to the programmable routing.

> 如果两个端口都是读/写(r/w)，我们还必须将可编程路由的端口数量加倍。

---

Because the FPGA on-chip memory must satisfy the needs of every application implemented on that FPGA, it is also common to add extra configurability to BRAMs to allow them to adapt to application needs [53], [54].

> 由于FPGA片上存储器必须满足在该FPGA上实现的每个应用程序的需求，因此通常还可以向bram添加额外的可配置性，以使其适应应用程序需求[53]，[54]。

FPGA BRAMs are designed to have configurable width and depth by adding low-cost multiplexing circuitry to the peripherals of the memory array.

> 通过在存储器阵列的外设上添加低成本的多路复用电路，FPGA bram被设计成具有可配置的宽度和深度。

For example, in Fig. 12 the actual SRAM array is implemented as a 4 × 8-bit array, meaning it naturally stores 8-bit data words.

> 例如，在图12中，实际的SRAM数组被实现为一个4 × 8位数组，这意味着它自然地存储8位数据字。

By adding multiplexers controlled by 3 address bits to the output crossbar, and extra decoding and enabling logic to the read/write circuitry, this RAM can also operate in 8 × 4-bit, 16 × 2-bit or 32 × 1-bit modes.

> 通过在输出交叉栏上增加由3个地址位控制的多路复用器，以及额外的解码和使能读/写电路的逻辑，该RAM还可以在8 × 4位，16 × 2位或32 × 1位模式下工作。

The width configurability decoder (WCnfg Dec.) selects between Vdd and address bits, as shown in the top-left of Fig. 12 for a maximum word size of 8 bits.

> 宽度可配置解码器(WCnfg dec)在Vdd和地址位之间进行选择，如图12左上角所示，最大字长为8位。

The multiplexers are programmed using configuration SRAM cells and are used to generate column select (CS) and write enable (Wen) signals that control the sense amplifiers and write drivers for narrow read and write operations, respectively.

> 多路复用器使用配置SRAM单元进行编程，并用于生成列选择(CS)和写入使能(Wen)信号，分别控制用于窄读和写操作的感测放大器和写入驱动器。

For typical BRAM sizes (several kb or more), the cost of this additional width configurability circuitry is small compared to the cost of a conventional SRAM array, and it does not require any additional routing ports.

> 对于典型的BRAM大小(几kb或更多)，与传统SRAM阵列的成本相比，这种额外宽度可配置电路的成本很小，并且不需要任何额外的路由端口。

---

Another unique component of the FPGA BRAMs compared to conventional memory blocks is their interface to the programmable routing fabric.

> 与传统存储器块相比，FPGA bram的另一个独特组件是它们与可编程路由结构的接口。

This interface is generally designed to be similar to that of the logic blocks described in Section III-A; it is easier to create a routing architecture that balances flexibility and cost well if all block types connect to it in similar ways.

> 这个接口通常被设计成类似于第III-A节中描述的逻辑块;如果所有块类型都以类似的方式连接到路由体系结构，那么创建一个平衡灵活性和成本的路由体系结构就会更容易。

Connection block multiplexers, followed by local crossbars in some FPGAs, form the BRAM input routing ports, while the read outputs drive switch block multiplexers to form the output routing ports.

> 连接块多路复用器，随后是一些fpga中的本地交叉条，形成BRAM输入路由端口，而读取输出驱动开关块多路复用器形成输出路由端口。

These routing interfaces are costly, particularly for small BRAMs; they constitute 5% to 35% of the BRAM tile area for 256Kb down to 8Kb BRAMs, respectively [55].

> 这些路由接口是昂贵的，特别是对于小型bram;从256Kb到8Kb的BRAM，它们分别占BRAM块面积的5%到35%[55]。

This motivates minimizing the number of routing ports to a BRAM as much as possible without unduly comprising its functionality.

> 这促使尽可能减少到BRAM的路由端口数量，而不会过度地影响其功能。

Table I summarizes the number of routing ports required for different numbers and types of BRAM read and write ports.

> 表1总结了不同数量和类型的BRAM读写端口所需的路由端口数量。

For example, a single-port BRAM (1r/w) requires W + log2(D) input ports for write data and read/write address, and W output ports for read data, where W and D are the maximum word width and the BRAM depth, respectively.

> 例如，单端口BRAM (1r/w)需要w + log2(D)个输入端口用于写入数据和读写地址，需要w个输出端口用于读取数据，其中w和D分别为最大字宽和BRAM深度。

The table shows that a true dual-port (2r/w) BRAM requires 2 W more ports compared to a simple dual-port (1r+1w) BRAM, which significantly increases the cost of the routing interfaces.

> 该表显示，与简单的双端口(1r+1w) BRAM相比，真正的双端口(2r/w) BRAM需要多2w的端口，这大大增加了路由接口的成本。

While true dual-port memory is useful for register files, caches and shared memory switches, the most common use of multi-ported RAMs on FPGAs is for FIFOs, which require only one read and one write port (1r+1w rather than 2r/w ports).

> 虽然真正的双端口内存对寄存器文件、缓存和共享内存开关很有用，但fpga上多端口ram最常见的用途是fifo，它只需要一个读和一个写端口(1r+1w而不是2r/w端口)。

Consequently, FPGA BRAMs typically have true dual-port SRAM cores but with only enough routing interfaces for simple-dual port mode at the full width supported by the SRAM core (W), and limit the width of the true-dual port mode to only half of the maximum width (W / 2).

> 因此，FPGA bram通常具有真正的双端口SRAM内核，但只有足够的路由接口用于SRAM内核支持的全宽度(W)的简单双端口模式，并将真正的双端口模式的宽度限制为最大宽度(W / 2)的一半。

---

Another way to mitigate the cost of additional BRAM ports is to multi-pump the memory blocks (i.e. operate the BRAMs at a frequency that is a multiple of that used for the rest of the design logic).

> 另一种降低额外BRAM端口成本的方法是对内存块进行多泵(即，以用于其余设计逻辑的频率的倍数操作BRAM)。

By doing so, a physically single-ported SRAM array can implement a logically multi-ported BRAM without the cost of additional ports as in Tabula’s Spacetime architecture [56].

> 通过这样做，物理上的单端口SRAM阵列可以实现逻辑上的多端口BRAM，而无需像Tabula的Spacetime架构[56]中那样增加额外的端口成本。

Multi-pumping can also be used with conventional FPGA BRAMs by building the time-multiplexing logic in the soft fabric; however, this leads to aggressive timing constraints for the time-multiplexing logic, which can make timing closure more challenging and increase compile time.

> 通过在软结构中构建时间复用逻辑，也可以将多泵浦与传统的FPGA bram一起使用;然而，这会导致时间多路复用逻辑的严格时序约束，这可能使时序闭包更具挑战性，并增加编译时间。

Altera introduced quad-port BRAMs in its Mercury devices in the early 2000s to make shared memory switches (useful in packet processing) and register files more efficent [57].

> Altera在21世纪初在其Mercury设备中引入了四端口bram，以使共享内存交换(在数据包处理中很有用)和注册文件更有效[57]。

However, this feature increased the BRAM size and was not sufficiently used to justify its inclusion in subsequent FPGA generations.

> 然而，这一特性增加了BRAM的大小，并没有充分地用于证明其在随后的FPGA世代中包含的合理性。

Instead designers use a variety of techniques to combine dual-ported FPGA BRAMs and soft logic to make highly-ported structures when needed, albeit at lower efficiency [58], [59].

> 相反，设计人员使用各种技术将双端口FPGA bram和软逻辑结合起来，在需要时制作高端口结构，尽管效率较低[58]，[59]。

We refer the interested reader to both [52] and [55] for extensive details about the design of BRAM core and peripheral circuitry.

> 我们建议感兴趣的读者参考[52]和[55]，了解有关BRAM核心和外围电路设计的详细信息。

---

In addition to building BRAMs, FPGA vendors can add circuitry that allows designers to repurpose the LUTs that form the logic fabric into additional RAM blocks.

> 除了构建bram之外，FPGA供应商还可以添加电路，使设计人员能够将构成逻辑结构的lut重新用于额外的RAM块。

The truth tables in the logic block K-LUTs are 2K ×1-bit read-only memories; they are written once by the configuration circuitry when the design bitstream is loaded.

> 逻辑块k - lut中的真值表为2K ×1-bit只读存储器;当加载设计位流时，它们由配置电路写入一次。

Since LUTs already have read circuitry (read out a stored value based on a K-bit input/address), they can be used as small distributed LUT-based RAMs (LUT-RAMs) just by adding designer-controlled write circuitry.

> 由于lut已经具有读电路(根据k位输入/地址读出存储值)，因此只需添加设计人员控制的写电路，它们就可以用作小型分布式基于lut的ram (lut - ram)。

However, a major concern is the number of additional routing ports necessary to implement the write functionality to change a LUT to a LUT-RAM.

> 然而，一个主要问题是实现将LUT更改为LUT- ram的写入功能所需的额外路由端口的数量。

For example, an ALM in recent Altera/Intel architectures is a 6-LUT that can be fractured into two 5-LUTs and has 8 input routing ports, as explained in Section III-A.

> 例如，最近Altera/Intel架构中的ALM是一个6-LUT，可以分成两个5- lut，并具有8个输入路由端口，如第III-A节所述。

This means it can operate as a 64 × 1-bit or a 32 × 2-bit memory with 6 or 5 bits for read address, respectively.

> 这意味着它可以作为64 × 1位或32 × 2位的存储器，分别具有6或5位的读地址。

This leaves only 2 or 3 unused routing ports, which are not enough for write address, data, and write enable (8 total signals) if we want to read and write in each cycle (simple dual-port mode), which is the most commonly used RAM mode in FPGA designs.

> 这只留下2或3个未使用的路由端口，如果我们想要在每个周期(简单的双端口模式)中读写，这对于写入地址，数据和写入启用(8个总信号)是不够的，这是FPGA设计中最常用的RAM模式。

To overcome this problem, an entire logic block of 10 ALMs is configured as a LUT-RAM to amortize the control circuitry and address bits across 10 ALMs.

> 为了克服这个问题，将10个alm的整个逻辑块配置为LUT-RAM，以分摊控制电路和跨10个alm的地址位。

The write address and write enable are assembled by bringing one signal in from an unused routing port in each ALM and broadcasting the resulting address and enable to all ALMs [60].

> 写地址和写使能通过从每个ALM中未使用的路由端口引入一个信号并将结果地址和使能广播给所有ALM来组装[60]。

Consequently, a logic block can implement a 64 × 10-bit or 32 × 20-bit simple dual-port RAM, but has a restriction that a single logic block cannot mix logic and LUT-RAM.

> 因此，一个逻辑块可以实现64 × 10位或32 × 20位的简单双端口RAM，但有一个限制，即单个逻辑块不能混合逻辑和LUT-RAM。

Xilinx Ultrascale similarly converts an entire logic block to LUT-RAM, but all the routing ports of one out of the eight LUTs in a logic block are repurposed to drive the (broadcast) write address and enable signals.

> Xilinx Ultrascale类似地将整个逻辑块转换为LUT-RAM，但逻辑块中八个lut中的一个的所有路由端口都被重新用于驱动(广播)写地址和启用信号。

Therefore, a Xilinx logic block can implement a 64 × 7-bit or 32 × 14-bit simple dual-port RAM, or a slightly wider single-port RAM (64 × 8-bit or 32 × 16-bit).

> 因此，Xilinx逻辑块可以实现64 × 7位或32 × 14位简单双端口RAM，或稍宽的单端口RAM (64 × 8位或32 × 16位)。

Avoiding extra routing ports keeps the cost of LUT-RAM low, but it still adds some area.

> 避免额外的路由端口可以降低LUT-RAM的成本，但它仍然增加了一些面积。

Since it would be very unusual for a design to convert more than 50% of the logic fabric to LUT-RAMs, both Altera/Intel and Xilinx have elected to make only half of their logic blocks LUT-RAM capable in their recent architectures, thereby further reducing the area cost.

> 由于将超过50%的逻辑结构转换为LUT-RAM的设计是非常不寻常的，因此Altera/Intel和Xilinx都选择在其最新架构中仅使一半的逻辑模块具有LUT-RAM功能，从而进一步降低了面积成本。

---

Designers require many different RAMs in a typical design, all of which must be implemented by the fixed BRAM and LUT-RAM resources on the chip.

> 设计人员在一个典型的设计中需要许多不同的ram，所有这些都必须通过芯片上的固定BRAM和LUT-RAM资源来实现。

Forcing designers to determine the best way to combine BRAM and LUT-RAM for each memory configuration they need and writing verilog to implement them would be laborious and also would tie the design to a specific FPGA architecture.

> 迫使设计人员确定为他们需要的每种内存配置组合BRAM和LUT-RAM的最佳方法，并编写verilog来实现它们将是费力的，并且还将设计与特定的FPGA架构联系起来。

Instead, the vendor CAD tools include a RAM mapping stage that implements the logical memories in the user’s design using the physical BRAMs and LUT-RAMs on the chip.

> 相反，供应商CAD工具包括一个RAM映射阶段，该阶段使用芯片上的物理bram和lut -RAM在用户的设计中实现逻辑存储器。

The RAM mapper chooses the physical memory implementation (i.e. memory type and the width/number/type of its ports) and generates any additional logic required to combine multiple BRAMs or LUT-RAMs to implement each logical RAM.

> RAM映射器选择物理内存实现(即内存类型及其端口的宽度/数量/类型)，并生成组合多个bram或lut -RAM以实现每个逻辑RAM所需的任何附加逻辑。

Fig. 13 gives an example of mapping a logical 2048 × 32-bit RAM with 2 read and 1 write ports to an FPGA with physical 1024 × 8-bit dual-port BRAMs.

> 图13给出了一个将具有2个读和1个写端口的逻辑2048 × 32位RAM映射到具有1024 × 8位双端口bram的FPGA的示例。

First, four physical BRAMs are combined in parallel to make wider RAMs with no extra logic.

> 首先，在没有额外逻辑的情况下，将四个物理ram并行组合成更宽的ram。

Then, soft logic resources are used to perform depth-wise stitching of two sets of four physical BRAMs, such that the most-significant bits of the write and read addresses are used as write enable and read output mux select signals, respectively.

> 然后，使用软逻辑资源对两组4个物理bram进行深度拼接，使写地址和读地址的最高有效位分别用作写使能和读输出多路选择信号。

Finally, in this case we require two read ports and one write port while the physical BRAMs only support a maximum of 2r/w ports.

> 最后，在这种情况下，我们需要两个读端口和一个写端口，而物理bram只支持最大2r/w端口。

To implement the second read port, the whole structure is either replicated (see Fig. 13) or double-pumped as previously explained.

> 为了实现第二个读端口，整个结构要么被复制(见图13)，要么像前面解释的那样被双泵浦。

Several algorithms for optimizing RAM mapping are described in [61], [62].

> [61]，[62]中描述了几种优化RAM映射的算法。

---

Over the past 25 years, FPGA memory architecture has evolved considerably and has also become increasingly important, as the ratio of memory to logic on an FPGA die has grown significantly.

> 在过去的25年中，随着FPGA芯片上的内存与逻辑的比例显著增长，FPGA内存架构已经发生了相当大的发展，并且变得越来越重要。

Fig. 14 plots the memory bits per logic element (including LUT-RAM) versus the number of logic elements in Altera/Intel devices starting from the 350 nm Flex 10 K devices (1995) to 10 nm Agilex devices (2019).

> 图14绘制了从350 nm Flex 10 K器件(1995年)到10 nm Agilex器件(2019年)的Altera/Intel器件中每个逻辑元件(包括LUT-RAM)的内存位数与逻辑元件数量的关系。

There has been a gradual increase in the memory richness of FPGAs over time, and to meet the demand for more bits, modern BRAMs have larger capacities (20 kb) than the first BRAMs (2 kb).

> 随着时间的推移，fpga的内存丰富度逐渐增加，为了满足对更多位的需求，现代bram的容量(20 kb)比第一代bram (2 kb)更大。

Some FPGAs have had highly heterogeneous BRAM architectures in order to provide some physical RAMs that are efficient for small or wide logical RAMs, and others that are efficient for large and relatively narrow logical RAMs.

> 一些fpga具有高度异构的BRAM架构，以便提供一些对小型或宽逻辑ram有效的物理ram，以及其他对大型和相对狭窄的逻辑ram有效的物理ram。

For example, Stratix (130 nm) had 3 types of BRAM, with capacities of 512 b, 4 kb and 512 kb.

> 例如，Stratix (130 nm)有3种类型的BRAM，容量分别为512 b、4 kb和512 kb。

The introduction of LUT-RAM in Stratix III (65 nm) reduced the need for small BRAMs, so it moved to a memory architecture with 9 kb and 144 kb BRAM.

> 在Stratix III (65 nm)中引入LUT-RAM减少了对小型BRAM的需求，因此它转向了具有9 kb和144 kb BRAM的内存架构。

Stratix V (28 nm) and later Intel devices have moved to a combination of LUT-RAM and a single medium-sized BRAM (20 kb) to simplify both the FPGA layout as well as RAM mapping and placement.

> Stratix V(28纳米)和后来的英特尔设备已经转向LUT-RAM和单个中型BRAM (20 kb)的组合，以简化FPGA布局以及RAM映射和放置。

Tatsumura et al. [52] plot a similar trend for on-chip memory density in Xilinx devices as well.

> Tatsumura等人[52]也在Xilinx设备的片上存储器密度上绘制了类似的趋势。

Similarly to Intel, Xilinx’s RAM architecture combines LUT-RAM and a medium-sized 18 kb RAM, but also includes hard circuitry to combine two BRAMs into a single 36 kb block.

> 与英特尔类似，赛灵思的RAM架构结合了LUT-RAM和一个中等大小的18kb RAM，但也包括将两个bram组合成一个36kb块的硬电路。

However, Xilinx’s most recent devices have also included a large 288 kb BRAM (UltraRAM) to be more efficient for very large buffers, showing that there is still no general agreement on the best BRAM architecture.

> 然而，赛灵思最新的设备还包括一个大的288 kb BRAM (UltraRAM)，以便在非常大的缓冲区中更有效，这表明对于最佳BRAM架构仍然没有普遍的共识。

---

To give some insight into the relative areas and efficiencies of different RAM blocks, Table II shows the resource usage, silicon area, and frequency of a 2048 × 72-bit logical RAM when it is implemented by Quartus (the CAD flow for Altera/Intel FPGAs) in a variety of ways on a Stratix IV device.

> 为了深入了解不同RAM块的相关面积和效率，表2显示了由Quartus (Altera/Intel fpga的CAD流程)以各种方式在Stratix IV设备上实现2048 × 72位逻辑RAM时的资源使用情况、硅面积和频率。

The silicon areas are computed using the published Stratix III block areas from [63] and scaling them from 65 nm down to 40 nm, as Stratix III and IV have the same architecture but use different process nodes.

> 硅面积是使用[63]中公布的Stratix III块面积计算的，并将它们从65 nm缩小到40 nm，因为Stratix III和IV具有相同的架构，但使用不同的工艺节点。

As this logical RAM is a perfect fit to the 144 kb BRAM in Stratix IV, it achieves the best area when mapped to a single 144 kb BRAM.

> 由于这个逻辑RAM非常适合Stratix IV中的144kb BRAM，因此当映射到单个144kb BRAM时，它可以实现最佳区域。

Interestingly, mapping to eighteen 9 kb BRAMs is only .1 9 # larger in silicon area (note that output width limitations lead to 18 BRAMs instead of the 16 one might expect).

> 有趣的是，映射到18个9 kb的bram在硅面积上只大了0.1 9 #(注意，输出宽度限制导致18个bram，而不是人们可能期望的16个)。

The 9 kb BRAM implementation is actually faster than the 144 kb BRAM implementation, as the smaller BRAMs have higher maximum operating frequencies.

> 9 kb的BRAM实现实际上比144 kb的BRAM实现更快，因为较小的BRAM具有更高的最大工作频率。

Mapping such a large logical RAM to LUT-RAMs is inefficient, requiring .12 7 # more area and running at 40% of the frequency.

> 将如此大的逻辑RAM映射到lut -RAM是低效的，需要0.12.7 #的面积，并以40%的频率运行。

Finally, mapping only to the logic and routing resources shows how important on-chip RAM is: area is over 300# larger than the 144 kb BRAM.

> 最后，仅映射到逻辑和路由资源显示了片上RAM的重要性:面积比144 kb的BRAM大300多#。

While the 144 kb BRAM is most efficient for this single test case, real designs have diverse logical RAMs, and for small or shallow memories the 9 kb and LUT-RAM options would outperform the 144 kb BRAM, motivating a diversity of on-chip RAM resources.

> 虽然144 kb的BRAM对于这个单一的测试用例是最有效的，但实际设计有多种逻辑RAM，对于小内存或浅内存，9 kb和LUT-RAM选项将优于144 kb BRAM，从而激发了片上RAM资源的多样性。

To choose the best mix of BRAM sizes and maximum word widths, one needs both a RAM mapping tool and tools to estimate the area, speed and power of each BRAM [55].

> 为了选择BRAM大小和最大字宽的最佳组合，我们既需要RAM映射工具，也需要估算每个BRAM的面积、速度和功率的工具[55]。

Published studies into BRAM architecture trade-offs for FPGAs include [30], [55], [64].

> 已发表的关于fpga的BRAM架构权衡的研究包括[30]，[55]，[64]。

---

Until now, all commercial FPGAs use only SRAM-based memory cells in their BRAMs.

> 到目前为止，所有商用fpga在其bram中仅使用基于sram的存储单元。

With the desire for more dense BRAMs that would enable more memory-rich FPGAs and SRAM scaling becoming increasingly difficult due to process variation, a few academic studies (e.g. [52], [65]) have explored the use of other emerging memory technologies such as magnetic tunnel junctions (MTJs) to build FPGA memory blocks.

> 由于对更密集的bram的渴望，这将使更多内存丰富的FPGA和SRAM缩放由于工艺变化而变得越来越困难，一些学术研究(例如[52]，[65])已经探索了使用其他新兴存储技术，如磁隧道结(MTJs)来构建FPGA存储块。

According to [52], MTJ-based BRAMs could increase the FPGA memory capac-ity by up to .2 9 5# with the same die size; however, they would increase the process complexity.

> 根据[52]，基于mtj的bram可以在相同芯片尺寸的情况下将FPGA内存容量增加高达0.2 9.5 #;然而，它们会增加流程的复杂性。

---

### E. DSP Blocks
