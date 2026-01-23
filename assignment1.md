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
  
<img width="1092" height="1260" alt="image" src="https://github.com/user-attachments/assets/8d60eb93-d9cf-4fca-a824-a97d43d69582" />

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
(.venv) root@b15bb95db334:~/PolyU-AAE5303-env-smork-test# ros2 run env_check_pkg talker
[INFO] [1769158653.178400040] [env_check_pkg_talker]: AAE5303 talker ready (publishing at 2 Hz).
[INFO] [1769158653.678569379] [env_check_pkg_talker]: Publishing: 'AAE5303 hello #0'
[INFO] [1769158654.133237595] [env_check_pkg_talker]: Publishing: 'AAE5303 hello #1'
```

**Run listener:**

```bash
ros2 run env_check_pkg listener.py
```

**Listener output (3–4 lines):**

```text
(.venv) root@b15bb95db334:~/PolyU-AAE5303-env-smork-test# ros2 run env_check_pkg listener
[INFO] [1769158699.630108148] [env_check_pkg_listener]: AAE5303 listener awaiting messages.
```

**Alternative (if you used the launch file instead):**

```bash
ros2 launch env_check_pkg env_check.launch.py
```

**Screenshot:**  
<img width="1095" height="534" alt="image" src="https://github.com/user-attachments/assets/76aa4a43-7313-4e5b-9008-09b5105f25ce" />
  


---

## 4. Problems Encountered and How I Solved Them

> **Important:** Write at least 2 real issues, even if they were small. This shows your problem‑solving process.

### Issue 1: _[Cursor-generated Dockerfile failed to build Ubuntu 22.04 + ROS 2 Humble environment]_ 

**Cause / diagnosis:**  
_[The Dockerfile automatically generated by Cursor was poorly written , resulting in failure to build a Docker image with ROS 2.]_  

**Fix (exact command or change):**  

```bash
# 1. Use the official ROS 2 image to avoid manual build issues
docker pull osrf/ros:humble-desktop-jammy

# 2. Run the container to verify the environment
docker run -it --name AAE5303_assignment1 osrf/ros:humble-desktop-jammy

# 3. Load the ROS 2 environment inside the container
source /opt/ros/humble/setup.bash
```

**Reference (where you got help):**  

<img width="933" height="354" alt="image" src="https://github.com/user-attachments/assets/e759cfb2-adb5-4e7f-bd37-9e4ba1fb95ce" />


---

### Issue 2: _[Failed to create Docker container via Cursor (permission denied error)]_

**Cause / diagnosis:**  
_[The user account used within Cursor was not added to the docker group, 
leading to insufficient permissions to interact with the Docker daemon. 
This resulted in "permission denied" errors when executing Docker commands (e.g., docker run, docker pull) through Cursor.]_  

**Fix (exact command or change):**

```bash
# Add current user to the docker group (execute on host machine)
sudo usermod -aG docker $USER

# Apply group changes immediately (no need to log out/log in)
newgrp docker

# Verify user is successfully added to docker group
groups $USER | grep docker

# Test Docker access to confirm permission issue is resolved
docker ps
```

**Reference:**  

<img width="924" height="369" alt="image" src="https://github.com/user-attachments/assets/e143b45c-46d4-448d-a8b9-a3d1cb884bb1" />



---


## 5. Use of Generative AI (Required)

Choose **one** of the issues above and document how you used AI to solve it.

### 5.1 Exact prompt you asked

**Your prompt (copy‑paste, not a summary):**

```text
[docker file是什么]
```

### 5.2 Key helpful part of the AI's answer

**AI's response (only the relevant part):**

```text
[Dockerfile 是一个纯文本的“构建脚本”，用来描述如何一步步制作一个 Docker 镜像（image）。Docker 会按顺序读取其中的指令，执行后把结果打包成镜像；你再用镜像启动容器（container）。]
```

### 5.3 What you changed or ignored and why

_[Cursor defaults to creating a ROS 2 Docker environment using a Dockerfile. 
However, this approach is slow and ultimately failed, even though the TA succeeded with it in the video. 
This method is inferior to directly using the official ROS 2 image. This was a detour that AI led me down.]_

### 5.4 Final solution you applied

**Final command/code you actually used:**

```bash

docker pull osrf/ros:humble-desktop-jammy

docker run -it --name ros2-humble osrf/ros:humble-desktop-jammy
```

**Why this worked:**  
_[Using the official ROS 2 image bypasses the complex and error-prone process of building a custom Dockerfile (which suffered from network timeouts and missing configurations in Cursor). 
The pre-built image is optimized for ROS 2, ensuring all dependencies and environment settings are correctly configured, resulting in a faster, more stable setup with no manual troubleshooting required.]_  

---

## 6. Reflection (3–5 sentences)

_[Write 3–5 thoughtful sentences here. For example: what you learned about configuring robotics environments, what surprised you, what you’d do differently next time, and how confident you feel about debugging ROS/Python issues now.]_

---

## 7. Declaration

✅ **I confirm that I performed this setup myself and all screenshots/logs reflect my own environment.**

**Name:**  
_[CHANG Jianshuo]_

**Student ID:**  
_[25043804g]_

**Date:**  
_[2026]_

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
