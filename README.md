<div align="center">
  <p>
    <a href="https://www.neuracore.com" target="_blank">
      <img width="100%" src="./docs/assets/neuracore_logo.jpg" alt="Neuracore banner"></a>
  </p>



<div align="center">

[![Downloads](https://static.pepy.tech/badge/neuracore)](https://pepy.tech/project/neuracore)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![PyPI - Version](https://img.shields.io/pypi/v/neuracore)](https://pypi.org/project/neuracore/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Last Commit](https://img.shields.io/github/last-commit/NeuracoreAI/neuracore)](https://github.com/NeuracoreAI/neuracore/commits/main)

</div>

<p align="center">
  Join our community!
</p>
<p align="center">
  <a target="_blank" href="https://discord.gg/DF5m8V6nbD"><img src="https://img.shields.io/badge/Discord-Join%20Server-5865F2?style=for-the-badge&logo=discord" alt="Discord" /></a>
</p>

<p align="center">
  Getting started
</p>
<p align="center">
  <a target="_blank" href="https://www.neuracore.com/try-on-colab"><img src="https://img.shields.io/badge/Try%20on%20Google%20Colab-303030?style=for-the-badge&logo=googlecolab" alt="Discord" /></a>
</p>

<div align="center">

</br> 


</div>

## 🤖 What is Neuracore?

**Neuracore** is a high-performance **Robot Learning Infrastructure** designed for large-scale data collection, real-time visualization, and cloud-native training. Neuracore enables researchers and engineers to stream complex, high-frequency robotics data from physical hardware to the cloud with minimal overhead, providing a unified platform for training and deploying state-of-the-art (SOTA) robot policies.

It is **fast**, **accurate**, and **easy to use**. Built for [Teleoperation](https://docs.neuracore.com/tasks/teleop/), [Data Logging](https://docs.neuracore.com/tasks/logging/), [Cloud Training](https://docs.neuracore.com/tasks/training/), and [Deployment](https://docs.neuracore.com/tasks/deployment/).

<a href="https://www.neuracore.com/platform" target="_blank">
  <img width="100%" src="https://github.com/user-attachments/assets/5f6e9f12-185f-4050-9e71-2e5712d49b03" alt="Neuracore Data Synchronization">
</a>

## 🌟 Key Features

- 🚀 **High-Frequency Streaming**: Use the **Data Daemon** to log multi-modal sensor data (joint poses, RGB-D, force) at high frequencies.
- 📊 **Real-Time Visualization**: Synchronize and visualize complex datasets in real-time through the Neuracore dashboard.
- ☁️ **Cloud-Native Training**: Launch training runs for **Diffusion Policy**, **ACT**, and more directly on scalable cloud infrastructure.
- 🤖 **Edge Deployment**: Deploy trained policies with optimized inference engines for low-latency robot control.


# 🛠️ Installation
To install the basic package for data logging and visualization:

```bash
pip install neuracore
```

**Note:** installing the `ffmpeg` binary is recommended for faster video encoding (during recording) and decoding (during playback/import). If not available, Neuracore falls back to PyAV for encoding.

Linux (Debian/Ubuntu):

```bash
sudo apt-get update && sudo apt-get install -y ffmpeg
```

For training and ML development:
```bash
pip install neuracore[ml]
```

For bulk importing datasets:
```bash
pip install neuracore[import]
```

To run our examples:
```bash
pip install neuracore[examples]
```

# 🍰 A Short Taste
Here is a short taste on what neuracore can do.
For a detailed walk-through, please refer to the [tutorial](./docs/tutorial.md) and [documentation](#-documentation), or [try it yourself on Google Colab](https://www.neuracore.com/try-on-colab).
```python
import neuracore as nc

# Login and setup robot
nc.login()
nc.connect_robot(robot_name="MyRobot", urdf_path="/path/to/robot.urdf")

# High-frequency logging
nc.start_recording()
nc.log_joint_positions(positions={'j1': 0.1})
nc.log_rgb(name="camera", rgb=image_array)
nc.stop_recording()

# Deploy policy for real-time inference
policy = nc.policy(train_run_name="MyJob")
action = policy.predict()
```

# 📚 Documentation
- [Examples](./examples/README.md)
- [Tutorial](./docs/tutorial.md)
- [Training](./docs/training.md)
- [Command Line Tools](./docs/commandline.md)
- [Dataset Importer](./docs/dataset_importer.md)
- [Environment Variables](./docs/environment_variable.md)
- [Contribution Guide](./docs/contribution_guide.md)
- [Data Daemon](./docs/data_daemon.md)

# 💬 Community

We are building Neuracore to help everyone accelerate their robot learning workflows, and we'd love to hear from you! Join our community to get help, share ideas, and stay updated:

- [Discord](https://discord.gg/DF5m8V6nbD) - Chat with the community and get support
- [GitHub Issues](https://github.com/NeuracoreAI/neuracore/issues) - Report bugs and request features

## ✨ Algorithms & Performance

Neuracore supports state-of-the-art robot learning algorithms, optimized for throughput and stability. Tables below show training/inference capabilities.

<br>

<details open><summary>Imitation Learning</summary>

Refer to the [Imitation Learning Docs](https://docs.neuracore.com/tasks/imitation/) for details.

| Algorithm | Type | Cloud Training | Inference Speed (ms) | Status |
| :--- | :--- | :---: | :---: | :---: |
| **Diffusion Policy** | Imitation | ✅ | 15-30 | Production |
| **ACT** | Transformer | ✅ | 20-40 | Beta |
| **VQ-BeT** | Discrete | ✅ | 10-25 | Beta |

</details>

<br>

## 🧩 Integrations

Neuracore integrates seamlessly with leading robotics simulators and machine learning platforms.

<a href="https://docs.neuracore.com/integrations/" target="_blank">
  <img width="100%" src="https://github.com/NeuracoreAI/neuracore/raw/main/docs/assets/integrations_banner.png" alt="Neuracore integrations banner">
</a>

| Simulators | Frameworks | ML Platforms |
| :---: | :---: | :---: |
| Mujoco, PyBullet, Isaac Gym | ROS1/ROS2, LeRobot, Bigym | Hugging Face, W&B, CometML |

# 🧾 Citation

If you use Neuracore in your research, please consider citing:

```bibtex
@software{Neuracore,
  author = {Neuracore Team},
  title = {Neuracore},
  month = {January},
  year = {2026},
  url = {https://github.com/NeuracoreAI/neuracore}
}
