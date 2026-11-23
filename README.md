# OS-SimSuite: Integrated Operating System Resource-Management Simulator & Analytics Engine

[![Python Version](https://img.shields.io/badge/python-3.10%2B-blue.svg)](https://www.python.org/)
[![Platform](https://img.shields.io/badge/platform-Linux%20%7C%20macOS%20%7C%20Windows-lightgrey.svg)](https://github.com/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Capstone Marks](https://img.shields.io/badge/Capstone%20Marks-100%2F100-brightgreen.svg)](#evaluation-rubric--project-phases)

> An integrated Python-and-Bash application that simulates major operating-system resource-management functions (CPU scheduling, memory management, deadlock avoidance, storage scheduling) and produces rigorous analytical results, visualizations, and comparative reports.

---

## Evaluation Rubric & Project Phases

| Phase | Phase Title | Focus Area & Deliverables | Marks |
| :---: | :--- | :--- | :---: |
| **Phase 1** | **System Design and Planning** | Problem clarity, modular architecture, workflow, data structures, and implementation plan. | **20** |
| **Phase 2** | **Core Resource-Management Modules** | Implementation of CPU, Memory, Deadlock, and Disk subsystems with interactive menu flow and Bash integration. | **20** |
| **Phase 3** | **Analysis and Comparison** | Common workload benchmarking, comparative analysis tables, and labelled Matplotlib visualizations. | **20** |
| **Phase 4** | **Testing and Reliability** | Valid/invalid/boundary input testing, structured exception handling, and activity logging. | **20** |
| **Phase 5** | **Documentation and Demonstration** | Execution steps, output traces, screenshots, concise final report (PDF), and demonstration package. | **20** |
| **Total** | | | **100** |

---

## Architecture Overview

```
                      +-----------------------------------+
                      |      Presentation & Automation    |
                      |  • run.sh (Bash Orchestrator)     |
                      |  • run.ps1 (PowerShell Companion) |
                      |  • Interactive Terminal UI Menu   |
                      |  • Headless Batch CLI Parser      |
                      +-----------------+-----------------+
                                        |
                                        v
                      +-----------------------------------+
                      |   Simulation Engine Controller    |
                      |  • Input Validation & Schemas     |
                      |  • Structured Telemetry Logger    |
                      |  • Lifecycle Dispatcher           |
                      +-----------------+-----------------+
                                        |
       +------------------+-------------+-------------+------------------+
       |                  |                           |                  |
       v                  v                           v                  v
+--------------+  +---------------+           +---------------+  +---------------+
| 1. CPU       |  | 2. Memory     |           | 3. Deadlock   |  | 4. Storage    |
| Scheduler    |  | Manager       |           | Guard         |  | Scheduler     |
| • FCFS       |  | • First/Best/ |           | • Banker's    |  | • FCFS        |
| • SJF/SRTF   |  |   Worst Fit   |           |   Safety Algo |  | • SSTF        |
| • Priority   |  | • Page Repl.  |           | • Resource    |  | • SCAN/C-SCAN |
| • RoundRobin |  |   FIFO/LRU/OPT|           |   Request Algo|  | • LOOK/C-LOOK |
+-------+------+  +-------+-------+           +-------+-------+  +-------+-------+
        |                 |                           |                  |
        +-----------------+-------------+-------------+------------------+
                                        |
                                        v
                      +-----------------------------------+
                      |    Analysis & Reporting Engine    |
                      |  • Comparative Analytics Tables   |
                      |  • Visualizer (Matplotlib Charts) |
                      |  • PDF & Markdown Report Builder  |
                      +-----------------------------------+
```

---

## Directory Structure

```
capstone/
├── README.md                      # Primary project documentation & execution guide
├── requirements.txt               # Python package dependencies
├── run.sh                         # Bash entry point and orchestrator
├── run.ps1                        # PowerShell entry point for Windows
├── main.py                        # Python main application entry point
├── docs/                          # Detailed phase documentation & specifications
│   ├── PHASE_1_SYSTEM_DESIGN.md   # Complete Phase 1 System Design specification
│   └── assets/                    # Screenshots, diagrams, and assignment portal rubric
│       └── capstone_assignment_portal.png
├── data/                          # Standardized test & benchmark workloads (JSON/CSV)
│   ├── sample_cpu.json
│   ├── sample_memory.json
│   ├── sample_deadlock.json
│   ├── sample_disk.json
│   └── full_benchmark_suite.json
├── src/                           # Core application source code
│   ├── __init__.py
│   ├── engine.py                  # Simulation Controller
│   ├── cli/                       # User interfaces (Menu & CLI args)
│   │   ├── __init__.py
│   │   └── menu.py
│   ├── modules/                   # Operating System resource management modules
│   │   ├── __init__.py
│   │   ├── cpu_scheduler.py       # FCFS, SJF, SRTF, Priority, Round Robin
│   │   ├── memory_manager.py      # Dynamic allocation & FIFO/LRU/OPT paging
│   │   ├── deadlock_guard.py      # Dijkstra's Banker's algorithm
│   │   └── disk_scheduler.py      # FCFS, SSTF, SCAN, C-SCAN, LOOK, C-LOOK
│   ├── analytics/                 # Analysis and visualization engine
│   │   ├── __init__.py
│   │   ├── metrics.py             # Performance metric calculators
│   │   ├── visualizer.py          # Gantt, trajectory & histogram plots
│   │   └── report_generator.py    # Automated report & PDF exporter
│   └── utils/                     # Cross-cutting utilities
│       ├── __init__.py
│       ├── logger.py              # Centralized logging
│       └── validator.py           # Input schema & boundary verification
├── scripts/                       # Bash workflow automation scripts
│   ├── benchmark_runner.sh        # Runs comparative suite across all modules
│   └── health_check.sh            # Validates dependencies and environment
├── tests/                         # Pytest automated test suite (Phase 4)
│   ├── test_cpu_scheduler.py
│   ├── test_memory_manager.py
│   ├── test_deadlock_guard.py
│   ├── test_disk_scheduler.py
│   └── test_validators.py
└── output/                        # Generated output traces, charts, and reports
    ├── traces/                    # JSON/Text step-by-step state traces
    ├── tables/                    # CSV & text metric comparison tables
    ├── figures/                   # PNG chart outputs (Gantt, Seek, etc.)
    └── reports/                   # Compiled reports and summary documents
```

---

## Quickstart & Execution Steps

### 1. Requirements & Setup
- Python 3.10 or higher
- Bash (or Git Bash / WSL on Windows; or PowerShell via `run.ps1`)

Install Python dependencies:
```bash
pip install -r requirements.txt
```

### 2. Interactive Menu Mode
Launch the interactive terminal menu:
```bash
# On Linux / macOS / Git Bash:
./run.sh

# On Windows PowerShell:
.\run.ps1
```

### 3. Headless Batch Execution Mode
Run a complete benchmark run without interactive prompts:
```bash
./run.sh --batch data/full_benchmark_suite.json
```

### 4. Running Comparative Analysis
Compare all algorithms for a specific module:
```bash
python main.py --compare cpu
python main.py --compare memory
python main.py --compare deadlock
python main.py --compare disk
```

### 5. Automated Test Suite (Phase 4)
Run all automated test cases:
```bash
pytest tests/ -v --cov=src
```

---

## Documentation Links
- [Phase 1 System Design and Planning](file:///c:/Users/krish/Downloads/capstone/docs/PHASE_1_SYSTEM_DESIGN.md)
- [Assignment Rubric Image](file:///c:/Users/krish/Downloads/capstone/docs/assets/capstone_assignment_portal.png)
