# Phase 2: Core Resource-Management Modules Implementation Report
**Evaluation Weightage:** 20 Marks  
**Status:** 100% Implemented & Battle-Tested  

---

## 1. Overview of Implemented Modules
While the rubric required at least three major OS modules, **OS-SimSuite implements all four primary operating system resource management domains** alongside a cross-cutting automation and validation layer:

1. **CPU Process Scheduling Engine (`src/modules/cpu_scheduler.py`)**:
   - Algorithms: First-Come First-Served (FCFS), Shortest Job First (SJF Non-Preemptive), Shortest Remaining Time First (SRTF / Preemptive SJF), Priority (Non-Preemptive & Preemptive), Round Robin (configurable time quantum).
   - Reusable Dataclasses: `Process`, `GanttSlice`, `ScheduleResult`.
   - Metrics: Waiting Time ($WT$), Turnaround Time ($TAT$), Response Time ($RT$), CPU Utilization %, Throughput, timeline Gantt chart.

2. **Memory Management Subsystem (`src/modules/memory_manager.py`)**:
   - Contiguous Allocation: First-Fit, Best-Fit, Worst-Fit with dynamic partition tracking, internal fragmentation calculation, process deallocation, and memory compaction.
   - Virtual Memory Page Replacement: FIFO, LRU, and Optimal (OPT) with step-by-step frame state snapshots, page hit/fault tracking, and hit/fault ratios.

3. **Deadlock Avoidance Subsystem (`src/modules/deadlock_guard.py`)**:
   - Dijkstra's Banker's Algorithm for multi-instance resource systems.
   - Core Functions:
     - `check_safety()`: Validates whether system is in a safe state and derives complete safe sequence (e.g. $\langle P_1, P_3, P_0, P_2, P_4 \rangle$).
     - `request_resources()`: Validates claims ($Req \le Need$ and $Req \le Available$), performs trial allocation, safety check, and commits or rolls back safely.

4. **Storage / Disk Scheduling Subsystem (`src/modules/disk_scheduler.py`)**:
   - Six cylinder scheduling algorithms: FCFS, SSTF, SCAN (Elevator), C-SCAN, LOOK, and C-LOOK.
   - Features: Boundary turnaround, configurable initial sweep direction (`RIGHT` / `LEFT`), total head movement, and average seek distance.

5. **Integrated Presentation & Automation**:
   - Interactive Terminal UI (`src/cli/menu.py`) with ANSI colors and submenus.
   - Headless Batch CLI (`main.py --batch`, `--compare`, `--report`, `--test`).
   - POSIX Bash automation wrapper (`run.sh`) and PowerShell companion (`run.ps1`).
