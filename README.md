<div align="center">
  <a href="https://www.neuracore.com" target="_blank">
    <img width="80%" src="./docs/assets/Neuracore_banner.png" alt="Neuracore banner"></a>
</div>

<br>

<div align="center">
    <a href="https://pypi.org/project/neuracore/"><img src="https://img.shields.io/pypi/v/neuracore?logo=pypi&logoColor=white" alt="PyPI - Version"></a>
    <a href="https://www.python.org/downloads/"><img src="https://img.shields.io/badge/python-3.10+-blue.svg" alt="Python 3.10+"></a>
    <a href="https://pepy.tech/project/neuracore"><img src="https://static.pepy.tech/badge/neuracore" alt="Neuracore Downloads"></a>
    <a href="https://github.com/NeuracoreAI/neuracore/commits/main"><img src="https://img.shields.io/github/last-commit/NeuracoreAI/neuracore" alt="Last Commit"></a>
    <a href="https://discord.gg/DF5m8V6nbD"><img alt="Neuracore Discord" src="https://img.shields.io/badge/Discord-Join%20Community-blue?logo=discord&logoColor=white"></a>
    <a href="https://www.neuracore.com/try-on-colab"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open Neuracore In Colab"></a>
    <a href="https://opensource.org/licenses/MIT"><img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="License: MIT"></a>
</div>

<div align="center">
  <h1>Neuracore</h1>
</div>

**An open-source framework for Physical and Embodied AI.** Stream, log, train, and deploy robot learning policies directly from Python.

<div align="center">
    <a href="https://www.neuracore.com/try-on-colab"><img src="https://img.shields.io/badge/Google_Colab-Try_Now-F9AB00?style=flat-square&logo=googlecolab&logoColor=white" alt="Open Neuracore In Colab"></a>
    <a href="https://discord.gg/DF5m8V6nbD"><img alt="Neuracore Discord" src="https://img.shields.io/badge/Community-Join_Discord-7289DA?style=flat-square&logo=discord&logoColor=white"></a>
    <a href="https://docs.neuracore.com/"><img alt="Neuracore Docs" src="https://img.shields.io/badge/Documentation-Read_Docs-blue?style=flat-square&logo=readthedocs"></a>
    <a href="https://pypi.org/project/neuracore/"><img alt="PyPI" src="https://img.shields.io/badge/PyPI-neuracore-blue?style=flat-square&logo=pypi&logoColor=white"></a>
</div>

<br>

**have a better image that shows data synchronization**

---

## 🚀 Quick Start

```python
import neuracore as nc

nc.login()
nc.connect_robot(robot_name="MyRobot", urdf_path="/path/to/robot.urdf")
nc.start_recording()
# ...stream sensory data...
policy = nc.policy(train_run_name="MyTrainingJob")
action = policy.predict()
```

## 🧠 What This Does

Neuracore eliminates the need to manually string together ROS bags, local data visualizers, and complex cloud GPU scripts. It provides a cohesive Python library to collect and synchronize high-frequency multi-modal data directly from your robots. Behind the scenes, Neuracore automatically uploads your datasets and scales state-of-the-art imitation learning algorithms on cloud GPUs, letting you seamlessly pull down trained policies for local, low-latency execution.

## ✨ Key Features

- **Collect** - High-frequency streaming data logging with support for fully custom multi-modal data types.
- **Visualize** - Real-time dataset visualization, playback, and precise synchronization via a unified dashboard.
- **Train** - Frictionless deployment of state-of-the-art robot learning algorithms on scalable cloud GPU infrastructure.
- **Deploy** - Seamless policy inference and low-latency execution engines built directly for production environments.

## 📥 Installation

Install the `neuracore` package in a **Python>=3.10** environment.

```bash
# Basic installation for data logging and visualization
pip install neuracore

# For training and ML development
pip install neuracore[ml]

# To run our example scripts
pip install neuracore[examples]
```

> **Note:** Installing the `ffmpeg` binary (`sudo apt-get install -y ffmpeg`) is heavily recommended for faster video encoding during recording.

## 🍰 Full Example

Here is an end-to-end glimpse of what an entire Neuracore pipeline looks like in a single script.

```python
import neuracore as nc # pip install neuracore
import time

# Ensure you have an account at neuracore.com
nc.login()

# Connect to a robot with URDF
nc.connect_robot(
    robot_name="MyRobot", 
    urdf_path="/path/to/robot.urdf",
)

# Create a dataset for recording
nc.create_dataset(
    name="My Robot Dataset",
    description="Example dataset with multiple data types"
)

# Recording and streaming data
nc.start_recording()
t = time.time()
nc.log_joint_positions(positions={'joint1': 0.5, 'joint2': -0.3}, timestamp=t)
nc.log_rgb(name="top_camera", rgb=image_array, timestamp=t)

# Stop recording, the dataset is automatically uploaded to the cloud
nc.stop_recording()

# Kick off cloud training
job_data = nc.start_training_run(
    name="MyTrainingJob",
    dataset_name="My Robot Dataset",
    algorithm_name="diffusion_policy",
    num_gpus=5,
    frequency=50,
)

# Load a trained model locally
policy = nc.policy(
    train_run_name="MyTrainingJob",
)

# Get model inputs
nc.log_joint_positions(positions={'joint1': 0.5, 'joint2': -0.3})
nc.log_rgb(name="top_camera", rgb=image_array)

# Model Inference
predictions = policy.predict(timeout=5)
```

## 💻 Supported Algorithms

Neuracore supports state-of-the-art robot learning algorithms out of the box. You can also **[upload your own custom algorithms](https://docs.neuracore.com/custom-models/)** directly using our flexible plugin interface.

| Algorithm | Cloud Training | Inference Speed (ms) | Status |
| :--- | :---: | :---: | :---: |
| **Behavioral Cloning (CNN-MLP)** | ✅ | 5-10 | Production |
| **Diffusion Policy** | ✅ | 15-30 | Production |
| **Action Chunking Transformer (ACT)** | ✅ | 20-40 | Production |
| **Flow Matching (pi0)** | ✅ | 25-50 | Beta |
| **Bring Your Own (Custom Model)** | ✅ | N/A | [Upload Yours →](https://docs.neuracore.com/custom-models/) |

## 📖 Documentation

For comprehensive references and deep-dives, see our main documentation hub:
- **[Tutorials & Examples](https://docs.neuracore.com/tutorials/)** - Step-by-step guides for teleoperation setups.
- **[Dataset Importer](https://docs.neuracore.com/importer/)** - Format and migrate external data.
- **[Command Line Tools](https://docs.neuracore.com/cli/)** - Full `neuracore` CLI commands.
- **[Data Daemon](https://docs.neuracore.com/daemon/)** - Manage the background stream.

## � Community

We are building Neuracore to help everyone accelerate their robot learning workflows, and we'd love to hear from you! Join our community to get help, share ideas, and stay updated:

- **[Discord](https://discord.gg/DF5m8V6nbD)** - Chat with the community and get support
- **[GitHub Issues](https://github.com/NeuracoreAI/neuracore/issues)** - Report bugs and request features

<br>

<div align="center">
  <a href="https://github.com/NeuracoreAI"><img src="./docs/assets/social/logo-social-github.png" width="2%" alt="Neuracore GitHub"></a>
  <img src="./docs/assets/social/logo-transparent.png" width="2%" alt="space">
  <a href="https://linkedin.com/company/neuracoreai/"><img src="./docs/assets/social/logo-social-linkedin.png" width="2%" alt="Neuracore LinkedIn"></a>
  <img src="./docs/assets/social/logo-transparent.png" width="2%" alt="space">
  <a href="https://x.com/Neuracore_AI"><img src="./docs/assets/social/logo-social-twitter.png" width="2%" alt="Neuracore Twitter"></a>
  <img src="./docs/assets/social/logo-transparent.png" width="2%" alt="space">
  <a href="https://www.youtube.com/@neuracoreai"><img src="./docs/assets/social/logo-social-youtube.png" width="2%" alt="Neuracore YouTube"></a>
  <img src="./docs/assets/social/logo-transparent.png" width="2%" alt="space">
  <a href="https://discord.gg/DF5m8V6nbD"><img src="./docs/assets/social/logo-social-discord.png" width="2%" alt="Neuracore Discord"></a>
</div>

## 📜 License

Neuracore is available under the **[MIT License](https://github.com/NeuracoreAI/neuracore/blob/main/LICENSE)**.

See the [`LICENSE.md`](https://github.com/NeuracoreAI/neuracore/blob/main/LICENSE) file for the complete terms and conditions regarding distribution, modification, and commercial use.
