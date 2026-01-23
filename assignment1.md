# AAE5303 Environment Setup Report — Assignment 1



## 1. System Information

**Laptop model:**  
_[HP Omen 11 Gaming Laptop]_

**CPU / RAM:**  
_[Intel Core i9-14900HX, 32GB RAM]_

**Host OS:**  
_[Ubuntu 22.04]_

**Linux/ROS environment type (choose one):**  
_[ WSL2 Ubuntu ]_

---

## 2. Python Environment Check

### 2.1 Steps Taken

I created and activated a venv environment with python3 -m venv .venv and source .venv/bin/activate, then installed dependencies via pip install

**Tool used:**  
_venv_  

**Key commands you ran (edit as needed):**

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

**Any deviations from the default instructions:**  
_None_

### 2.2 Test Results

Run these commands in your environment and paste the **actual terminal output** (not just screenshots).

Command:

```bash
python scripts/test_python_env.py
```

**Output (paste your real output here):**

```text
(.venv) root@b15bb95db334:~/PolyU-AAE5303-env-smork-test/scripts# python test_python_env.py
========================================
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
  "executable": "/root/PolyU-AAE5303-env-smork-test/.venv/bin/python",
  "cwd": "/root/PolyU-AAE5303-env-smork-test/scripts",
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
✅ Binary 'python3' found at /root/PolyU-AAE5303-env-smork-test/.venv/bin/python3

All checks passed. You are ready for AAE5303 🚀

```

Command:

```bash
python scripts/test_open3d_pointcloud.py
```

**Output (paste your real output here):**

```text
(.venv) root@b15bb95db334:~/PolyU-AAE5303-env-smork-test/scripts# python test_open3d_pointcloud.py
ℹ️ Loading /root/PolyU-AAE5303-env-smork-test/data/sample_pointcloud.pcd ...
✅ Loaded 8 points.
   • Centroid: [0.025 0.025 0.025]
   • Axis-aligned bounds: min=[0. 0. 0.], max=[0.05 0.05 0.05]
✅ Filtered point cloud kept 7 points.
✅ Wrote filtered copy with 7 points to /root/PolyU-AAE5303-env-smork-test/data/sample_pointcloud_copy.pcd
   • AABB extents: [0.05 0.05 0.05]
   • OBB  extents: [0.08164966 0.07071068 0.05773503], max dim 0.0816 m
🎉 Open3D point cloud pipeline looks good.
```

**Screenshot:**  
  

Caption: _Python tests passing_

---

## 3. ROS 2 Workspace Check

### 3.1 Build the workspace

Run the following (adapt path if needed), then paste the **build summary**.

```bash
source /opt/ros/humble/setup.bash
colcon build
```

**Expected output example:**

```text
Summary: 1 package finished [x.xx s]
```

**Your actual output :**

```text
(.venv) root@b15bb95db334:~/PolyU-AAE5303-env-smork-test# source /opt/ros/humble/setup.bash
colcon build
Starting >>> env_check_pkg
Finished <<< env_check_pkg [0.86s]
```

### 3.2 Run talker and listener

First source the environments:

```bash
source /opt/ros/humble/setup.bash
source install/setup.bash
```

**Run talker:**

```bash
ros2 run env_check_pkg talker.py
```

**Talker output (3–4 lines):**

```text
[Paste 3–4 lines of talker output here]
```

**Run listener:**

```bash
ros2 run env_check_pkg listener.py
```

**Listener output (3–4 lines):**

```text
[Paste 3–4 lines of listener output here]
```

**Alternative (if you used the launch file instead):**

```bash
ros2 launch env_check_pkg env_check.launch.py
```

**Screenshot:**  
_[Insert one screenshot showing talker + listener running in separate terminals or panes]_  

Caption: _Talker and listener running_

---

## 4. Problems Encountered and How I Solved Them

> **Important:** Write at least 2 real issues, even if they were small. This shows your problem‑solving process.

### Issue 1: _[Write the exact error message or problem]_ 

**Cause / diagnosis:**  
_[Explain what you think caused it]_  

**Fix (exact command or change):**  

```bash
[Put the actual command(s) or config changes you used here]
```

**Reference (where you got help):**  
_[Official ROS docs? StackOverflow? AI assistant? Other?]_

---

### Issue 2: _[Another real error or roadblock]_

**Cause / diagnosis:**  
_[Explain what you think caused it]_  

**Fix (exact command or change):**

```bash
[Put the actual command(s) or config changes you used here]
```

**Reference:**  
_[Official docs / forum / AI / etc.]_

---

### Issue 3 (Optional): _[Title of issue]_ 

**Cause / diagnosis:**  
_[Explain what you think caused it]_  

**Fix (exact command or change):**

```bash
[Put the actual command(s) or config changes you used here]
```

**Reference:**  
_[Official docs / forum / AI / etc.]_

---

## 5. Use of Generative AI (Required)

Choose **one** of the issues above and document how you used AI to solve it.

### 5.1 Exact prompt you asked

**Your prompt (copy‑paste, not a summary):**

```text
[Paste the exact message you sent to the AI here]
```

### 5.2 Key helpful part of the AI's answer

**AI's response (only the relevant part):**

```text
[Quote only the part of the AI answer that helped you]
```

### 5.3 What you changed or ignored and why

_[Explain briefly: did the AI suggest anything unsafe? What did you change? Did you cross‑check with docs?]_

### 5.4 Final solution you applied

**Final command/code you actually used:**

```bash
[Paste the final command(s) or code you used]
```

**Why this worked:**  
_[Short explanation of why the fix makes sense]_  

---

## 6. Reflection (3–5 sentences)

_[Write 3–5 thoughtful sentences here. For example: what you learned about configuring robotics environments, what surprised you, what you’d do differently next time, and how confident you feel about debugging ROS/Python issues now.]_

---

## 7. Declaration

✅ **I confirm that I performed this setup myself and all screenshots/logs reflect my own environment.**

**Name:**  
_[Your name]_

**Student ID:**  
_[Your student ID]_

**Date:**  
_[Date of submission]_

---

## Submission Checklist

Before submitting, make sure you have:

- **System information** fully filled in
- **Actual terminal outputs** pasted (for Python tests and ROS workspace)
- **At least 2 screenshots** (Python tests + ROS talker/listener)
- **2–3 real problems** documented with causes, fixes, and references
- **AI usage section** completed with real prompts and answers
- **Reflection** (3–5 sentences) written
- **Declaration** filled and “signed” with your name and date

---

**End of Report**