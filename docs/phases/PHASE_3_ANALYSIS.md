# Phase 3: Analysis and Comparison Report
**Evaluation Weightage:** 20 Marks  
**Status:** Completed with Empirical Tables, Labelled Charts & Technical Observations  

---

## 1. Standardized Workload Evaluation

All algorithms were benchmarked on standardized workloads (`data/sample_workload.json`):

### 1.1 CPU Scheduling Comparative Evaluation
Workload: 4 processes ($P_1$: AT=0, BT=8, Pri=3; $P_2$: AT=1, BT=4, Pri=1; $P_3$: AT=2, BT=9, Pri=4; $P_4$: AT=3, BT=5, Pri=2), Round Robin Quantum = 3.

| Algorithm | Avg Waiting Time | Avg Turnaround Time | Avg Response Time | CPU Util % | Throughput | Total Time |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **FCFS** | 8.75 | 15.25 | 8.75 | 100.0% | 0.1538 | 26 |
| **SJF (Non-Preemptive)** | 7.75 | 14.25 | 7.75 | 100.0% | 0.1538 | 26 |
| **SRTF (Preemptive SJF)** | **6.50** | **13.00** | 4.25 | 100.0% | 0.1538 | 26 |
| **Priority (Non-Preemptive)** | 7.75 | 14.25 | 7.75 | 100.0% | 0.1538 | 26 |
| **Priority (Preemptive)** | **6.50** | **13.00** | 4.25 | 100.0% | 0.1538 | 26 |
| **Round Robin (Q=3)** | 13.50 | 20.00 | **3.00** | 100.0% | 0.1538 | 26 |

**Technical Observations:**
- **SRTF** achieved the lowest average turnaround (13.00) and waiting time (6.50) because it preemptively switched to shorter tasks ($P_2, P_4$) as they arrived.
- **Round Robin** achieved the best response time (3.00), making it ideal for interactive time-sharing systems despite higher turnaround due to context switching overhead.

---

### 1.2 Virtual Memory Page Replacement Comparison
Reference String: `[7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2, 1, 2, 0, 1, 7, 0, 1]` across 3 physical frames.

| Algorithm | Frames | Total References | Page Faults | Page Hits | Fault Ratio | Hit Ratio |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **FIFO** | 3 | 20 | 15 | 5 | 75.00% | 25.00% |
| **LRU** | 3 | 20 | 12 | 8 | 60.00% | 40.00% |
| **Optimal (OPT)** | 3 | 20 | **9** | **11** | **45.00%** | **55.00%** |

**Technical Observations:**
- **Optimal (OPT)** achieved the highest hit ratio (55.00%) and lowest page faults (9), validating theoretical bounds.
- **LRU** closely mirrored Optimal by exploiting temporal locality, reducing page faults by 20% compared to FIFO without requiring knowledge of future references.

---

### 1.3 Disk Head Scheduling Trajectory Comparison
Initial Head: 53, Cylinders: 200, Request Queue: `[98, 183, 37, 122, 14, 124, 65, 67]`.

| Algorithm | Initial Head | Direction | Total Head Movement | Avg Seek Distance |
| :--- | :---: | :---: | :---: | :---: |
| **FCFS** | 53 | N/A | 640 | 80.00 |
| **SSTF** | 53 | Dynamic | **236** | **29.50** |
| **LOOK** | 53 | RIGHT | 299 | 37.38 |
| **C-LOOK** | 53 | RIGHT | 322 | 40.25 |
| **SCAN (Elevator)** | 53 | RIGHT | 331 | 41.38 |
| **C-SCAN** | 53 | RIGHT | 382 | 47.75 |

**Technical Observations:**
- **SSTF** minimized total head travel (236 cylinders), but risks starvation for tracks far from current cluster.
- **LOOK** outperformed SCAN (299 vs 331) by reversing immediately at the highest pending track (183) rather than travelling unnecessarily to the mechanical boundary (199).
