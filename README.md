# Petri Net Analyzer

**Course:** CO2011 - Mathematical Modeling  
**Semester:** 1 (2025-2026)  
**University:** HCMC University of Technology - VNU-HCM

---

## 📋 Table of Contents

- [Overview](#overview)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Building the Project](#building-the-project)
- [Testing Each Task](#testing-each-task)
- [Input Files](#input-files)
- [Expected Results](#expected-results)
- [Troubleshooting](#troubleshooting)
- [References](#references)

---

## 🎯 Overview

This project implements a Petri Net analyzer with the following capabilities:

| Task | Description | Weight | Status |
|------|-------------|--------|--------|
| **Task 1** | PNML Parsing | 5% | ✅ Ready |
| **Task 2** | Explicit Reachability (BFS/DFS) | 5% | ✅ Ready |
| **Task 3** | BDD-based Symbolic Reachability | 40% | 🔧 Requires CUDD |
| **Task 4** | ILP + BDD Deadlock Detection | 20% | 🔧 Requires CUDD + Gurobi |
| **Task 5** | Optimization over Reachable Markings | 20% | 🔧 Requires CUDD + Gurobi |
| **Report** | Documentation Quality | 10% | 📝 In Progress |

---

## 📁 Project Structure

```
PetriNetAnalyzer/
├── Makefile                          # Build system
├── README.md                         # This file
│
├── include/                          # External libraries
│   ├── tinyxml2.h
│   └── tinyxml2.cpp
│
├── src/
│   ├── core/                         # Core Petri Net classes
│   │   ├── PetriNet.h
│   │   └── PetriNet.cpp
│   │
│   ├── parser/                       # PNML file parser (Task 1)
│   │   ├── PNMLParser.h
│   │   └── PNMLParser.cpp
│   │
│   ├── explicit/                     # Explicit reachability (Task 2)
│   │   ├── ExplicitReachability.h
│   │   └── ExplicitReachability.cpp
│   │
│   ├── symbolic/                     # BDD-based methods (Task 3)
│   │   ├── BDDReachability.h
│   │   └── BDDReachability.cpp
│   │
│   ├── ilp/                          # ILP-based methods (Task 4 & 5)
│   │   ├── DeadlockDetector.h
│   │   ├── DeadlockDetector.cpp
│   │   ├── OptimizationSolver.h
│   │   └── OptimizationSolver.cpp
│   │
│   └── tests/                        # Test programs for each task
│       ├── test_task1.cpp
│       ├── test_task2.cpp
│       ├── test_task3.cpp
│       ├── test_task4.cpp
│       └── test_task5.cpp
│
└── test_models/                      # PNML test files and weights
    ├── simple.pnml
    ├── mutex.pnml
    ├── producer_consumer.pnml
    ├── deadlock.pnml
    ├── weights_simple.txt
    └── weights_mutex.txt
```

---

## 🔧 Prerequisites

### Required (for Task 1 & 2):
- **g++** (with C++17 support)
- **make**
- **TinyXML2** (included in `include/`)

### Optional (for Task 3-5):
- **CUDD** (Colorado University Decision Diagram library)
- **Gurobi** (or alternative ILP solver like PuLP)

### Check your environment:
```bash
g++ --version      # Should be >= 7.0
make --version     # Any recent version
```

---

## 📦 Installation

### 1. Clone the repository
```bash
git clone <repository-url>
cd PetriNetAnalyzer
```

### 2. Verify project structure
```bash
ls -R
# Should see: Makefile, src/, include/, test_models/
```

### 3. Install CUDD (Optional - for Task 3-5)

#### Option A: Using apt (Ubuntu/Debian)
```bash
sudo apt-get update
sudo apt-get install libcudd-dev
```

#### Option B: Build from source
```bash
git clone https://github.com/ivmai/cudd
cd cudd
./configure
make
sudo make install
cd ..
```

### 4. Install Gurobi (Optional - for Task 4-5)

1. Download from: https://www.gurobi.com/downloads/
2. Register for academic license (free for students)
3. Follow installation instructions for your OS
4. Set environment variables:
   ```bash
   export GUROBI_HOME="/opt/gurobi950/linux64"
   export PATH="${PATH}:${GUROBI_HOME}/bin"
   export LD_LIBRARY_PATH="${LD_LIBRARY_PATH}:${GUROBI_HOME}/lib"
   ```

---

## 🔨 Building the Project

### Build individual tasks:
```bash
# Task 1: PNML Parsing
make task1

# Task 2: Explicit Reachability
make task2

# Task 3: BDD Symbolic Reachability (requires CUDD)
make task3

# Task 4: Deadlock Detection (requires CUDD + Gurobi)
make task4

# Task 5: Optimization (requires CUDD + Gurobi)
make task5
```

### Build all tasks at once:
```bash
make all
```

### Clean build artifacts:
```bash
make clean
```

---

## ✅ Testing Each Task

### Task 1: PNML Parsing

**Purpose:** Read and parse PNML files, verify consistency.

**Command:**
```bash
make test-task1
```

**Or manually:**
```bash
./test_task1 test_models/simple.pnml
./test_task1 test_models/mutex.pnml
./test_task1 test_models/producer_consumer.pnml
```

**Expected Output:**
```
========== TASK 1: PNML Parsing ==========
Parsing file: test_models/simple.pnml
  [+] Place: p1 tokens=1
  [+] Place: p2 tokens=0
  [+] Place: p3 tokens=0
  [+] Transition: t1
  [+] Transition: t2
  [+] Arc: p1 → t1
  ...
✓ Petri Net is VALID
========================================
```

---

### Task 2: Explicit Reachability

**Purpose:** Compute all reachable markings using BFS or DFS.

**Command:**
```bash
make test-task2
```

**Or manually:**
```bash
# Using BFS
./test_task2 test_models/simple.pnml bfs

# Using DFS
./test_task2 test_models/simple.pnml dfs

# Test other models
./test_task2 test_models/mutex.pnml bfs
./test_task2 test_models/producer_consumer.pnml bfs
```

**Expected Output:**
```
========== TASK 2: BFS Reachability ==========
Initial Marking: { p1:1 }

Exploring reachable states...
  Step 1 [t1]: { p2:1 }
  Step 2 [t2]: { p3:1 }

--- BFS Completed ---
Total reachable markings: 3
Execution time: 2 ms
========================================
```

---

### Task 3: BDD Symbolic Reachability

**Purpose:** Use Binary Decision Diagrams to compactly represent reachable states.

**Requirements:** CUDD library installed

**Command:**
```bash
make test-task3
```

**Or manually:**
```bash
./test_task3 test_models/simple.pnml
./test_task3 test_models/mutex.pnml
./test_task3 test_models/producer_consumer.pnml
```

**Expected Output:**
```
========== TASK 3: BDD Symbolic Reachability ==========
Building BDD representation...
BDD nodes created: 45
Reachable markings: 3
Execution time: 5 ms
Memory usage: 0.2 MB
========================================
```

---

### Task 4: Deadlock Detection

**Purpose:** Detect deadlocks using ILP formulation + BDD.

**Requirements:** CUDD + Gurobi installed

**Command:**
```bash
make test-task4
```

**Or manually:**
```bash
./test_task4 test_models/simple.pnml      # No deadlock
./test_task4 test_models/deadlock.pnml    # Has deadlock
./test_task4 test_models/mutex.pnml       # No deadlock
```

**Expected Output (no deadlock):**
```
========== TASK 4: DEADLOCK DETECTION TEST ==========
Reachable markings computed: 3
Running ILP-based deadlock detection...
✅ No deadlock found
========================================
```

**Expected Output (deadlock found):**
```
========== TASK 4: DEADLOCK DETECTION TEST ==========
Reachable markings computed: 4
Running ILP-based deadlock detection...
❌ Deadlock detected at marking: { p4:1 }
  - No transition is enabled
  - This state is reachable from initial marking
========================================
```

---

### Task 5: Optimization

**Purpose:** Find optimal marking that maximizes objective function.

**Requirements:** CUDD + Gurobi installed

**Command:**
```bash
make test-task5
```

**Or manually:**
```bash
./test_task5 test_models/simple.pnml test_models/weights_simple.txt
./test_task5 test_models/mutex.pnml test_models/weights_mutex.txt
```

**Expected Output:**
```
========== TASK 5: OPTIMIZATION TEST ==========
--- Objective Function Weights ---
  p1: 5
  p2: 3
  p3: -2

Reachable markings computed: 3
Solving optimization problem...

✅ Optimal marking found:
  Marking: { p1:1 }
  Objective value: 5
  Execution time: 8 ms
========================================
```

---

## 📝 Input Files

### PNML Files (.pnml)

**Format:** Standard PNML (Petri Net Markup Language)

**Example structure:**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<pnml>
  <net id="example" type="http://www.pnml.org/version-2009/grammar/ptnet">
    <page id="page1">
      
      <place id="p1">
        <name><text>Start</text></name>
        <initialMarking><text>1</text></initialMarking>
      </place>
      
      <transition id="t1">
        <name><text>Move</text></name>
      </transition>
      
      <arc id="a1" source="p1" target="t1">
        <inscription><text>1</text></inscription>
      </arc>
      
    </page>
  </net>
</pnml>
```

### Weights Files (.txt)

**Format:** Plain text, one weight per line

**Syntax:** `<place_id> <integer_weight>`

**Example:**
```txt
p1 5
p2 3
p3 -2
```

**Meaning:**
- Positive weights: desirable states
- Negative weights: undesirable states
- Zero: neutral

---

## 📊 Expected Results

### Test Model Characteristics:

| Model | Places | Transitions | Arcs | Markings | Deadlock? |
|-------|--------|-------------|------|----------|-----------|
| simple.pnml | 3 | 2 | 4 | 3 | No |
| mutex.pnml | 5 | 4 | 12 | 6 | No |
| producer_consumer.pnml | 4 | 2 | 8 | 3 | No |
| deadlock.pnml | 4 | 3 | 7 | 4 | Yes |

### Performance Benchmarks (Reference):

| Task | Model | Time (ms) | Memory (MB) |
|------|-------|-----------|-------------|
| Task 2 (BFS) | simple | < 5 | < 1 |
| Task 2 (BFS) | mutex | < 10 | < 2 |
| Task 3 (BDD) | simple | < 10 | < 1 |
| Task 3 (BDD) | mutex | < 20 | < 5 |
| Task 4 (ILP) | deadlock | < 50 | < 5 |
| Task 5 (ILP) | mutex | < 100 | < 10 |

*Note: Times may vary based on hardware*

---

## 🐛 Troubleshooting

### Issue: "No rule to make target"
**Cause:** Missing source file or wrong path

**Solution:**
```bash
# Check if all files exist
ls src/tests/test_task1.cpp
ls src/core/PetriNet.cpp

# Verify Makefile paths match your structure
```

---

### Issue: "undefined reference to CUDD functions"
**Cause:** CUDD library not installed or not linked

**Solution:**
```bash
# Install CUDD
sudo apt-get install libcudd-dev

# Or add library path
export LD_LIBRARY_PATH="/usr/local/lib:$LD_LIBRARY_PATH"
```

---

### Issue: "Cannot load PNML file"
**Cause:** File not found or invalid XML

**Solution:**
```bash
# Check file exists
ls -l test_models/simple.pnml

# Validate XML syntax online or use xmllint
xmllint --noout test_models/simple.pnml
```

---

### Issue: Compilation warnings about unused variables
**Cause:** Code optimization or incomplete implementation

**Solution:**
```bash
# Suppress warnings (temporary)
make CXXFLAGS="-std=c++17 -w -Iinclude -Isrc" task1
```

---

## 📚 References

### Petri Net Theory:
- Murata, T. (1989). "Petri nets: Properties, analysis and applications"
- Peterson, J. L. (1981). "Petri Net Theory and the Modeling of Systems"

### Tools & Libraries:
- **TinyXML2:** https://github.com/leethomason/tinyxml2
- **CUDD:** https://github.com/ivmai/cudd
- **Gurobi:** https://www.gurobi.com/documentation/
- **PNML Standard:** https://www.pnml.org/

### Course Materials:
- Assignment document: `mm-251-assignment.pdf`
- Lecture slides on BK-eLearning

---

## 👥 Team Information

**Group Members:**
- Member 1: [Student ID] - [Name]
- Member 2: [Student ID] - [Name]
- Member 3: [Student ID] - [Name]
- Member 4: [Student ID] - [Name]
- Member 5: [Student ID] - [Name]

**Instructor:** Dr. Van-Giang Trinh

**Course:** CO2011 - Mathematical Modeling  
**Semester:** 1 (2025-2026)

---

## 📅 Submission

**Deadline:** December 05, 2025, 23:00 (GMT+7)

**Submission format:**
```
Assignment-CO2011-CSE251-{StudentID1-StudentID2-...}.zip
```

**Contents:**
- Source code with this README
- Report (PDF, max 15 pages)
- Test PNML files

---

## ⚖️ License

This project is for academic use only. Redistribution without permission is prohibited.

---

## 📧 Contact

For questions or issues:
- Post on BK-eLearning forum
- Email instructor: [instructor email]
- Office hours: [time and location]

---

**Last Updated:** November 17, 2025  
**Version:** 1.0
