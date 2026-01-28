# AAE5303 Environment Setup Report

> **Important:** Follow this structure exactly in your submission README.  
> Your goal is to demonstrate **evidence, process, problem-solving, and reflection** — not only screenshots.

---

## 1. System Information

**Laptop model:**  
_[LAPTOP-HL6F1HDG]_

**CPU / RAM:**  
_[Intel(R) Core(TM) i5-1035G1 CPU @ 1.00GHz   1.19 GHz]_

**Host OS:**  
_[Windows 10]_

**Linux/ROS environment type:**  
_[Choose one:]_
- [ ] Dual-boot Ubuntu
- [✓ ] WSL2 Ubuntu
- [ ] Ubuntu in VM (UTM/VirtualBox/VMware/Parallels)
- [ ] Docker container
- [ ] Lab PC
- [ ] Remote Linux server

---

## 2. Python Environment Check

### 2.1 Steps Taken

Describe briefly how you created/activated your Python environment:

**Tool used:**  
_[venv]_

**Key commands you ran:**
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

**Any deviations from the default instructions:**  
_[None]_

### 2.2 Test Results

Run these commands and paste the actual terminal output (not just screenshots):

```bash
python scripts/test_python_env.py
```

**Output:**
```
[========================================
AAE5303 Environment Check (Python + ROS)
Goal: help you verify your environment and understand what each check means.
========================================

Step 1: Environment snapshot
  Why: We capture platform/Python/ROS variables to diagnose common setup mistakes (especially mixed ROS env).
Step 2: Python version
  Why: The course assumes Python 3.10+; older versions often break package wheels.
Step 3: Python imports (required/optional)
  Why: Imports verify packages are installed and compatible with your Python version.
Step 4: NumPy sanity checks
  Why: We run a small linear algebra operation so success means more than just `import numpy`.
Step 5: SciPy sanity checks
  Why: We run a small FFT to confirm SciPy is functional (not just installed).
Step 6: Matplotlib backend check
  Why: We generate a tiny plot image (headless) to confirm plotting works on your system.
Step 7: OpenCV PNG decoding (subprocess)
  Why: PNG decoding uses native code; we isolate it so corruption/codec issues cannot crash the whole report.
Step 8: Open3D basic geometry + I/O (subprocess)
  Why: Open3D is a native extension; ABI mismatches can segfault. Subprocess isolation turns crashes into readable failures.
Step 9: ROS toolchain checks
  Why: The course requires ROS tooling. This check passes if ROS 2 OR ROS 1 is available (either one is acceptable).
  Action: building ROS 2 workspace package `env_check_pkg` (this may take 1-3 minutes on first run)...
  Action: running ROS 2 talker/listener for a few seconds to verify messages flow...
Step 10: Basic CLI availability
  Why: We confirm core commands exist on PATH so students can run the same commands as in the labs.

=== Summary ===
✅ Environment: {
  "platform": "Linux-6.6.87.2-microsoft-standard-WSL2-x86_64-with-glibc2.35",
  "python": "3.10.12",
  "executable": "/home/everyonemoon/aae5303-env-check/.venv/bin/python",
  "cwd": "/home/everyonemoon/aae5303-env-check",
  "ros": {
    "ROS_VERSION": "2",
    "ROS_DISTRO": "humble",
    "ROS_ROOT": null,
    "ROS_PACKAGE_PATH": null,
    "AMENT_PREFIX_PATH": "/opt/ros/humble",
    "CMAKE_PREFIX_PATH": null
  }
}
✅ Python version OK: 3.10.12
✅ Module 'numpy' found (v2.2.6).
✅ Module 'scipy' found (v1.15.3).
✅ Module 'matplotlib' found (v3.10.8).
✅ Module 'cv2' found (v4.13.0).
✅ Module 'rclpy' found (vunknown).
✅ numpy matrix multiply OK.
✅ numpy version 2.2.6 detected.
✅ scipy FFT OK.
✅ scipy version 1.15.3 detected.
✅ matplotlib backend OK (Agg), version 3.10.8.
✅ OpenCV OK (v4.13.0), decoded sample image 128x128.
✅ Open3D OK (v0.19.0), NumPy 2.2.6.
✅ Open3D loaded sample PCD with 8 pts and completed round-trip I/O.
✅ ROS 2 CLI OK: /opt/ros/humble/bin/ros2
✅ ROS 1 tools not found (acceptable if ROS 2 is installed).
✅ colcon found: /usr/bin/colcon
✅ ROS 2 workspace build OK (env_check_pkg).
✅ ROS 2 runtime OK: talker and listener exchanged messages.
✅ Binary 'python3' found at /home/everyonemoon/aae5303-env-check/.venv/bin/python3

All checks passed. You are ready for AAE5303 🚀]
```

```bash
python scripts/test_open3d_pointcloud.py
```

**Output:**
```
[ℹ️ Loading /home/everyonemoon/aae5303-env-check/data/sample_pointcloud.pcd ...
✅ Loaded 8 points.
   • Centroid: [0.025 0.025 0.025]
   • Axis-aligned bounds: min=[0. 0. 0.], max=[0.05 0.05 0.05]
✅ Filtered point cloud kept 7 points.
✅ Wrote filtered copy with 7 points to /home/everyonemoon/aae5303-env-check/data/sample_pointcloud_copy.pcd
   • AABB extents: [0.05 0.05 0.05]
   • OBB  extents: [0.08164966 0.07071068 0.05773503], max dim 0.0816 m
🎉 Open3D point cloud pipeline looks good.]
```

**Screenshot:**  
_[<img width="1856" height="1020" alt="image" src="https://github.com/user-attachments/assets/39134ab0-8ffb-4843-9717-f4dbd8a1e76f" />
]_

![Python Tests Passing](path/to/your/screenshot.png)

---

## 3. ROS 2 Workspace Check

### 3.1 Build the workspace

Paste the build output summary (final lines only):

```bash
source /opt/ros/humble/setup.bash
colcon build
```

**Expected output:**
```
Summary: 1 package finished [x.xx s]
```

**Your actual output:**
```
[Starting >>> env_check_pkg
Finished <<< env_check_pkg [0.18s]                

Summary: 1 package finished [0.49s]]
```

### 3.2 Run talker and listener

Show both source commands:

```bash
source /opt/ros/humble/setup.bash
source install/setup.bash
```

**Then run talker:**
```bash
ros2 run env_check_pkg talker.py
```

**Output (3–4 lines):**
```
[[INFO] [1769574251.943347507] [env_check_pkg_talker]: AAE5303 talker ready (publishing at 2 Hz).
[INFO] [1769574252.443597536] [env_check_pkg_talker]: Publishing: 'AAE5303 hello #0'
[INFO] [1769574252.921798494] [env_check_pkg_talker]: Publishing: 'AAE5303 hello #1'
[INFO] [1769574253.400790077] [env_check_pkg_talker]: Publishing: 'AAE5303 hello #2'
[INFO] [1769574253.880079055] [env_check_pkg_talker]: Publishing: 'AAE5303 hello #3'
[INFO] [1769574254.358932097] [env_check_pkg_talker]: Publishing: 'AAE5303 hello #4'
[INFO] [1769574254.837871464] [env_check_pkg_talker]: Publishing: 'AAE5303 hello #5'
[INFO] [1769574255.317026212] [env_check_pkg_talker]: Publishing: 'AAE5303 hello #6'
^C[INFO] [1769574255.411294748] [rclcpp]: signal_handler(SIGINT/SIGTERM)]
```

**Run listener:**
```bash
ros2 run env_check_pkg listener.py
```

**Output (3–4 lines):**
```
[[INFO] [1769574462.642234758] [env_check_pkg_listener]: AAE5303 listener awaiting messages.
[INFO] [1769574462.797713943] [env_check_pkg_listener]: I heard: 'AAE5303 hello #51'
[INFO] [1769574463.276951103] [env_check_pkg_listener]: I heard: 'AAE5303 hello #52'
[INFO] [1769574463.755695727] [env_check_pkg_listener]: I heard: 'AAE5303 hello #53'
[INFO] [1769574464.234792437] [env_check_pkg_listener]: I heard: 'AAE5303 hello #54'
[INFO] [1769574464.714016567] [env_check_pkg_listener]: I heard: 'AAE5303 hello #55'
[INFO] [1769574465.192678703] [env_check_pkg_listener]: I heard: 'AAE5303 hello #56'
[INFO] [1769574465.672170706] [env_check_pkg_listener]: I heard: 'AAE5303 hello #57']
```

**Alternative (using launch file):**
```bash
ros2 launch env_check_pkg env_check.launch.py
```

**Screenshot:**  
_[<img width="1856" height="1020" alt="image" src="https://github.com/user-attachments/assets/14b140e7-b9ca-460e-a3d1-69445316931f" />
]_

![Talker and Listener Running](<img width="1856" height="1020" alt="image" src="https://github.com/user-attachments/assets/ae36186a-0d1b-4340-964e-3d4f4fab078c" />
)

---

## 4. Problems Encountered and How I Solved Them

> **Note:** Write 2–3 issues, even if small. This section is crucial — it demonstrates understanding and problem-solving.

### Issue 1: [ROS requirement not satisfied
]

**Cause / diagnosis:**  
_[ROS2 installed on WSL

Running scripts in Windows/Error Terminal]_

**Fix:**  
_[The exact command/config change you used to solve it]_

```bash
[source /opt/ros/humble/setup.bash]
```

**Reference:**  
_[AI assistant]_

---

### Issue 2: [No module named 'catkin_pkg']

**Cause / diagnosis:**  
_[colcon build was run with Python venv activated]_

**Fix:**  
_[The exact command/config change you used to solve it]_

```bash
[sudo apt install -y python3-catkin-pkg]
```

**Reference:**  
_[AI assistant]_

---

### Issue 3 (Optional): [Multiple repositories were cloned, resulting in disordered paths.]

**Cause / diagnosis:**  
_[The smoke test/colcon was running between different warehouses.

The environment variables were inconsistent.]_

**Fix:**  
_[The exact command/config change you used to solve it]_

```bash
[rm -rf PolyU-AAE5303-env-smork-test
]
```

**Reference:**  
_[ AI assistant]_

---

## 5. Use of Generative AI (Required)

Choose one of the issues above and document how you used AI to solve it.

> **Goal:** Show critical use of AI, not blind copying.

### 5.1 Exact prompt you asked

**Your prompt:**
```
[为什么我的ROS2已经安装但检测不到，catkin_pkg找不到，该怎么解决这些问题]
```

### 5.2 Key helpful part of the AI's answer

**AI's response (relevant part only):**
```
[# 1) 安装 ROS2 构建所需系统依赖
sudo apt update
sudo apt install -y python3-catkin-pkg python3-colcon-common-extensions

# 2) 进入 ROS2 workspace 并清理旧构建产物
cd ~/aae5303-env-check/ros2_ws
rm -rf build install log

# 3) source ROS2 并重新编译
source /opt/ros/humble/setup.bash
colcon build --packages-select env_check_pkg --event-handlers console_direct+
]
```

### 5.3 What you changed or ignored and why

Explain briefly:
- Did the AI recommend something unsafe?
- Did you modify its solution?
- Did you double-check with official docs?

**Your explanation:**  
_[AI did not recommend unsafe content.The commands provided mainly involve system package installation (apt install) and cleanup of the workspace (deleting build/install/log), which are routine and controllable environment configuration operations. The deletion commands (such as rm -rf build install log or deleting duplicate repository directories) all involve project files in the user's directory and do not involve critical system directories.
The solution has been modified.

Based on the actual error path showing `execute_process(.../.venv/bin/python3 ...)`, I stopped trying to build ROS2 within the venv instance. Instead, I performed a colcon build in a new terminal without an activated venv instance, and strictly changed the execution directory of the colcon build to `ros2_ws/`. Furthermore, I abandoned using `ros2 --version` to check the installation status and instead used `ros2 run demo_nodes_*` or `ros2 pkg list` to verify it.]_

### 5.4 Final solution you applied

Show the exact command or file edit that fixed the problem:

```bash
[
sudo apt update
sudo apt install -y python3-catkin-pkg python3-colcon-common-extensions

cd ~/aae5303-env-check/ros2_ws
rm -rf build install log

source /opt/ros/humble/setup.bash
colcon build --packages-select env_check_pkg --event-handlers console_direct+

# 4) source 工作空间并运行（两个终端分别运行 talker/listener）
source install/setup.bash
ros2 run env_check_pkg listener
# 在另一个新终端中：
source /opt/ros/humble/setup.bash
cd ~/aae5303-env-check/ros2_ws
source install/setup.bash
ros2 run env_check_pkg talker

rm -rf ~/PolyU-AAE5303-env-smork-test]
```

**Why this worked:**  
_[`python3-catkin-pkg` and `colcon` are system dependencies in the ROS2 build chain. Installing them using `apt` ensures consistency with the system's Python/ROS2 environment.
Running `colcon build` under `ros2_ws/` and cleaning up `build/install/log` avoids secondary failures caused by old caches and incorrect paths.
Avoid building ROS2 in `.venv` files to prevent `ament/colcon` from mistakenly using `.venv/bin/python3`, causing dependencies to be invisible and resolving `catkin_pkg` missing errors at the root.
Using `ros2 run env_check_pkg listener/talker` (without `.py`) conforms to ROS2's "run installed executable targets" mechanism, ensuring that executables are correctly discovered and run.]_

---

## 6. Reflection (3–5 sentences)

Short but thoughtful:

- What did you learn about configuring robotics environments?
- What surprised you?
- What would you do differently next time (backup, partitioning, reading error logs, asking better AI questions)?
- How confident do you feel about debugging ROS/Python issues now?

**Your reflection:**

_[I learned that configuring a robotics environment is often more about managing system environments and dependencies than writing code, especially when mixing ROS2 and Python virtual environments. I was surprised that activating a Python virtual environment could silently break ROS2 builds by redirecting the Python interpreter used by colcon and ament. Next time, I will clearly separate system-level ROS installations from Python project environments, read full error logs before acting, and provide more precise context when asking AI for help. After resolving these issues, I feel confident in debugging common ROS/Python environment and build problems.]_

---

## 7. Declaration

✅ **I confirm that I performed this setup myself and all screenshots/logs reflect my own environment.**

**Name:**  
_[ZhongZiyi]_

**Student ID:**  
_[25075125G]_

**Date:**  
_[2026/1/28]_

---

## Submission Checklist

Before submitting, ensure you have:
- [✓] Filled in all system information
- [✓] Included actual terminal outputs (not just screenshots)
- [✓] Provided at least 2 screenshots (Python tests + ROS talker/listener)
- [✓] Documented 2–3 real problems with solutions
- [✓] Completed the AI usage section with exact prompts
- [✓] Written a thoughtful reflection (3–5 sentences)
- [✓] Signed the declaration

---

**End of Report**
