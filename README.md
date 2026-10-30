# Awesome Agentic Chip Design

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![Papers](https://img.shields.io/badge/papers-152-2563eb)](#contents)
[![Last updated](https://img.shields.io/badge/last_updated-2026--10--30-0f766e)](CHANGELOG.md)
[![Contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen)](CONTRIBUTING.md)
[![License: CC0](https://img.shields.io/badge/license-CC0_1.0-lightgrey)](LICENSE)

**A curated collection of research papers, benchmarks, code, and industrial resources on agentic chip design.**

Agentic chip design uses large language model (LLM) agents to plan design tasks, generate and revise hardware descriptions, invoke electronic design automation (EDA) tools, and refine designs using simulation, formal verification, synthesis, and physical-design feedback. This list covers digital, analog, mixed-signal, and radio-frequency (RF) design, together with agent architectures and EDA algorithm development.

**[Start reading](#start-reading)** · **[Browse papers](#contents)** · **[Explore industry](#industrial-systems-and-reports)** · **[Contribute](CONTRIBUTING.md)**

## Contents

Browse by design task, model capability, agent architecture, or evaluation setting.

- [Awesome Agentic Chip Design](#awesome-agentic-chip-design)
  - [Contents](#contents)
  - [Start Reading](#start-reading)
  - [Recent Papers](#recent-papers)
  - [Scope and Labels](#scope-and-labels)
  - [1. Foundations and Surveys](#1-foundations-and-surveys)
  - [2. Agentic Chip Design by Task](#2-agentic-chip-design-by-task)
    - [2.1. Digital Design](#21-digital-design)
      - [2.1.1. Specification, Architecture, and Hardware–Software Co-Design](#211-specification-architecture-and-hardwaresoftware-co-design)
      - [2.1.2. RTL Generation and Repository-Level Design](#212-rtl-generation-and-repository-level-design)
      - [2.1.3. Verification, Testbenches, Assertions, and Debugging](#213-verification-testbenches-assertions-and-debugging)
      - [2.1.4. RTL Optimization](#214-rtl-optimization)
      - [2.1.5. High-Level Synthesis and Design-Space Exploration](#215-high-level-synthesis-and-design-space-exploration)
      - [2.1.6. Logic Synthesis and Optimization Sequences](#216-logic-synthesis-and-optimization-sequences)
      - [2.1.7. Physical Design, Flow Tuning, and Timing Closure](#217-physical-design-flow-tuning-and-timing-closure)
    - [2.2. Analog, Mixed-Signal, and RF Design](#22-analog-mixed-signal-and-rf-design)
  - [3. Agent Architectures and Execution Systems](#3-agent-architectures-and-execution-systems)
    - [3.1. Domain Models and Learning](#31-domain-models-and-learning)
      - [3.1.1. Domain Adaptation and Engineering Knowledge](#311-domain-adaptation-and-engineering-knowledge)
      - [3.1.2. Data Construction and Generative Modeling](#312-data-construction-and-generative-modeling)
      - [3.1.3. Learning from EDA and Verification Feedback](#313-learning-from-eda-and-verification-feedback)
    - [3.2. Task Planning and Multi-Agent Tool Orchestration](#32-task-planning-and-multi-agent-tool-orchestration)
    - [3.3. Memory and Stateful Optimization](#33-memory-and-stateful-optimization)
    - [3.4. Tool Interfaces and Execution Infrastructure](#34-tool-interfaces-and-execution-infrastructure)
  - [4. EDA Algorithm Discovery and Tool Development](#4-eda-algorithm-discovery-and-tool-development)
    - [4.1. Logic Synthesis and Technology Mapping Algorithms](#41-logic-synthesis-and-technology-mapping-algorithms)
    - [4.2. Placement and Routing Algorithms](#42-placement-and-routing-algorithms)
    - [4.3. Repository-Level Tool Improvement and Research Workflows](#43-repository-level-tool-improvement-and-research-workflows)
  - [5. Benchmarks and Evaluation](#5-benchmarks-and-evaluation)
    - [5.1. RTL Generation and Repository Benchmarks](#51-rtl-generation-and-repository-benchmarks)
    - [5.2. Verification and Assertion Benchmarks](#52-verification-and-assertion-benchmarks)
    - [5.3. PPA, Physical Design, and Cross-Stage Closure Benchmarks](#53-ppa-physical-design-and-cross-stage-closure-benchmarks)
    - [5.4. Evaluation Methodology](#54-evaluation-methodology)
  - [6. Industrial Systems and Official Reports](#6-industrial-systems-and-official-reports)
    - [6.1. Established EDA Vendors](#61-established-eda-vendors)
      - [6.1.1. Synopsys](#611-synopsys)
      - [6.1.2. Cadence](#612-cadence)
      - [6.1.3. Siemens EDA](#613-siemens-eda)
    - [6.2. Startups and Emerging Platforms](#62-startups-and-emerging-platforms)
      - [6.2.1. ChipAgents](#621-chipagents)
      - [6.2.2. Cognichip](#622-cognichip)
      - [6.2.3. Chipmind](#623-chipmind)
      - [6.2.4. Ricursive Intelligence](#624-ricursive-intelligence)
  - [Contributing](#contributing)
  - [License](#license)

## Start Reading

| Your question                             | Start with                                                                                           | Then explore                                                                                                                       |
| ----------------------------------------- | ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| How does an agent actually use EDA tools? | [ChatEDA](#paper-2308-10204) → [ORFS-agent](#paper-2506-08332)                                       | [Orchestration and infrastructure](#eda-orchestration-and-infrastructure)                                                          |
| How do agents generate and debug RTL?     | [AutoChip](#paper-2311-04887) → [VerilogCoder](#paper-2408-08927) → [MAGE](#paper-2412-07822)        | [RTL generation](#rtl-generation)                                                                                                  |
| How is correctness checked?               | [RTLFixer](#paper-2311-16543) → [AssertLLM](#paper-2411-14436) → [FVEval](#paper-2410-23299)         | [Verification and debugging](#verification-and-debugging)                                                                          |
| Can agents improve PPA and timing?        | [RTLRewriter](#paper-2409-11414) → [AgenticPD](#paper-2607-04758) → [TicTacBench](#paper-2609-23363) | [RTL optimization](#rtl-and-hls-optimization), [HLS](#high-level-synthesis), and [physical design](#synthesis-and-physical-design) |
| Can agents improve EDA software itself?   | [AuDoPEDA](#paper-2601-06268) → [GR-Evolve](#paper-2604-22234) → [MappingEvolve](#paper-2604-26591)  | [Algorithm and tool development](#eda-algorithm-and-tool-development)                                                              |
| What changes for analog and RF circuits?  | [AnalogCoder](#paper-2405-14918) → [LEDRO](#paper-2411-12930) → [RFChipAgent](#paper-2610-10858)     | [Analog and mixed-signal design](#analog-and-mixed-signal)                                                                         |
| What is industry building and deploying?  | [Established EDA vendors](#established-eda-vendors) → [Startups](#startups-and-emerging-platforms)   | [Official technical blogs, product pages, and reports](#industrial-systems-and-reports)                                            |

For an introduction, start with [perspectives and surveys](#surveys), follow a reading path above, and consult the corresponding benchmarks.

## Recent Papers

Selected papers from October 2026. Dates refer to the initial paper version; collection updates are recorded in the [changelog](CHANGELOG.md).

| Paper date | Work                                         | Topic                                                     |
| ---------- | -------------------------------------------- | --------------------------------------------------------- |
| 2026-10    | [TACS-RF](#paper-2610-31882)                 | Tool-driven RF/mmWave circuit synthesis                  |
| 2026-10    | [CorrectRTL](#paper-2610-24977)              | Decomposed RTL generation and self-correction; ScaleBench |
| 2026-10    | [ArchAgent](#paper-2610-23724)               | Hierarchical heterogeneous-system exploration             |
| 2026-10    | [LATCH](#paper-2610-16625)                   | Post-route FPGA timing closure                            |
| 2026-10    | [RFChipAgent](#paper-2610-10858)             | Simulator-guided analog/RF design                         |
| 2026-10    | [Agentic research in EDA](#paper-2610-10129) | Algorithm-research case studies and validation            |
| 2026-10    | [Back to the Future](#paper-2610-06790)      | Trace databases and agentic verification                  |
| 2026-10    | [SparseCraft](#paper-2610-05037)             | Hardware–software co-optimization                         |

## Scope and Labels

**Agent** means an execution loop uses tool or environment feedback to choose subsequent actions. **Framework** denotes a system architecture or proposal whose integration scope should be checked in the source. **Method** covers techniques that support design without asserting an autonomous execution loop. **Model** identifies training or reusable generation capabilities. **Infrastructure** identifies tool interfaces and execution services; **Benchmark** identifies evaluation resources. **Survey** and **Perspective** identify reviews and viewpoints, respectively.

**Abbreviations:** RTL — register-transfer level; HDL — hardware description language; HLS — high-level synthesis; PPA — power, performance, and area; QoR — quality of results; LLM — large language model.

<a id="foundations-and-surveys"></a>

## 1. Foundations and Surveys

Start with perspectives and surveys on agentic chip design, LLM-based EDA, and circuit foundation models. These works introduce the research landscape and its connections to model capabilities and design workflows.

<a id="surveys"></a>

<a id="paper-2606-19795"></a>

- **[Agentic Electronic Design Automation: A Handoff Perspective](https://arxiv.org/abs/2606.19795)**
  `arXiv 2026-06` · `Perspective`
  Discusses the transfer of design intent, constraints, and verification results between stages of agentic EDA.

<a id="paper-2512-23189"></a>

- **[The Dawn of Agentic EDA: A Survey of Autonomous Digital Chip Design](https://arxiv.org/abs/2512.23189)**
  `arXiv 2025-12` · `Survey`
  An overview of autonomous digital chip design and the emerging agentic EDA landscape.

<a id="paper-2504-03711"></a>

- **[A Survey of Circuit Foundation Model: Foundation AI Models for VLSI Circuit Design and EDA](https://doi.org/10.1145/3827602)**
  `ACM TODAES 2026` · `Survey` · [Preprint](https://arxiv.org/abs/2504.03711)
  A map of circuit foundation models, connecting predictive circuit representations with generative design methods.

<a id="paper-2501-09655"></a>

- **[A Survey of Research in Large Language Models for Electronic Design Automation](https://doi.org/10.1145/3715324)**
  `ACM TODAES 2025` · `Survey` · [Preprint](https://arxiv.org/abs/2501.09655)
  A broad starting point for LLM applications across EDA tasks, datasets, and evaluation.

<a id="agentic-chip-design-tasks"></a>

## 2. Agentic Chip Design by Task

Locate a method by the hardware artifact or design decision it changes. Digital-design tasks follow the path from specifications to implementation; verification provides feedback throughout this path. Analog and RF design introduces topology, sizing, and layout decisions of its own.

<a id="digital-design"></a>

### 2.1. Digital Design

<a id="specification-and-architecture"></a>

#### 2.1.1. Specification, Architecture, and Hardware–Software Co-Design

<a id="paper-2610-23724"></a>

- **[Agentic AI for Heterogeneous System Design Across Chip, Scale-Up, and Scale-Out Domains](https://arxiv.org/abs/2610.23724)**
  `arXiv 2026-10` · `Agent`
  ArchAgent decomposes heterogeneous system design into chip, scale-up, and scale-out decisions evaluated by an analytical model.

<a id="paper-2610-05037"></a>

- **[SparseCraft: Agentic Hardware-Software Co-Optimization for Sparse Computing](https://arxiv.org/abs/2610.05037)**
  `arXiv 2026-10` · `Agent`
  SparseCraft revises Chisel RTL, memory configuration, and kernel schedules using elaboration, simulation, reference checking, and synthesis feedback.

<a id="paper-2603-02895"></a>

- **[SpecLoop: An Agentic RTL-to-Specification Framework with Formal Verification Feedback Loop](https://arxiv.org/abs/2603.02895)**
  `arXiv 2026-03` · `Agent`
  SpecLoop generates specifications from RTL, reconstructs RTL from those specifications, and uses formal-equivalence counterexamples to iteratively refine the documents.

<a id="paper-2506-05007"></a>

- **[QiMeng: Fully Automated Hardware and Software Design for Processor Chip](https://arxiv.org/abs/2506.05007)**
  `arXiv 2025-06` · `Framework`
  A processor hardware/software co-design framework built around domain models and design agents; the system proposal and integrated implementation should be read separately.

<a id="paper-2401-13266"></a>

- **[SpecLLM: Exploring Generation and Review of VLSI Design Specification with Large Language Model](https://doi.org/10.1109/iseda65950.2025.11100410)**
  `ISEDA 2025` · `Method` · [Preprint](https://arxiv.org/abs/2401.13266)
  Explores generating and reviewing architecture specifications, including deriving specification documents from RTL.

<a id="rtl-generation"></a>

#### 2.1.2. RTL Generation and Repository-Level Design

<a id="paper-2610-24977"></a>

- **[CorrectRTL: Boost RTL Generation Quality Through Automated Self-Correction with Instruction Decomposition](https://arxiv.org/abs/2610.24977)**
  `arXiv 2026-10` · `Agent`
  CorrectRTL separates scaffold construction from implementation and combines retrieval with SVA-based self-correction; also introduces ScaleBench.

<a id="paper-2606-28279"></a>

- **[Agentic Hardware Design as Repository-Level Code Evolution](https://arxiv.org/abs/2606.28279)**
  `arXiv 2026-06` · `Agent`
  HORIZON organizes hardware design as repository-level code evolution using executable evaluators, acceptance conditions, and versioned project packs.

<a id="paper-2603-17208"></a>

- **[SYMDIREC: A Neuro-Symbolic Divide-Retrieve-Conquer Framework for Enhanced RTL Synthesis and Summarization](https://doi.org/10.18653/v1/2026.eacl-industry.66)**
  `EACL Industry Track 2026` · `Framework` · [Preprint](https://arxiv.org/abs/2603.17208)
  SYMDIREC decomposes RTL tasks into symbolic subgoals, retrieves relevant code, and combines verified outputs through LLM reasoning for Verilog and VHDL generation and summarization.

<a id="paper-2603-08719"></a>

- **[SiliconMind-V1: Multi-Agent Distillation and Debug-Reasoning Workflows for Verilog Code Generation](https://doi.org/10.1109/compsac69091.2026.00023)**
  `COMPSAC 2026` · `Agent` · [Preprint](https://arxiv.org/abs/2603.08719)
  SiliconMind-V1 combines multi-agent training-data construction with testbench-driven, iterative RTL generation and debugging at inference time.

<a id="paper-2512-11398"></a>

- **[AutoFSM: A Multi-agent Framework for FSM Code Generation with IR and SystemC-Based Testing](https://doi.org/10.1007/978-981-95-4088-4_29)**
  `ICONIP 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2512.11398)
  AutoFSM coordinates agents around an intermediate representation translated into Verilog, with SystemC modeling and automatic testbench generation supporting debugging; also introduces SKT-FSM.

<a id="paper-doi-10-1109-aihcir67580-2025-11404766"></a>

- **[EDA-in-the-Loop: Automated HDL Code Generation and Verification Using Multi-Agent LLMs](https://doi.org/10.1109/aihcir67580.2025.11404766)**
  `AIHCIR 2025` · `Agent`
  EDA-in-the-Loop coordinates requirements, RTL, testbench, and debugging agents through AutoGen, using Vivado execution logs to guide iterative patches.

<a id="paper-2511-16395"></a>

- **[CorrectHDL: Agentic HDL Design with LLMs Leveraging High-Level Synthesis as Reference](https://arxiv.org/abs/2511.16395)**
  `arXiv 2025-11` · `Agent`
  Uses HLS-generated reference designs to guide simulation-based correction of HDL generated from C/C++ specifications.

<a id="paper-2511-02285"></a>

- **[VFocus: Better Verilog Generation from Large Language Model via Focused Reasoning](https://doi.org/10.1109/socc66126.2025.11235465)**
  `SOCC 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2511.02285)
  VFocus simulates generated RTL candidates, groups them by output consistency, and uses disagreements to focus subsequent LLM reasoning and code revision.

<a id="paper-2510-21407"></a>

- **[REvolution: An Evolutionary Framework for RTL Generation driven by Large Language Models](https://doi.org/10.1109/asp-dac66049.2026.11420420)**
  `ASP-DAC 2026` · `Agent` · [Preprint](https://arxiv.org/abs/2510.21407)
  REvolution evolves RTL candidates in separate populations for bug fixing and PPA optimization, using evaluation feedback and adaptive prompt selection.

<a id="paper-doi-10-1109-mlcad65511-2025-11189211"></a>

- **[Verilog Code Generation of Hierarchical Design Using LLMs](https://doi.org/10.1109/mlcad65511.2025.11189211)**
  `MLCAD 2025` · `Agent`
  Decomposes hierarchical designs from the top down and generates modules from the bottom up, feeding compilation and functional-simulation errors back to the LLM for revision.

<a id="paper-doi-10-1109-coins65080-2025-11125745"></a>

- **[Beyond Verilog: Agents for Emerging HDLs](https://doi.org/10.1109/coins65080.2025.11125745)**
  `COINS 2025` · `Agent`
  HDLAgent combines HDL description summaries with compiler-error feedback to generate and correct code in less-represented hardware description languages.

<a id="paper-2506-13905"></a>

- **[Spec2RTL-Agent: Automated Hardware Code Generation from Complex Specifications Using LLM Agent Systems](https://doi.org/10.1109/iclad65226.2025.00013)**
  `ICLAD 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2506.13905)
  Processes complex specifications through planning and progressive generation of synthesizable C++, then uses [HLS](#high-level-synthesis) to obtain RTL, with error reflection guiding revisions.

<a id="paper-doi-10-1145-3737286"></a>

- **[AutoSilicon: Scaling Up RTL Design Generation Capability of Large Language Models](https://doi.org/10.1145/3737286)**
  `ACM TODAES 2025` · `Agent`
  AutoSilicon decomposes complex RTL design tasks and generates and tests code fragments within an integrated compilation and simulation environment.

<a id="paper-doi-10-1145-3727980"></a>

- **[A data-centric chip design agent framework for Verilog code generation](https://doi.org/10.1145/3727980)**
  `ACM TODAES 2025` · `Agent`
  Combines Verilog and EDA-script data augmentation with an agent framework that iteratively filters RTL variants and uses EDA feedback and structured prompts to improve PPA.

<a id="paper-doi-10-23919-date64628-2025-10992751"></a>

- **[LLM4GV: An LLM-Based Flexible Performance-Aware Framework for GEMM Verilog Generation](https://doi.org/10.23919/date64628.2025.10992751)**
  `DATE 2025` · `Framework`
  LLM4GV uses a multi-agent LLM framework with hardware optimization and performance modeling to generate performance-aware Verilog implementations of GEMM modules.

<a id="paper-2501-05470"></a>

- **[RTLSquad: Multi-Agent Based Interpretable RTL Design](https://arxiv.org/abs/2501.05470)**
  `arXiv 2025-01` · `Agent`
  Uses cooperating agents to support interpretable RTL design and coordinated implementation.

<a id="paper-doi-10-1109-ats64447-2024-10915277"></a>

- **[RTL Agent: An Agent-Based Approach for Functionally Correct HDL Generation via LLMs](https://doi.org/10.1109/ats64447.2024.10915277)**
  `ATS 2024` · `Agent`
  RTL Agent applies Reflexion to Verilog generation, repeatedly generating code, executing testbenches, reflecting on feedback, and revising the design.

<a id="paper-doi-10-1109-ats64447-2024-10915239"></a>

- **[LLM-aided Front-End Design Framework For Early Development of Verified RTLs](https://doi.org/10.1109/ats64447.2024.10915239)**
  `ATS 2024` · `Agent`
  Coordinates RTL-generation, testbench-generation, and review LLMs, using simulation feedback to iteratively revise and debug generated designs.

<a id="paper-2412-07822"></a>

- **[MAGE: A Multi-Agent Engine for Automated RTL Code Generation](https://doi.org/10.1109/dac63849.2025.11133191)**
  `DAC 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2412.07822) · [Code](https://github.com/stable-lab/MAGE)
  Separates generation and debugging responsibilities and uses simulation-state checkpoints to locate functional errors.

<a id="paper-2412-05393"></a>

- **[HiVeGen – Hierarchical LLM-based Verilog Generation for Scalable Chip Design](https://doi.org/10.1109/iclad65226.2025.00031)**
  `ICLAD 2025` · `Method` · [Preprint](https://arxiv.org/abs/2412.05393)
  Generates hierarchical Verilog through submodule decomposition, hierarchy-aware prompting, and reusable code retrieval.

<a id="paper-2412-04485"></a>

- **[EDA-Aware RTL Generation with Large Language Models](https://doi.org/10.23919/date64628.2025.10992789)**
  `DATE 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2412.04485)
  AIvril2 coordinates LLM agents for RTL generation and self-verification, using EDA error logs to locate and iteratively repair syntax and functional defects.

<a id="paper-2411-11856"></a>

- **[Automatically Improving LLM-based Verilog Generation using EDA Tool Feedback](https://doi.org/10.1145/3723876)**
  `ACM TODAES 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2411.11856)
  A journal extension of [AutoChip](#paper-2311-04887), combining conversational LLM generation with compiler and simulation feedback to iteratively repair Verilog designs.

<a id="paper-2408-08927"></a>

- **[VerilogCoder: Autonomous Verilog Coding Agents with Graph-based Planning and Abstract Syntax Tree (AST)-based Waveform Tracing Tool](https://doi.org/10.1609/aaai.v39i1.32007)**
  `AAAI 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2408.08927) · [Code](https://github.com/NVlabs/VerilogCoder)
  Combines graph-based task planning with syntax checking, simulation, and AST-based waveform tracing.

<a id="paper-2311-04887"></a>

- **[AutoChip: Automating HDL Generation Using LLM Feedback](https://arxiv.org/abs/2311.04887)**
  `arXiv 2023-11` · `Agent` · [Code](https://github.com/shailja-thakur/AutoChip)
  An early feedback loop that revises generated Verilog using compiler diagnostics and simulation mismatches.

<a id="paper-2305-13243"></a>

- **[Chip-Chat: Challenges and Opportunities in Conversational Hardware Design](https://doi.org/10.1109/mlcad58807.2023.10299874)**
  `MLCAD 2023` · `Method` · [Preprint](https://arxiv.org/abs/2305.13243)
  A conversational hardware-design case study that motivates later tool-integrated design agents.

<a id="verification-and-debugging"></a>

#### 2.1.3. Verification, Testbenches, Assertions, and Debugging

These methods construct verification artifacts or diagnose design failures. Model training for stimulus generation is covered in [Section 3.1.3](#learning-from-eda-feedback).

<a id="paper-2610-06790"></a>

- **[Back to the Future: Rethinking EDA Infrastructure for Agentic Systems in Chip Design Verification](https://arxiv.org/abs/2610.06790)**
  `arXiv 2026-10` · `Agent`
  BTTF converts simulation traces into a relational database and combines schema-aware queries with versioned RTL analysis.

<a id="paper-2609-34785"></a>

- **[BEHAVE: Functional Behavior Modeling Enables Self-Improving Agents for Hardware Design and Verification](https://arxiv.org/abs/2609.34785)**
  `arXiv 2026-09` · `Agent / Model`
  Jointly develops RTL and executable behavior models, using a hidden reference evaluator for verification and learning.

<a id="paper-2607-26181"></a>

- **[GoGoTB: Agentic RTL Verification with Specification-Grounded Coverage Closure](https://arxiv.org/abs/2607.26181)**
  `arXiv 2026-07` · `Agent`
  Connects verification-environment generation with specification-grounded coverage analysis and targeted closure.

<a id="paper-doi-10-1145-3770743-3804231"></a>

- **[ReflectBench: An Agentic Framework for Generating System-Level Design Testbench via Consensus and Reflection](https://doi.org/10.1145/3770743.3804231)**
  `DAC 2026` · `Agent` · [Code](https://gitee.com/sdu-aes-lab/reflectbench)
  ReflectBench combines consensus validation, self-reflection, and functional correction for system-level testbench generation; the paper also introduces ReflectVDB.

<a id="paper-2607-01668"></a>

- **[VeriChat: An Agentic Conversational AI Assistant for Hardware Security Verification](https://doi.org/10.1109/coins69995.2026.11715649)**
  `COINS 2026` · `Agent` · [Preprint](https://arxiv.org/abs/2607.01668)
  VeriChat combines retrieval and specialized agents with Icarus Verilog, Yosys, and SymbiYosys for conversational RTL security analysis, simulation, and formal verification.

<a id="paper-doi-10-23919-date69613-2026-11539733"></a>

- **[ChatTest: Coverage-Enhanced Testbench Generation for Agile Hardware Verification with LLMs](https://doi.org/10.23919/date69613.2026.11539733)**
  `DATE 2026` · `Agent`
  ChatTest decomposes verification specifications into functional points, generates directed stimuli with cooperating agents, and adds tests in response to coverage reports.

<a id="paper-doi-10-1109-vlsitsa69131-2026-11527986"></a>

- **[SHARP: A Comprehensive SystemC HLS Benchmark Suite and LLM-Assisted Testbench Optimization for RTL Coverage Closure](https://doi.org/10.1109/vlsitsa69131.2026.11527986)**
  `VLSI TSA 2026` · `Agent`
  SHARP pairs a SystemC HLS benchmark with an LLM-assisted workflow that analyzes RTL coverage gaps and synthesis artifacts to iteratively refine testbenches.

<a id="paper-doi-10-1109-vlsitsa69131-2026-11527768"></a>

- **[FLAIR: A Framework for LLM-Driven Assertion Generation and Incremental Refinement](https://doi.org/10.1109/vlsitsa69131.2026.11527768)**
  `VLSI TSA 2026` · `Agent`
  FLAIR integrates an LLM with JasperGold for assertion generation; its reactive workflow refines assertions using formal feedback, while its proactive workflow enriches the input prompts.

<a id="paper-2604-23100"></a>

- **[From Language to Logic: Bridging LLMs & Formal Representations for RTL Assertion Generation](https://doi.org/10.1109/vts69484.2026.11563398)**
  `VTS 2026` · `Agent` · [Preprint](https://arxiv.org/abs/2604.23100)
  ProofLoop gathers RTL context through retrieval and JasperGold queries, then iteratively refines generated SystemVerilog assertions using formal proof feedback.

<a id="paper-2604-06607"></a>

- **[CoverAssert: Iterative LLM Assertion Generation Driven by Functional Coverage via Syntax-Semantic Representations](https://doi.org/10.23919/date69613.2026.11539151)**
  `DATE 2026` · `Agent` · [Preprint](https://arxiv.org/abs/2604.06607)
  CoverAssert combines semantic and AST-based assertion representations with specification mapping to guide iterative assertion generation through functional-coverage feedback. See also the [ETS publication](#paper-2602-15388) on CoverAssert.

<a id="paper-2602-15388"></a>

- **[Iterative LLM-Based Assertion Generation Using Syntax–Semantic Representations for Functional Coverage–Guided Verification](https://doi.org/10.1109/ets69887.2026.11591998)**
  `ETS 2026` · `Agent` · [Preprint](https://arxiv.org/abs/2602.15388)
  CoverAssert maps semantic and AST-based assertion representations to specification features and uses functional-coverage feedback to prioritize missing assertions. See also the [DATE publication](#paper-2604-06607) on CoverAssert.

<a id="paper-doi-10-1145-3773087"></a>

- **[ConfiBench: Automatic Testbench Generation with Confidence-Based Scenario Mask and Testbench Ensemble using LLMs for HDL Design](https://doi.org/10.1145/3773087)**
  `ACM TODAES 2026` · `Agent` · [Code](https://github.com/AutoBench/ConfiBench)
  ConfiBench combines functional self-validation and correction with confidence-based scenario masking and testbench ensembles to improve generated HDL testbenches.

<a id="paper-doi-10-1109-mlcad65511-2025-11189172"></a>

- **[LLM-assisted Path Exploration for RTL Verification](https://doi.org/10.1109/mlcad65511.2025.11189172)**
  `MLCAD 2025` · `Agent`
  Uses RTL structure and dynamic simulation information to guide LLM path selection within concolic testing for branch-coverage improvement.

<a id="paper-2508-05266"></a>

- **[Understanding and Mitigating Errors of LLM-Generated RTL Code](https://doi.org/10.1109/tcad.2026.3661446)**
  `IEEE TCAD 2026` · `Agent` · [Preprint](https://arxiv.org/abs/2508.05266)
  Combines retrieval, specification checking, and input conversion with an iterative simulation-debugging loop to diagnose and correct LLM-generated RTL errors.

<a id="paper-doi-10-1109-isvlsi65124-2025-11130226"></a>

- **[LISA: LLM Informed Systemverilog Assertion generation with RAG and Chain-of-Thought](https://doi.org/10.1109/isvlsi65124.2025.11130226)**
  `ISVLSI 2025` · `Agent`
  LISA combines specification decomposition, retrieval, and chain-of-thought reasoning for assertion generation, with formal verification, coverage analysis, and human guidance supporting iterative refinement.

<a id="paper-2507-02660"></a>

- **[Hey AI, Generate Me a Hardware Code! Agentic AI-based Hardware Design & Verification](https://doi.org/10.1109/sbcci66862.2025.11218681)**
  `SBCCI 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2507.02660)
  Studies agentic hardware design and verification through iterative refinement, self-reflection, and human participation, with evaluation on open-source designs.

<a id="paper-2506-12200"></a>

- **[PRO-V-R1: Reasoning Enhanced Programming Agent for RTL Verification](https://doi.org/10.1145/3770743.3803912)**
  `DAC 2026` · `Agent` · [Preprint](https://arxiv.org/abs/2506.12200)
  PRO-V-R1 couples LLM reasoning with programmatic tool use for autonomous RTL verification, using simulation-validated training trajectories and verification-specific rewards.

<a id="paper-2506-10501"></a>

- **[BugGen: A Self-Correcting Multi-Agent LLM Pipeline for Realistic RTL Bug Synthesis](https://doi.org/10.1109/mlcad65511.2025.11189127)**
  `MLCAD 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2506.10501)
  Synthesizes realistic RTL bugs through a self-correcting multi-agent pipeline for verification evaluation.

<a id="paper-2505-11963"></a>

- **[MARVEL: Multi-Agent RTL Vulnerability Extraction using Large Language Models](https://doi.org/10.1145/3832325)**
  `ACM TODAES 2026` · `Agent` · [Preprint](https://arxiv.org/abs/2505.11963)
  MARVEL uses a supervisor to plan security checks and executor agents to run formal verification, linting, simulation, and static analysis, then reviews the reported RTL vulnerabilities.

<a id="paper-doi-10-1109-isqed65160-2025-11014349"></a>

- **[Automated Verilog Assertion Generation Using Fine-Tuned LLMs with Subtask-Specific Iterative Prompting](https://doi.org/10.1109/isqed65160.2025.11014349)**
  `ISQED 2025` · `Agent`
  AssertCraft combines fine-tuning with subtask-specific iterative prompting, using compiler diagnostics to correct generated Verilog assertions.

<a id="paper-2504-19959"></a>

- **[From Concept to Practice: an Automated LLM-aided UVM Machine for RTL Verification](https://doi.org/10.1109/iccad66269.2025.11240679)**
  `ICCAD 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2504.19959)
  Generates UVM verification environments with LLMs and iteratively revises testbenches using code- and functional-coverage feedback.

<a id="paper-doi-10-70456-twnx3992"></a>

- **[A DYNAMIC MULTI-AGENT SYSTEM FOR COVERAGE-BASED TESTBENCH SYNTHESIS IN SYSTEMVERILOG](https://doi.org/10.70456/twnx3992)**
  `UNITECH Selected Papers 2025` · `Agent`
  Coordinates specification parsing, testbench and stimulus generation, and coverage monitoring through specialized LLM agents, using cocotb and Verilator for iterative verification.

<a id="paper-2411-08510"></a>

- **[CorrectBench: Automatic Testbench Generation with Functional Self-Correction using LLMs for HDL Design](https://doi.org/10.23919/date64628.2025.10992873)**
  `DATE 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2411.08510) · [Code](https://github.com/AutoBench/CorrectBench)
  CorrectBench generates HDL testbenches and uses defect information from functional self-validation to drive LLM-based testbench correction.

<a id="paper-2411-14436"></a>

- **[AssertLLM: Generating Hardware Verification Assertions from Design Specifications via Multi-LLMs](https://doi.org/10.1145/3658617.3697756)**
  `ASP-DAC 2025` · `Method` · [Preprint](https://arxiv.org/abs/2411.14436)
  Generates hardware assertions from specification text and waveform diagrams using structured intermediate descriptions.

<a id="paper-doi-10-1145-3649329-3663498"></a>

- **[Late Breaking Results: LLM-assisted Automated Incremental Proof Generation for Hardware Verification](https://doi.org/10.1145/3649329.3663498)**
  `DAC 2024` · `Agent`
  Uses LLMs to plan incremental module-level hardware proofs, define and verify invariants with Z3, and formulate integration properties as the proof scope expands.

<a id="paper-2406-04373"></a>

- **[VerilogReader: LLM-Aided Hardware Test Generation](https://doi.org/10.1109/lad62341.2024.10691801)**
  `LAD 2024` · `Agent` · [Preprint](https://arxiv.org/abs/2406.04373)
  VerilogReader embeds LLM analysis in coverage-directed test generation to produce stimuli targeting unexplored RTL branches.

<a id="paper-2405-06840"></a>

- **[MEIC: Re-thinking RTL Debug Automation using LLMs](https://doi.org/10.1145/3676536.3676801)**
  `ICCAD 2024` · `Agent` · [Preprint](https://arxiv.org/abs/2405.06840)
  Iteratively diagnoses and repairs RTL syntax and functional errors with LLM-guided debugging.

<a id="paper-2311-16543"></a>

- **[RTLFixer: Automatically Fixing RTL Syntax Errors with Large Language Model](https://doi.org/10.1145/3649329.3657353)**
  `DAC 2024` · `Agent` · [Preprint](https://arxiv.org/abs/2311.16543) · [Code](https://github.com/NVlabs/RTLFixer)
  Uses retrieval and interactive compiler feedback to repair Verilog syntax errors.

<a id="rtl-and-hls-optimization"></a>

#### 2.1.4. RTL Optimization

<a id="paper-2606-06530"></a>

- **[RTLScout: Joint Agentic Code and Synthesis Optimization for Efficient Digital Circuits](https://arxiv.org/abs/2606.06530)**
  `arXiv 2026-06` · `Agent`
  RTLScout jointly refines RTL, logic-synthesis choices, and arithmetic architectures, using Yosys and OpenROAD delay and area feedback through the Spire HDL.

<a id="paper-2606-05253"></a>

- **[Alpha-RTL: Test-Time Training for RTL Hardware Optimization](https://arxiv.org/abs/2606.05253)**
  `arXiv 2026-06` · `Method`
  Studies test-time training for RTL optimization, complementing approaches that search with fixed model weights.

<a id="paper-2603-17613"></a>

- **[VeriAgent: A Tool-Integrated Multi-Agent System with Evolving Memory for PPA-Aware RTL Code Generation](https://arxiv.org/abs/2603.17613)**
  `arXiv 2026-03` · `Agent`
  Coordinates RTL generation, simulation, PPA analysis, and evolving memory through a tool-integrated multi-agent system.

<a id="paper-2603-17204"></a>

- **[CODMAS: A Dialectic Multi-Agent Collaborative Framework for Structured RTL Optimization](https://doi.org/10.18653/v1/2026.eacl-industry.57)**
  `EACL Industry Track 2026` · `Agent` · [Preprint](https://arxiv.org/abs/2603.17204)
  Uses structured discussion, domain-aware code edits, and deterministic evaluation for pipelining and clock-gating transformations.

<a id="paper-doi-10-1109-mlcad65511-2025-11189222"></a>

- **[ASPEN: LLM-Guided E-Graph Rewriting for RTL Datapath Optimization](https://doi.org/10.1109/mlcad65511.2025.11189222)**
  `MLCAD 2025` · `Agent`
  ASPEN uses an LLM agent to propose and select e-graph rewrite rules, with EDA-derived PPA feedback guiding equivalent RTL datapath optimization.

<a id="paper-2508-08709"></a>

- **[CRADLE: Conversational RTL Design Space Exploration with LLM-Based Multi-Agent Systems](https://doi.org/10.1109/isocc66390.2025.11329873)**
  `ISOCC 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2508.08709)
  CRADLE combines generator and critic agents with user guidance for RTL self-validation, correction, and FPGA resource optimization.

<a id="paper-2507-14776"></a>

- **[VeriOpt: PPA-Aware High-Quality Verilog Generation via Multi-Role LLMs](https://doi.org/10.1109/iccad66269.2025.11240771)**
  `ICCAD 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2507.14776)
  VeriOpt coordinates planning, coding, review, and evaluation roles, using synthesis reports and timing graphs to guide functional and PPA optimization.

<a id="paper-2504-10369"></a>

- **[SymRTLO: Enhancing RTL Code Optimization with LLMs and Neuron-Inspired Symbolic Reasoning](https://doi.org/10.52202/085713-1670)**
  `NeurIPS 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2504.10369)
  Combines RTL rewriting with AST templates, symbolic FSM reasoning, and formal-equivalence checks.

<a id="paper-2409-11414"></a>

- **[RTLRewriter: Methodologies for Large Models aided RTL Code Optimization](https://doi.org/10.1145/3676536.3676775)**
  `ICCAD 2024` · `Agent` · [Preprint](https://arxiv.org/abs/2409.11414) · [Code](https://github.com/yaoxufeng/RTLRewriter-Bench)
  Combines circuit partitioning, retrieved optimization guidance, cost-aware search, and verification for RTL rewriting.

<a id="high-level-synthesis"></a>

#### 2.1.5. High-Level Synthesis and Design-Space Exploration

<a id="paper-2602-09919"></a>

- **[LLM4PQC - Accurate and Efficient Synthesis of PQC Cores by Feedback-Driven LLMs](https://doi.org/10.23919/date69613.2026.11539440)**
  `DATE 2026` · `Framework` · [Preprint](https://arxiv.org/abs/2602.09919)
  LLM4PQC refactors post-quantum cryptography reference C code into synthesizable HLS code and checks generated implementations through C compilation, C simulation, and RTL simulation.

<a id="paper-2602-06085"></a>

- **[LAAFD: LLM-based Agents for Accelerated FPGA Design](https://doi.org/10.1615/jmachlearnmodelcomput.2026064494)**
  `Journal of Machine Learning for Modeling and Computing 2026` · `Agent` · [Preprint](https://arxiv.org/abs/2602.06085)
  LAAFD optimizes C++ kernels for Vitis HLS through pipelining, vectorization, and dataflow partitioning, using co-simulation and synthesis feedback to refine performance.

<a id="paper-doi-10-1145-3747291"></a>

- **[High-level Synthesis Directives Design Optimization via Large Language Model](https://doi.org/10.1145/3747291)**
  `ACM TODAES 2025` · `Framework`
  Uses LLMs as feature extractors and agents to explore HLS directive configurations and prioritize search strategies for design-space optimization.

<a id="paper-2507-00642"></a>

- **[ChatHLS: Towards Systematic Design Automation and Optimization for High-Level Synthesis](https://doi.org/10.18653/v1/2026.acl-long.962)**
  `ACL 2026` · `Agent` · [Preprint](https://arxiv.org/abs/2507.00642)
  Combines HLS error diagnosis with directive tuning and QoR-aware reasoning.

<a id="paper-2505-22086"></a>

- **[iDSE: Navigating Design Space Exploration in High-Level Synthesis Using LLMs](https://arxiv.org/abs/2505.22086)**
  `arXiv 2025-05` · `Method`
  Uses LLM-guided sampling and refinement to explore HLS directive configurations and Pareto trade-offs.

<a id="paper-2412-00214"></a>

- **[C2HLSC: Leveraging Large Language Models to Bridge the Software-to-Hardware Design Gap](https://doi.org/10.1145/3734524)**
  `ACM TODAES 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2412.00214)
  C2HLSC iteratively refactors C code using HLS tool feedback and processes complex designs hierarchically to obtain synthesizable implementations.

<a id="paper-2408-06810"></a>

- **[HLSPilot: LLM-based High-Level Synthesis](https://doi.org/10.1145/3676536.3676781)**
  `ICCAD 2024` · `Method` · [Preprint](https://arxiv.org/abs/2408.06810) · [Code](https://github.com/xcw-1010/HLSPilot)
  Translates and optimizes C/C++ for HLS using profiling, in-context transformation strategies, and directive exploration.

<a id="logic-synthesis"></a>

#### 2.1.6. Logic Synthesis and Optimization Sequences

Agents choose synthesis operations using tool feedback. Changes to synthesis algorithms appear in [Section 4.1](#synthesis-and-mapping-algorithms).

<a id="paper-2608-12751"></a>

- **[SynAct: A Reasoning-Acting Large Language Model Agent for Adaptive Synthesis Optimization](https://arxiv.org/abs/2608.12751)**
  `arXiv 2026-08` · `Agent`
  Selects synthesis actions through a reasoning–acting loop grounded in tool reports.

<a id="synthesis-and-physical-design"></a>

#### 2.1.7. Physical Design, Flow Tuning, and Timing Closure

<a id="paper-2610-16625"></a>

- **[LATCH: LLM-Assisted Timing Closure Harness for Post-Route FPGA Optimisation](https://arxiv.org/abs/2610.16625)**
  `arXiv 2026-10` · `Agent`
  LATCH studies recipe selection, direct operations, and branching exploration for post-route FPGA timing optimization.

<a id="paper-2607-04758"></a>

- **[AgenticPD: A Stage-Aware Agentic Framework for Closed-Loop Physical Design Optimization](https://arxiv.org/abs/2607.04758)**
  `arXiv 2026-07` · `Agent`
  Uses a coordinating judge and stage-specialized agents to optimize physical design through stage-local tool feedback.

<a id="paper-doi-10-1109-iccsp68173-2026-11539254"></a>

- **[ChipGPT: Leveraging Large Language Models for Automated and Optimized Soc Floorplanning](https://doi.org/10.1109/iccsp68173.2026.11539254)**
  `ICCSP 2026` · `Agent`
  ChipGPT iteratively adjusts SoC floorplans from netlists, macro properties, and constraints, using wirelength, area, and congestion estimates from a cost engine.

<a id="paper-2507-02128"></a>

- **[CROP: Circuit Retrieval and Optimization with Parameter Guidance using LLMs](https://doi.org/10.1109/iccad66269.2025.11240643)**
  `ICCAD 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2507.02128)
  CROP retrieves semantically similar circuits and uses their configuration priors to guide LLM-based EDA parameter search for design-flow tuning.

<a id="paper-2506-08332"></a>

- **[ORFS-agent: Tool-Using Agents for Chip Design Optimization](https://doi.org/10.1109/mlcad65511.2025.11189204)**
  `MLCAD 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2506.08332) · [Code](https://github.com/ABKGroup/ORFS-Agent)
  Tunes OpenROAD flow parameters using iterative tool execution and design-quality feedback.

<a id="paper-2504-11502"></a>

- **[Timing Analysis Agent: Autonomous Multi-Corner Multi-Mode (MCMM) Timing Debugging with Timing Debug Relation Graph](https://arxiv.org/abs/2504.11502)**
  `arXiv 2025-04` · `Agent`
  Uses a timing-debug relation graph to support autonomous multi-corner, multi-mode timing analysis and debugging.

<a id="paper-2406-06549"></a>

- **[Large Language Model (LLM) for Standard Cell Layout Design Optimization](https://doi.org/10.1109/lad62341.2024.10691722)**
  `LAD 2024` · `Agent` · [Preprint](https://arxiv.org/abs/2406.06549)
  Uses ReAct prompting to incrementally generate device-clustering constraints for standard-cell layout PPA optimization and routability debugging.

<a id="analog-and-mixed-signal"></a>

### 2.2. Analog, Mixed-Signal, and RF Design

Tasks span circuit generation, simulator-guided sizing, interactive layout, and coordinated RF design. Reusable analog topology models appear in [Section 3.1.2](#data-and-generative-modeling).

<a id="paper-2610-31882"></a>

- **[TACS-RF: Tool-driven Agentic Circuit Synthesis of RF and mmWave Modules](https://arxiv.org/abs/2610.31882)**
  `arXiv 2026-10` · `Agent`
  TACS-RF uses an LLM coding agent to operate circuit, layout-verification, and electromagnetic tools for RF/mmWave module design under human supervision.

<a id="paper-2610-10858"></a>

- **[RFChipAgent: Multi-Agentic AI Flow for Analog/RF Chip Design](https://arxiv.org/abs/2610.10858)**
  `arXiv 2026-10` · `Agent`
  Combines document retrieval, topology selection, schematic/testbench construction, and simulator-guided RF circuit sizing under human supervision.

<a id="paper-2603-23910"></a>

- **[AnalogAgent: Self-Improving Analog Circuit Design Automation with LLM Agents](https://doi.org/10.1145/3770855.3818993)**
  `KDD 2026` · `Agent` · [Preprint](https://arxiv.org/abs/2603.23910)
  Coordinates generation, optimization, and knowledge curation with an evolving memory for analog circuit design.

<a id="paper-2602-02849"></a>

- **[AutoSizer: Automatic Sizing of Analog and Mixed-Signal Circuits via Large Language Model (LLM) Agents](https://arxiv.org/abs/2602.02849)**
  `arXiv 2026-02` · `Agent`
  Uses an outer reflective loop to adapt a simulator-driven sizing search; also introduces AMS-SizingBench.

<a id="paper-doi-10-1109-tcad-2026-3673493"></a>

- **[AnalogCoder-Pro: Unifying Analog Circuit Generation and Optimization via Multi-modal LLMs](https://doi.org/10.1109/tcad.2026.3673493)**
  `IEEE TCAD 2026` · `Agent`
  AnalogCoder-Pro extends [AnalogCoder](#paper-2405-14918) with multimodal diagnosis of simulation errors and waveforms, Bayesian sizing optimization, and a reusable library of successful subcircuits.

<a id="paper-2512-21613"></a>

- **[AMS-IO-Bench and AMS-IO-Agent: Benchmarking and Structured Reasoning for Analog and Mixed-Signal Integrated Circuit Input/Output Design](https://doi.org/10.1609/aaai.v40i2.37134)**
  `AAAI 2026` · `Agent / Benchmark` · [Preprint](https://arxiv.org/abs/2512.21613)
  AMS-IO-Agent translates analog/mixed-signal I/O design intent into structured JSON and Python representations; AMS-IO-Bench evaluates the associated I/O-ring design tasks.

<a id="paper-2511-03697"></a>

- **[(Invited Paper) AnaFlow: Agentic LLM-based Workflow for Reasoning-Driven Explainable and Sample-Efficient Analog Circuit Sizing](https://doi.org/10.1109/iccad66269.2025.11240818)**
  `ICCAD 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2511.03697)
  Coordinates circuit interpretation and parameter refinement with an adaptive simulation strategy for analog sizing.

<a id="paper-2510-17002"></a>

- **[EEschematic: Multimodal-LLM Based AI Agent for Schematic Generation of Analog Circuit](https://doi.org/10.1109/iscas66217.2026.11562002)**
  `ISCAS 2026` · `Agent` · [Preprint](https://arxiv.org/abs/2510.17002)
  EEschematic converts SPICE netlists into editable analog schematics, using multimodal reasoning and visual chain-of-thought to iteratively refine component placement and wiring.

<a id="paper-2509-25510"></a>

- **[EEsizer: LLM-Based AI Agent for Sizing of Analog and Mixed Signal Circuit](https://doi.org/10.1109/tcsi.2025.3646359)**
  `IEEE TCAS-I 2026` · `Agent` · [Preprint](https://arxiv.org/abs/2509.25510)
  EEsizer combines an LLM, circuit simulators, and data-analysis functions for iterative transistor sizing, extending the authors' [NEWCAS study](#paper-2504-11497) with broader circuit and model evaluation.

<a id="paper-doi-10-1109-dac63849-2025-11133334"></a>

- **[Multi-Agent Yield Analysis For Circuit Design](https://doi.org/10.1109/dac63849.2025.11133334)**
  `DAC 2025` · `Agent`
  Uses a three-level LLM-agent architecture to coordinate circuit-yield analysis strategies, retrieve domain knowledge, and tune estimation-method hyperparameters.

<a id="paper-doi-10-1109-tcad-2025-3573228"></a>

- **[Atelier: An Automated Analog Circuit Design Framework via Multiple Large Language Model-Based Agents](https://doi.org/10.1109/tcad.2025.3573228)**
  `IEEE TCAD 2026` · `Agent`
  Atelier coordinates LLM agents for circuit analysis, topology selection and modification, and sizing through graph-of-thoughts reasoning, tool integration, reflection, and backtracking.

<a id="paper-2505-06364"></a>

- **[LATENT: LLM-Augmented Trojan Insertion and Evaluation Framework for Analog Netlist Topologies](https://doi.org/10.1109/iclad65226.2025.00040)**
  `ICLAD 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2505.06364)
  LATENT uses an LLM to insert and revise hardware Trojans in analog netlists, adapting the modifications through iterative feedback from a detection model.

<a id="paper-doi-10-1109-aicas64808-2025-11173131"></a>

- **[Circuit-Agent: A Large Language Model Based Circuit Agent Framework for Analog/Mixed-signal Circuit Design Automation](https://doi.org/10.1109/aicas64808.2025.11173131)**
  `AICAS 2025` · `Agent`
  Circuit-Agent combines circuit retrieval-augmented generation with cooperating LLM agents for analog and mixed-signal circuit generation, including operational amplifiers and ADCs.

<a id="paper-2504-11497"></a>

- **[LLM-Based AI Agent for Sizing of Analog and Mixed Signal Circuit](https://doi.org/10.1109/newcas64648.2025.11107079)**
  `NEWCAS 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2504.11497)
  Integrates LLM agents with circuit simulators and data-analysis functions for transistor sizing toward target specifications. The related [EEsizer journal study](#paper-2509-25510) expands the evaluation.

<a id="paper-2412-19824"></a>

- **[AnalogXpert: Automating Analog Topology Synthesis by Incorporating Circuit Design Expertise into Large Language Models](https://doi.org/10.1109/iseda65950.2025.11100627)**
  `ISEDA 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2412.19824)
  AnalogXpert decomposes analog topology synthesis into subcircuit selection and connection, using a subcircuit library and incremental proofreading to correct generated SPICE designs.

<a id="paper-2411-12930"></a>

- **[LEDRO: LLM-Enhanced Design Space Reduction and Optimization for Analog Circuits](https://doi.org/10.1109/iclad65226.2025.00011)**
  `ICLAD 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2411.12930)
  Combines LLM-based design-space reduction with iterative numerical optimization for analog circuit sizing.

<a id="paper-2411-13560"></a>

- **[AMSnet-KG: A Netlist Dataset for LLM-based AMS Circuit Auto-design Using Knowledge Graph RAG](https://doi.org/10.1145/3736166)**
  `ACM TODAES 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2411.13560) · [Project](https://ams-net.github.io/)
  AMSnet-KG combines a circuit knowledge graph with LLM-based topology planning and retrieval, Bayesian transistor sizing, and simulation feedback for iterative topology refinement.

<a id="paper-2406-18873"></a>

- **[LayoutCopilot: An LLM-Powered Multiagent Collaborative Framework for Interactive Analog Layout Design](https://doi.org/10.1109/tcad.2025.3529805)**
  `IEEE TCAD 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2406.18873)
  Translates designer instructions into tool operations through a multi-agent interactive analog-layout assistant.

<a id="paper-2406-18770"></a>

- **[ADO-LLM: Analog Design Bayesian Optimization with In-Context Learning of Large Language Models](https://doi.org/10.1145/3676536.3676816)**
  `ICCAD 2024` · `Agent` · [Preprint](https://arxiv.org/abs/2406.18770)
  ADO-LLM alternates LLM-proposed analog sizing points with Bayesian optimization, using evaluated designs as in-context demonstrations for subsequent proposals.

<a id="paper-2405-14918"></a>

- **[AnalogCoder: Analog Circuit Design via Training-Free Code Generation](https://doi.org/10.1609/aaai.v39i1.32016)**
  `AAAI 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2405.14918)
  Generates analog circuits through Python code, execution feedback, and a library of reusable subcircuits.

<a id="eda-orchestration-and-infrastructure"></a>

## 3. Agent Architectures and Execution Systems

This section organizes the capabilities and mechanisms that connect models to design work: domain models and learning, task decomposition and tool coordination, persistent experience, and execution interfaces. These capabilities and mechanisms support the tasks in Section 2.

<a id="models-and-training"></a>

### 3.1. Domain Models and Learning

This section follows how models acquire circuit knowledge and generation capabilities: domain adaptation, data construction, and learning from executable feedback. These capabilities can support agents across multiple design tasks.

<a id="domain-adaptation"></a>

#### 3.1.1. Domain Adaptation and Engineering Knowledge

<a id="paper-2311-00176"></a>

- **[ChipNeMo: Domain-Adapted LLMs for Chip Design](https://arxiv.org/abs/2311.00176)**
  `arXiv 2023-10` · `Model`
  Studies chip-domain adaptation for engineering assistance, EDA scripting, and bug summarization.

<a id="data-and-generative-modeling"></a>

#### 3.1.2. Data Construction and Generative Modeling

<a id="paper-2503-00205"></a>

- **[AnalogGenie: A Generative Engine for Automatic Discovery of Analog Circuit Topologies](https://openreview.net/forum?id=jCPak79Kev)**
  `ICLR 2025` · `Model` · [Preprint](https://arxiv.org/abs/2503.00205) · [Code](https://github.com/xz-group/AnalogGenie)
  AnalogGenie learns a sequence-based circuit-graph representation for analog topology generation.

<a id="paper-2407-16237"></a>

- **[OriGen: Enhancing RTL Code Generation with Code-to-Code Augmentation and Self-Reflection](https://doi.org/10.1145/3676536.3676830)**
  `ICCAD 2024` · `Model` · [Preprint](https://arxiv.org/abs/2407.16237)
  Uses code-to-code data augmentation and compiler-guided self-reflection for RTL generation.

<a id="paper-2407-10424"></a>

- **[CodeV: Empowering LLMs with HDL Generation through Multi-Level Summarization](https://arxiv.org/abs/2407.10424)**
  `arXiv 2024-07` · `Model`
  Uses multi-level code summarization and instruction tuning for HDL generation and infilling.

<a id="paper-2312-08617"></a>

- **[RTLCoder: Fully Open-Source and Efficient LLM-Assisted RTL Code Generation Technique](https://doi.org/10.1109/tcad.2024.3483089)**
  `IEEE TCAD 2025` · `Model` · [Preprint](https://arxiv.org/abs/2312.08617) · [Code](https://github.com/hkust-zhiyao/RTL-Coder)
  An open RTL generation model and dataset that provide a useful baseline for hardware-specialized LLMs.

<a id="learning-from-eda-feedback"></a>

#### 3.1.3. Learning from EDA and Verification Feedback

<a id="paper-2608-10090"></a>

- **[CHORUS: Complementary Experts for High-Coverage Testbench Stimulus Generation](https://arxiv.org/abs/2608.10090)**
  `arXiv 2026-08` · `Model`
  A post-training and expert-consolidation approach for testbench stimulus generation and coverage improvement.

<a id="paper-2507-04736"></a>

- **[ChipSeek: Optimizing Verilog Generation via EDA-Integrated Reinforcement Learning](https://doi.org/10.18653/v1/2026.acl-long.1154)**
  `ACL 2026` · `Model` · [Preprint](https://arxiv.org/abs/2507.04736)
  Trains RTL generators with hierarchical rewards from syntax, simulation, and synthesis feedback.

<a id="paper-2505-24183"></a>

- **[QiMeng-CodeV-R1: Reasoning-Enhanced Verilog Generation](https://doi.org/10.52202/085713-5160)**
  `NeurIPS 2025` · `Model` · [Preprint](https://arxiv.org/abs/2505.24183)
  Combines verified data synthesis, reasoning distillation, and reinforcement learning for Verilog generation.

<a id="paper-2505-11849"></a>

- **[VeriReason: Reinforcement Learning with Testbench Feedback for Reasoning-Enhanced Verilog Generation](https://doi.org/10.1145/3787109.3815310)**
  `GLSVLSI 2026` · `Model` · [Preprint](https://arxiv.org/abs/2505.11849)
  Uses testbench feedback and reinforcement learning to strengthen reasoning and first-attempt RTL generation.

<a id="planning-and-tool-orchestration"></a>

### 3.2. Task Planning and Multi-Agent Tool Orchestration

<a id="paper-2605-06434"></a>

- **[Knowledge Graphs, the Missing Link in Agentic AI-based Formal Verification](https://doi.org/10.1109/icicdt69693.2026.11669279)**
  `ICICDT 2026` · `Agent` · [Preprint](https://arxiv.org/abs/2605.06434)
  A multi-agent verification workflow maintains a knowledge graph linking specifications, RTL, and formal-tool results to support syntax repair, counterexample-guided correction, and coverage-directed assertion generation.

<a id="paper-doi-10-23919-date69613-2026-11539468"></a>

- **[Special Day—A Design Blueprint for Scalable Multi-Agent Architectures in Complex EDA Workflows](https://doi.org/10.23919/date69613.2026.11539468)**
  `DATE 2026` · `Agent / Infrastructure`
  Introduces Nexus, an SDK for hierarchical multi-agent EDA workflows with explicit task interfaces, structured communication, tool execution, modular memory, and recovery mechanisms.

<a id="paper-2508-15940"></a>

- **[ASIC-Agent: An Autonomous Multi-Agent System for ASIC Design with Benchmark Evaluation](https://doi.org/10.1109/iclad65226.2025.00033)**
  `ICLAD 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2508.15940)
  ASIC-Agent coordinates specialized agents for RTL generation, verification, OpenLane implementation, and Caravel integration through sandboxed hardware-design tools.

<a id="paper-2505-14978"></a>

- **[JARVIS: A Multi-Agent Code Assistant for High-Quality EDA Script Generation](https://arxiv.org/abs/2505.14978)**
  `arXiv 2025-05` · `Agent`
  Combines domain expertise, retrieval, structural checking, and code repair for EDA script generation.

<a id="paper-2504-03723"></a>

- **[VFlow: Discovering Optimal Agentic Workflows for Verilog Generation](https://doi.org/10.1109/asp-dac66049.2026.11420713)**
  `ASP-DAC 2026` · `Agent` · [Preprint](https://arxiv.org/abs/2504.03723)
  VFlow searches graph-structured LLM workflows using cooperative evolution and Monte Carlo tree search, with syntax, functional, and synthesis checks and hardware-quality feedback.

<a id="paper-2502-10857"></a>

- **[Divergent Thoughts toward One Goal: LLM-based Multi-Agent Collaboration System for Electronic Design Automation](https://doi.org/10.18653/v1/2025.naacl-long.83)**
  `NAACL 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2502.10857)
  EDAid explores multi-agent collaboration for electronic design automation tasks.

<a id="paper-2308-10204"></a>

- **[ChatEDA: A Large Language Model Powered Autonomous Agent for EDA](https://doi.org/10.1109/tcad.2024.3383347)**
  `IEEE TCAD 2024` · `Agent` · [Preprint](https://arxiv.org/abs/2308.10204) · [Code](https://github.com/wuhy68/ChatEDA)
  Connects natural-language requirements to task decomposition, script generation, and EDA tool execution.

<a id="memory-and-stateful-optimization"></a>

### 3.3. Memory and Stateful Optimization

<a id="paper-2609-27067"></a>

- **[ChipMEM: Verification-Grounded Memory for EDA Agents](https://arxiv.org/abs/2609.27067)**
  `arXiv 2026-09` · `Agent`
  Stores reusable skills after tool-based verification and adds statistical guidance for recovery strategies across tasks.

<a id="paper-2608-23601"></a>

- **[StateTune: Transforming LLM-Assisted EDA Flow Tuning into a Stateful, Closed-Loop Process](https://arxiv.org/abs/2608.23601)**
  `arXiv 2026-08` · `Agent`
  Maintains persistent optimization memory and allocates runtime budgets across staged EDA flow evaluations.

<a id="tool-interfaces-and-execution"></a>

### 3.4. Tool Interfaces and Execution Infrastructure

<a id="paper-2608-07925"></a>

- **[ZhuLong: Execution-Grounded LLM Agent for EDA Scripting with Offline API Self-Exploration](https://arxiv.org/abs/2608.07925)**
  `arXiv 2026-08` · `Agent`
  ZhuLong combines API retrieval, documentation inspection, and sandbox execution through MCP tools for EDA scripting, with offline API exploration for undocumented behavior.

<a id="paper-2603-25243"></a>

- **[FluxEDA: A Unified Execution Infrastructure for Stateful Agentic EDA](https://arxiv.org/abs/2603.25243)**
  `arXiv 2026-03` · `Infrastructure`
  Provides persistent tool backends and structured execution interfaces for stateful analysis, rollback, and iterative optimization.

<a id="paper-doi-10-1109-access-2026-3730896"></a>

- **[FlowFixer-EDA: A Tool-Feedback-Augmented Large Language Model Agent for Automated Diagnosis and Repair of Open-Source RTL-to-GDS Design Flow Failures](https://doi.org/10.1109/access.2026.3730896)**
  `IEEE Access 2026` · `Agent`
  FlowFixer-EDA combines stage-aware log parsing, knowledge retrieval, and structured patches to diagnose RTL-to-GDS flow failures; EDA tool reruns validate repairs and guide further revision.

<a id="paper-2508-01012"></a>

- **[AutoEDA: Enabling EDA Flow Automation through Microservice-Based LLM Agents](https://doi.org/10.1145/3842675)**
  `ACM TODAES 2026` · `Agent` · [Preprint](https://arxiv.org/abs/2508.01012)
  Uses microservice-style MCP tool interfaces for task decomposition, tool selection, and EDA flow execution.

<a id="paper-2507-19570"></a>

- **[MCP4EDA: LLM-Powered Model Context Protocol RTL-to-GDSII Automation with Backend Aware Synthesis Optimization](https://arxiv.org/abs/2507.19570)**
  `arXiv 2025-07` · `Agent`
  Explores MCP-based RTL-to-GDSII automation with backend-aware synthesis optimization.

<a id="eda-algorithm-and-tool-development"></a>

## 4. EDA Algorithm Discovery and Tool Development

Here the modified artifact is the EDA software itself. Candidate algorithm or repository changes are compiled and evaluated for correctness and implementation quality across designs.

<a id="synthesis-and-mapping-algorithms"></a>

### 4.1. Logic Synthesis and Technology Mapping Algorithms

<a id="paper-2604-26591"></a>

- **[MappingEvolve: LLM-Driven Code Evolution for Technology Mapping](https://doi.org/10.1145/3770743.3803988)**
  `DAC 2026` · `Agent` · [Preprint](https://arxiv.org/abs/2604.26591) · [Code](https://github.com/Flians/MappingEvolve)
  Evolves technology-mapping source code with LLM-generated candidates and implementation-quality feedback.

<a id="paper-2604-15082"></a>

- **[Autonomous Evolution of EDA Tools: Multi-Agent Self-Evolved ABC](https://doi.org/10.1145/3770743.3804221)**
  `DAC 2026` · `Agent` · [Preprint](https://arxiv.org/abs/2604.15082)
  Evolves components of the integrated ABC synthesis codebase under build, correctness, and QoR checks.

<a id="placement-and-routing-algorithms"></a>

### 4.2. Placement and Routing Algorithms

<a id="paper-2604-22234"></a>

- **[GR-Evolve: Design-Adaptive Global Routing via LLM-Driven Algorithm Evolution](https://arxiv.org/abs/2604.22234)**
  `arXiv 2026-04` · `Agent` · [Code](https://github.com/ASU-VDA-Lab/GR-Evolve)
  Adapts global-routing implementations through source-code evolution evaluated inside OpenROAD flows.

<a id="paper-2504-17801"></a>

- **[Evolution of Optimization Algorithms for Global Placement via Large Language Models](https://arxiv.org/abs/2504.17801)**
  `arXiv 2025-04` · `Method`
  EvoPlace evolves optimization algorithms for analytical global placement through an LLM-guided genetic flow.

<a id="repository-level-eda-research"></a>

### 4.3. Repository-Level Tool Improvement and Research Workflows

<a id="paper-2610-10129"></a>

- **[When Algorithmic Exploration Becomes Cheap: A Case Study of Agentic Research in EDA](https://arxiv.org/abs/2610.10129)**
  `arXiv 2026-10` · `Perspective`
  Reports agentic EDA algorithm-research case studies and discusses how executable results should be validated.

<a id="paper-doi-10-1145-3797154"></a>

- **[SpiceFuzz: LLM-Based Fuzzing for Spice Circuit Simulator Tools Bug Detection](https://doi.org/10.1145/3797154)**
  `ACM TODAES 2026` · `Agent`
  SpiceFuzz generates SPICE netlists with LLM-guided mutations, uses mutation history and execution feedback to guide subsequent tests, and compares simulator results to detect tool bugs.

<a id="paper-2601-06268"></a>

- **[Automated QoR improvement in OpenROAD with coding agents](https://arxiv.org/abs/2601.06268)**
  `arXiv 2026-01` · `Agent`
  AuDoPEDA makes repository-grounded OpenROAD code changes and evaluates their effects on design quality.

<a id="paper-2412-05311"></a>

- **[DRC-Coder: Automated DRC Checker Code Generation Using LLM Autonomous Agent](https://doi.org/10.1145/3698364.3705347)**
  `ISPD 2025` · `Agent` · [Preprint](https://arxiv.org/abs/2412.05311)
  DRC-Coder coordinates rule-interpretation and coding agents with visual layout information and automated evaluation to generate and debug integrated DRC-checker code.

<a id="benchmarks-and-datasets"></a>

## 5. Benchmarks and Evaluation

Benchmarks are grouped by the capability they measure: design generation, verification, or implementation and closure. Evaluation methodology then explains how correctness, quality, and execution budgets affect comparisons.

<a id="rtl-generation-benchmarks"></a>

### 5.1. RTL Generation and Repository Benchmarks

<a id="paper-2601-21448"></a>

- **[ChipBench: A Next-Step Benchmark for Evaluating LLM Performance in AI-Aided Chip Design](https://arxiv.org/abs/2601.21448)**
  `arXiv 2026-01` · `Benchmark`
  ChipBench evaluates chip-design tasks with attention to reference behavior and practical design complexity.

<a id="paper-doi-10-1109-iccd65941-2025-00087"></a>

- **[RTLBench: A Multi-Dimensional Benchmark Suite for Evaluating LLM-Generated RTL Code](https://doi.org/10.1109/iccd65941.2025.00087)**
  `ICCD 2025` · `Benchmark` · [Project](https://fangzhigang32.github.io/RTLBench)
  RTLBench evaluates generated RTL across multiple dimensions and studies Log2BetterRTL, which converts EDA diagnostic logs into prompts for iterative code improvement.

<a id="paper-2507-16200"></a>

- **[RealBench: Benchmarking Verilog Generation Models with Real-World IP Designs](https://arxiv.org/abs/2507.16200)**
  `arXiv 2025-07` · `Benchmark`
  RealBench evaluates Verilog generation using real-world IP designs.

<a id="paper-doi-10-1109-isqed65160-2025-11014310"></a>

- **[Evaluating LLM-Based Communicative Agents for Verilog Design](https://doi.org/10.1109/isqed65160.2025.11014310)**
  `ISQED 2025` · `Benchmark`
  Evaluates communicating LLM agents on Verilog design tasks, including collaborative generation and correction using Icarus Verilog compiler feedback.

<a id="paper-2405-17378"></a>

- **[RTL-Repo: A Benchmark for Evaluating LLMs on Large-Scale RTL Design Projects](https://doi.org/10.1109/lad62341.2024.10691810)**
  `LAD 2024` · `Benchmark` · [Preprint](https://arxiv.org/abs/2405.17378)
  RTL-Repo focuses on large-scale RTL projects and repository context.

<a id="paper-2309-07544"></a>

- **[Invited Paper: VerilogEval: Evaluating Large Language Models for Verilog Code Generation](https://doi.org/10.1109/iccad57390.2023.10323812)**
  `ICCAD 2023` · `Benchmark` · [Preprint](https://arxiv.org/abs/2309.07544) · [Code](https://github.com/NVlabs/verilog-eval)
  VerilogEval provides executable Verilog-generation evaluations; the linked repository documents subsequent benchmark versions.

<a id="paper-2308-05345"></a>

- **[RTLLM: An Open-Source Benchmark for Design RTL Generation with Large Language Model](https://doi.org/10.1109/asp-dac58780.2024.10473904)**
  `ASP-DAC 2024` · `Benchmark` · [Preprint](https://arxiv.org/abs/2308.05345) · [Code](https://github.com/hkust-zhiyao/RTLLM)
  RTLLM evaluates natural-language-to-RTL generation with functional and design-quality checks.

<a id="verification-benchmarks"></a>

### 5.2. Verification and Assertion Benchmarks

<a id="paper-2506-14074"></a>

- **[Comprehensive Verilog Design Problems: A Next-Generation Benchmark Dataset for Evaluating Large Language Models and Agents on RTL Design and Verification](https://arxiv.org/abs/2506.14074)**
  `arXiv 2025-06` · `Benchmark`
  CVDP provides design and verification tasks for evaluating hardware language models and agents.

<a id="paper-2410-23299"></a>

- **[FVEval: Understanding Language Model Capabilities in Formal Verification of Digital Hardware](https://doi.org/10.23919/date64628.2025.10992720)**
  `DATE 2025` · `Benchmark` · [Preprint](https://arxiv.org/abs/2410.23299) · [Code](https://github.com/NVlabs/FVEval)
  FVEval evaluates language models on formal-verification tasks, including assertion-related reasoning.

<a id="paper-2406-18627"></a>

- **[AssertionBench: A Benchmark to Evaluate Large-Language Models for Assertion Generation](https://doi.org/10.18653/v1/2025.findings-naacl.449)**
  `NAACL Findings 2025` · `Benchmark` · [Preprint](https://arxiv.org/abs/2406.18627) · [Code](https://github.com/achieve-lab/assertion_data_for_LLM)
  AssertionBench evaluates assertion generation using hardware verification tasks and property data.

<a id="implementation-and-closure-benchmarks"></a>

### 5.3. PPA, Physical Design, and Cross-Stage Closure Benchmarks

<a id="paper-2609-23363"></a>

- **[TicTacBench: Benchmarking Timing Closure Capabilities of Coding Agents](https://arxiv.org/abs/2609.23363)**
  `arXiv 2026-09` · `Benchmark`
  TicTacBench evaluates RTL timing closure with post-place-and-route results and functional checks.

<a id="paper-doi-10-1145-3770743-3858389"></a>

- **[Special Research Session: Toward Agentic Solution for DRC Challenges in Digital VLSI Design](https://doi.org/10.1145/3770743.3858389)**
  `DAC 2026` · `Benchmark`
  Introduces an agentic DRC benchmark for violation detection and repair across polygon- and block-level layouts, with containerized execution and standardized evaluation metrics.

<a id="paper-2607-16632"></a>

- **[CLOSER-Bench: Evaluating Budgeted Cross-Stage Design Closure for Hardware Agents](https://arxiv.org/abs/2607.16632)**
  `arXiv 2026-07` · `Benchmark`
  CLOSER-Bench pairs tasks across RTL and physical-design stages and measures progress under a tool budget.

<a id="paper-2606-17253"></a>

- **[PDAGENT-BENCH: Characterizing, Grounding, and Architecting LLM/VLM Agents for VLSI Physical Design](https://arxiv.org/abs/2606.17253)**
  `arXiv 2026-06` · `Benchmark`
  PDAGENT-BENCH characterizes agents on tool-grounded VLSI physical-design tasks.

<a id="paper-2605-06936"></a>

- **[Bridging the Last Mile of Circuit Design: PostEDA-Bench, a Hierarchical Benchmark for PPA Convergence and DRC Fixing](https://arxiv.org/abs/2605.06936)**
  `arXiv 2026-05` · `Benchmark`
  PostEDA-Bench targets PPA convergence and design-rule fixing in later implementation stages.

<a id="evaluation-notes"></a>

### 5.4. Evaluation Methodology

Use the benchmark and tool setup to interpret a result:

- **Correctness:** distinguish compilation, simulation against an independent reference, formal equivalence, property proofs, and coverage. Coverage alone does not establish functional correctness.
- **Implementation quality:** identify whether PPA comes from synthesis, placement, or completed routing; record technology, constraints, and tool versions.
- **Budget:** count model calls, repair iterations, simulations, synthesis runs, and physical-design runs. A completed multi-turn run is different from a single generation attempt.
- **Generalization:** distinguish per-design adaptation from evaluation on held-out designs, processes, or task families; record whether memory and training data are frozen.
- **Workflow scope:** distinguish parameter tuning, design edits, and changes to the EDA tool's implementation. These actions have different correctness and regression requirements.

<a id="industrial-systems-and-reports"></a>

## 6. Industrial Systems and Official Reports

Follow commercial systems, technical blogs, whitepapers, and industry reports alongside the research literature. Entries describe vendor-stated capabilities and availability at the linked source date; product pages are mutable, and reported gains are not independently validated here. Industrial resources are separate from the paper count.

<a id="established-eda-vendors"></a>

### 6.1. Established EDA Vendors

<a id="industry-synopsys"></a>

#### 6.1.1. Synopsys

Focus: cross-domain orchestration, verification, implementation, and analog design. Related research: [agent architectures](#eda-orchestration-and-infrastructure), [physical design](#synthesis-and-physical-design), and [analog design](#analog-and-mixed-signal).

- **[GPT-Synopsys: Specialized Models for Chip-Design Workflows](https://news.synopsys.com/2026-09-30-OpenAI-and-Synopsys-Announce-GPT-Synopsys-Frontier-Intelligence-to-Revolutionize-Chip-Design)**
  `Official announcement 2026-09-30` · `Model–tool integration`
  Synopsys and OpenAI announce joint development of a specialized model for operating EDA tools, interpreting results, and iterating toward PPA, timing, and verification objectives. The announcement describes early customer engagements and planned integration with Synopsys.ai and Autopilot.

- **[Synopsys AgentEngineer and Autopilot Platform](https://news.synopsys.com/2026-09-28-Synopsys-Powers-Autonomous-Engineering-with-a-Broad-Portfolio-of-Long-Horizon-Agents-and-Autopilot-Platform)**
  `Official announcement 2026-09-28` · `Agent orchestration`
  Describes long-horizon domain agents supported by task agents, reusable skills, persistent memory, and engineering-tool feedback across verification, implementation, analog, and other workflows. Availability was planned for the end of 2026 at announcement time.

<a id="industry-cadence"></a>

#### 6.1.2. Cadence

Focus: front-end design, verification, and early PPA optimization. Related research: [RTL generation](#rtl-generation), [verification and debugging](#verification-and-debugging), and [RTL optimization](#rtl-and-hls-optimization).

- **[ChipStack RTL Generation Agent and Early PPA Optimization](https://semiiphub.com/pulse/news/cadence-chipstack-ai-super-agent-rtl-generation-ppa-optimization)**
  `Vendor announcement 2026-09-22` · `Press-release reprint` · `RTL generation and optimization`
  Cadence describes specification-to-RTL generation and updates to existing RTL, with EDA tools checking functionality and PPA during refinement. The announcement schedules expanded capabilities for selected early-access customers in Q4 2026.

- **[Cadence Unleashes ChipStack AI Super Agent](https://www.cadence.com/en_US/home/company/newsroom/press-releases/pr/2026/cadence-unleashes-chipstack-ai-super-agent-pioneering-a-new.html)**
  `Official announcement 2026-02-10` · `Design and verification agents` · [Press-release reprint](https://semiiphub.com/pulse/news/cadence-chipstack-ai-super-agent) · [Product](https://www.cadence.com/en_US/home/tools/system-design-and-verification/chipstack-ai-superagent.html)
  Introduces agents that call Cadence tools to create designs and testbenches, generate test plans, orchestrate regressions, debug failures, and propose fixes. The release describes early-access deployments and support for cloud-hosted and on-premises models.

The Cadence summaries and announcement dates follow the linked Cadence-authored press-release reprints on Semi IP Hub.

<a id="industry-siemens"></a>

#### 6.1.3. Siemens EDA

Focus: verification planning, tool execution, debugging, and RTL sign-off. Related research: [verification and debugging](#verification-and-debugging), [tool interfaces](#tool-interfaces-and-execution), and [evaluation methodology](#evaluation-notes).

- **[Questa One Agentic Toolkit](https://www.siemens.com/en-us/products/ic/questa-one/agentic-toolkit/)**
  `Official product overview` · `Undated` · `Verification orchestration`
  Describes five flow agents for planning, design, verification, debug, and closure, connected through a licensed Gateway to Questa engines, databases, and services. The page also describes integration with Siemens Fuse EDA for enterprise orchestration and support for external LLMs and coding agents.

- **[The 2026 Functional Verification Study](https://blogs.sw.siemens.com/verificationhorizons/2026/09/08/the-2026-functional-verification-study/)**
  `Official report overview 2026-09-08` · `Industry survey`
  Introduces the Siemens EDA/Wilson Research Group study, including focused whitepapers, a methodology reference, and a data atlas. Provides industry context on verification complexity and AI/ML adoption.

- **[Why Agentic AI Could Redefine the Future of Design and Verification](https://blogs.sw.siemens.com/verificationhorizons/2026/08/31/why-agentic-ai-could-redefine-the-future-of-design-and-verification/)**
  `Official blog 2026-08-31` · `Industry perspective`
  Discusses the shift toward parallel, integrated design and verification workflows, with engineers defining objectives and directing agents. A keynote preview and perspective on engineering roles.

- **[Human-Centered Agentic AI Workflows for RTL Verification](https://verificationacademy.com/topics/machine-learning/human-centered-agentic-ai-workflows-for-rtl-verification)**
  `Official whitepaper landing page 2026-02-27` · `Human–agent collaboration`
  The public introduction explains engine-native context, goal-driven agents, bounded task execution, and engineer decision authority in the Questa One Agentic Toolkit. Links to the whitepaper for the broader workflow discussion.

<a id="startups-and-emerging-platforms"></a>

### 6.2. Startups and Emerging Platforms

<a id="industry-chipagents"></a>

#### 6.2.1. ChipAgents

[ChipAgents](https://chipagents.ai/) develops commercial agents for chip design and verification; access is through its demo and customer channels. Related research: [verification and debugging](#verification-and-debugging) and [multi-agent orchestration](#planning-and-tool-orchestration).

- **[Scaling Autonomous Root Cause Analysis for Regression Triage](https://chipagents.ai/blogs/scaling-autonomous-root-cause-analysis-regression-triage)**
  `Official technical blog 2026-10-06` · `Regression triage`
  Describes grouping failures by root cause, selecting witness simulations, selectively rerunning with waveform dumps, and coordinating diagnosis, fixes, and verification across regressions.

- **[ChipAgents RCA: Autonomous ASIC Root Cause Analysis](https://chipagents.ai/blogs/chipagents-rca)**
  `Official technical blog 2025-11-05` · `Waveform-guided debugging`
  Presents a waveform-query engine, a multi-agent prover–verifier loop, and self-consistency ranking for tracing failures across RTL, testbenches, logs, and waveforms. Includes vendor case studies and evaluation discussion.

<a id="industry-cognichip"></a>

#### 6.2.2. Cognichip

- **[Cognichip Artificial Chip Intelligence — ACI Enterprise](https://www.cognichip.ai/product/aci)**
  `Official product overview` · `Undated` · `Domain models and agent workflows`
  Describes a physics-informed model and agent stack with context, memory, and engineering workflows spanning specification, RTL generation, verification, and PPA optimization. Access is offered through a demo request. Related research: [domain models and learning](#models-and-training) and [agent architectures](#eda-orchestration-and-infrastructure).

<a id="industry-chipmind"></a>

#### 6.2.3. Chipmind

- **[How to Use Chipmind Agents and RTL Canvas with IP-XACT](https://chipmind.ai/post/how-to-use-chipmind-agents-and-rtl-canvas-with-ip-xact)**
  `Official technical blog 2026-10-20` · `SoC integration and visual review`
  Uses PULPino and Croc examples to explain typed structural edits, IP-XACT/RTL consistency, bus-interface connections, and visual diffs that engineers accept or reject. Related research: [specification and architecture](#specification-and-architecture) and [repository-level RTL design](#rtl-generation).

- **[Chipmind Agents and RTL Canvas](https://chipmind.ai/)**
  `Official product overview` · `Undated` · `EDA execution and design context`
  Describes agents that work with existing lint, simulation, synthesis, and scripting flows, maintain SoC-level context, and expose results through RTL Canvas. Demo access; the vendor lists cloud, VPC, and on-premises deployment options.

<a id="industry-ricursive"></a>

#### 6.2.4. Ricursive Intelligence

- **[Ricursive Intelligence](https://www.ricursive.com/)**
  `Official company overview` · `Undated` · `Research direction`
  Describes a research program connecting AI for chip design with hardware for AI through iterative improvement. The overview establishes the company's direction; it does not provide a detailed public agent implementation or evaluation protocol. Related research: [agent architectures](#eda-orchestration-and-infrastructure).

## Contributing

Add a paper, a runnable project, a benchmark, an official industry resource, or a correction through an issue or pull request. See [CONTRIBUTING.md](CONTRIBUTING.md) for inclusion criteria and the entry format. Self-submissions are welcome under the same criteria.

Useful contributions include verified code links, publication metadata, benchmark-version clarifications, broken-link fixes, and concise summaries of new work.

## License

The original list text is dedicated to the public domain under [CC0 1.0](LICENSE). Linked papers, code, datasets, logos, and tools retain their respective licenses.

