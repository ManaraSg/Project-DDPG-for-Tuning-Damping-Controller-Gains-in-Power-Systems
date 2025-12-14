# DDPG-for-Tuning-Damping-Controller-Gains-in-Power-Systems
ECE394K Course project implementing a Deep Deterministic Policy Gradient (DDPG) reinforcement learning framework to automatically tune supplementary damping controller gains in power systems with high inverter-based resource (IBR) penetration.

## Overview
This project integrates **DIgSILENT PowerFactory** with a **DDPG agent** to optimize damping controller parameters across diverse generation mixes. The system is evaluated on a modified IEEE 9-bus test system under three-phase fault disturbances.

## Repository Contents
```
Project-DDPG-for-Tuning-Damping-Controller-Gains-in-Power-Systems/
│
├── ddpg_based_damping_control_powerfactory.ipynb  # Main implementation notebook
├── Nine-bus Grid Cortex Feb2025.pfd               # PowerFactory modified 9-bus test system
├── requirements.txt                                # Python dependencies
└── README.md                                      
```

## Prerequisites
- **Operating System:** Windows (required for DIgSILENT PowerFactory)
- **DIgSILENT PowerFactory:** Version 2024 SP4 with valid license
- **Python:** 3.10 (PowerFactory-compatible version)
  
## Installation & Setup

### Step 1: Make Virtual Environment
```bash
# Create virtual environment
python -m venv .venv

# Activate on Windows
.venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### Step 2: Install PowerFactory Python API
DIgSILENT PowerFactory must be installed separately with a valid license. After installation, verify the Python API path in your notebook:
```python
import sys
sys.path.append(r"C:\Program Files\DIgSILENT\PowerFactory 2024 SP4\Python\3.10")
import powerfactory as pf
```
**Important:** Ensure PowerFactory is not running in the background before importing the API.

## Running the Project

### 1. Verify PowerFactory Installation
```python
import sys
sys.path.append(r"C:\Program Files\DIgSILENT\PowerFactory 2024 SP4\Python\3.10")
import powerfactory as pf

app = pf.GetApplication()
if app is None:
    print("PowerFactory not accessible - check installation and license")
else:
    print("PowerFactory successfully connected!")
```

### 2. Configure PowerFactory Project File
The notebook imports the 9-bus test system from `Nine-bus Grid Cortex Feb2025.pfd`. Make sure to update the file path in the notebook to match your local directory:
```python
# Locate this block in the notebook and verify the path
import_path = r'Nine-bus Grid Cortex Feb2025.pfd'
imp = app.GetFromStudyCase('ComPfdImport')
imp.g_file = import_path
imp.activatePrj = 1
imp.Execute()
```

### 3. Launch Jupyter Notebook
```bash
# Make sure your environment is activated
jupyter notebook ddpg_based_damping_control_powerfactory.ipynb
```
