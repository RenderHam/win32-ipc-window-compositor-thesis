
# win32-ipc-window-compositor-thesis

A low-level desktop environment middleware engine that programmatically captures independent, running Windows applications, isolates their window messaging loops, strips their native OS borders/title bars, and embeds them dynamically into a single unified parent application container. 

This repository serves as the complete engineering implementation for a non-AI Computer Science thesis project addressing **deterministic window containment, geometric coordinate synchronization, and input routing semantics within the Win32 subsystem.**

---

## 🔬 Thesis Project Specifications

- **Project Title:** Design and Implementation of a Window-Parenting Compositor Subsystem Using Win32 Hooking and Shared-Memory Inter-Process Communication (IPC)
- **Primary Objective:** Mitigate desktop workspace context-switching fatigue by creating an explicit application containment framework without utilizing resource-heavy virtualization layers (e.g., Virtual Machines or Docker Display Servers).
- **Core Methodology:** Relies entirely on deterministic Windows user/kernel APIs (`user32.dll`, `kernel32.dll`), low-level window message hooking, and real-time bounding box matrix coordinate transformations.
- **Architectural Scope Restrictions:** 
  - **In-Scope:** Standard Win32/GDI productivity applications (e.g., Notepad, Calculator) running at identical Medium Integrity user isolation levels.
  - **Out-of-Scope:** Cross-integrity Administrator/UAC privilege bypasses and hardware-accelerated 3D game engine swap-chain hook injection (DirectX/Vulkan).

---

## 📂 Repository File Structure

```text
win32-ipc-window-compositor-thesis/
│
├── src/                      # Active engine source code
│   ├── main.py               # Main parent application shell entry point
│   ├── hijacker.py           # Window capture, layout parenting, and border stripping
│   ├── input_router.py       # Focus state machine and low-level mouse/keyboard hooking
│   └── layout_matrix.py      # Resizing and DPI-coordinate transformation matrices
│
├── benchmarks/               # Quantitative performance profiling tools
│   ├── input_latency.py      # Microsecond keyboard/mouse input propagation timers
│   └── resource_monitor.py   # OS-level memory allocation and CPU tracking tools
│
├── tests/                    # Standardized verification test cases
│   ├── test_gdi_notepad.py   # Baseline test profile for legacy GDI apps
│   └── test_modern_calc.py   # Baseline test profile for modern UI frameworks
│
├── docs/                     # Academic documentation and manuscript versions
│   ├── abstract.md
│   └── thesis_draft.docx
│
├── README.md                 # System configuration and execution guide
└── requirements.txt          # Explicit Python runtime dependencies
```

---

## 📊 Target Quantitative Validation Metrics

To pass the academic thesis panel evaluation, the compositor framework must programmatically validate and log the following strict engineering performance constraints during benchmarking phases:

1. **Input Propagation Delay (\(\Delta t_{input}\)):** Target threshold is **< 16,000 μ s** (under 16 milliseconds, matching a standard 60Hz display refresh window). Measured using high-resolution hardware counters (`time.perf_counter_ns()`) tracing path intervals from a low-level `WH_KEYBOARD_LL` hook down to the nested child's target thread receipt of a `WM_CHAR` packet.
2. **Frame Rendering Latency:** System stability measured during an automated 5Hz resize cycle. The child application's rendering layout matrix must drop **≤ 15%** of its native frames during active layout resizing loops.
3. **Computational Resource Overhead (\(O_{sys}\)):** Evaluated against standard system memory allocations via the Win32 `GetProcessMemoryInfo` and `GetProcessTimes` API blocks. Target footprint must consume **< 50 MB of dedicated RAM** and **< 2% single-core CPU utilization** during continuous execution states.

---

## 🛠️ System Requirements & Dependencies

- **Operating System:** Windows 10 or Windows 11 (64-bit architecture mandatory for Win32 API pointer mapping compatibility).
- **Runtime Environment:** Python 3.8 to Python 3.11.
- **Python Dependencies:** `pywin32` library bindings.

---

## 🚀 Installation & Quick Start

### 1. Clone the Repository
Open a terminal (Command Prompt or PowerShell) and clone this workspace to your local storage path:
```bash
git clone https://github.com
cd win32-ipc-window-compositor-thesis
```

### 2. Configure Virtual Environment & Install Dependencies
Create an isolated Python environment and install the required native Windows wrapper packages:
```bash
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
```

### 3. Verify Baseline Target App Visibility
Before running the main container shell, initialize an instance of standard Windows Notepad to serve as the baseline test handle:
```bash
start notepad.exe
```

### 4. Execute the Subsystem Engine
Launch the compositor shell script to capture, strip, and parent the running Notepad window process dynamically:
```bash
python src/main.py
```

---

## 📋 Comprehensive 14-Week Development Roadmap

- [ ] **Weeks 1-2:** Finalize Architecture Design, Complete Win32 API Vector Mapping, and Secure Formal Advisor Abstract Sign-off.
- [ ] **Weeks 3-5:** Complete the Window Hijacking Module, Handle Style Mask Overrides (`GWL_STYLE`), and Execute Visual Containment (`SetParent`).
- [ ] **Weeks 6-8:** Implement Focus Routing Overrides, Mouse Coordinate Matrix Transforms, and Build the Resizing Loop Shell.
- [ ] **Weeks 9-11:** Deploy Standardized Profilers, Record Macro Metrics Across GDI/Modern Apps, and Generate Data Chapter Graph Outputs.
- [ ] **Weeks 12-14:** Refine Academic Manuscript Drafts, Finalize Performance Limits/Failure Analysis Sections, and Complete Thesis Panel Presentation Defense.
