<p>
  <a href="https://www.neuracore.com" target="_blank">
    <img width="100%" src="./docs/assets/Neuracore_banner.png" alt="Neuracore banner"></a>
</p>

<div align="center">
    <a href="https://pypi.org/project/neuracore/"><img src="https://img.shields.io/pypi/v/neuracore?logo=pypi&logoColor=white" alt="PyPI - Version"></a>
    <a href="https://www.python.org/downloads/"><img src="https://img.shields.io/badge/python-3.10+-blue.svg" alt="Python 3.10+"></a>
    <a href="https://pepy.tech/project/neuracore"><img src="https://static.pepy.tech/badge/neuracore" alt="Neuracore Downloads"></a>
    <a href="https://github.com/NeuracoreAI/neuracore/commits/main"><img src="https://img.shields.io/github/last-commit/NeuracoreAI/neuracore" alt="Last Commit"></a>
    <a href="https://discord.gg/DF5m8V6nbD"><img alt="Neuracore Discord" src="https://img.shields.io/badge/Discord-Join%20Community-blue?logo=discord&logoColor=white"></a>
    <a href="https://www.neuracore.com/try-on-colab"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open Neuracore In Colab"></a>
    <a href="https://opensource.org/licenses/MIT"><img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="License: MIT"></a>
</div>
<br>

Neuracore is an open-source framework for Physical and Embodied AI. It allows you to collect high-frequency data, visualize it in real-time, train cloud-native policies, and deploy them to edge devices directly from Python.

**[Join the Discord Community](https://discord.gg/DF5m8V6nbD)** | **[Try Neuracore in Colab](https://www.neuracore.com/try-on-colab)** | **[Read the Docs](https://docs.neuracore.com/)**

**have a better image that shows data synchronization**

## ✨ Key Features

- **Collect** - High-frequency streaming data logging with support for fully custom multi-modal data types.
- **Visualize** - Real-time dataset visualization, playback, and precise synchronization via a unified dashboard.
- **Train** - Frictionless deployment of state-of-the-art robot learning algorithms on scalable cloud GPU infrastructure.
- **Deploy** - Seamless policy inference and low-latency execution engines built directly for production environments.

## � Install

Install the `neuracore` package including all requirements in a **Python>=3.10** environment.

> **Note:** Installing the `ffmpeg` binary is recommended for faster video encoding during recording and decoding during playback/import. If unavailable, Neuracore falls back to PyAV automatically.
>
> **Linux (Debian/Ubuntu):** `sudo apt-get update && sudo apt-get install -y ffmpeg`

```bash
# Basic installation for data logging and visualization
pip install neuracore

# For training and ML development
pip install neuracore[ml]

# For bulk importing datasets 
pip install neuracore[import]

# To run our example scripts
pip install neuracore[examples]
```

## 💻 Usage

### Python

Collect multi-modal data and deploy trained policies in minutes.

```python
import neuracore as nc

# Authenticate and register your robot
nc.login()
nc.connect_robot(robot_name="MyRobot", urdf_path="/path/to/robot.urdf")

# Stream and log high-frequency sensor data
nc.start_recording()
nc.log_joint_positions(positions={'j1': 0.1, 'j2': -0.3})
nc.log_rgb(name="wrist_cam", rgb=image_array)
nc.log_depth(name="wrist_cam", depth=depth_array)
nc.stop_recording()

# Deploy a trained policy for real-time inference
policy = nc.policy(train_run_name="MyTrainingJob")
action = policy.predict()
```

### CLI

Manage datasets, hardware, and cloud training directly from your terminal.

```bash
# 1. Launch the background data pipeline (required for all streaming tasks)
nc-data-daemon launch

# 2. Connect a robot via URDF and create a new dataset
neuracore connect --name "MyRobot" --urdf "/path/to/robot.urdf"
neuracore datasets create --name "My Robot Dataset"

# 3. Start/Stop recording data streams
neuracore record start
neuracore record stop

# 4. Kick off a Diffusion Policy training run on 5 cloud GPUs
neuracore train start --name "MyJob" --dataset "My Robot Dataset" --algo "diffusion_policy" --gpus 5

# 5. Run a trained model on a live camera source
neuracore predict --model "MyJob" --source "top_camera"
```

## 🍰 A Short Taste

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

## 📖 Quick Links

| Type | Links | Description |
| :-- | :-- | :-- |
| **Tutorials** | **[Tutorials](https://docs.neuracore.com/tutorials/)** & **[Examples](https://docs.neuracore.com/examples/)** | Step-by-step guides for teleoperation and end-to-end setups. |
| **How-To Guides** | **[Training](https://docs.neuracore.com/training/)** | How to kick off cloud training runs and evaluate policies. |
| **How-To Guides** | **[Dataset Importer](https://docs.neuracore.com/importer/)** | Formatting custom datasets and migrating from external sources. |
| **Explanation** | **[Data Daemon](https://docs.neuracore.com/daemon/)** | Managing the background data streaming pipeline. |
| **Reference** | **[Command Line Tools](https://docs.neuracore.com/cli/)** | Full command reference for the `neuracore` CLI. |
| **Reference** | **[Environment Variables](https://docs.neuracore.com/env/)** | Securely configuring your Neuracore runtime context. |
| **Explanation** | **[Contribution Guide](https://docs.neuracore.com/contribute/)** | Guidelines to help you contribute back to the open source project. |

## 💻 Supported Models

Neuracore supports state-of-the-art robot learning algorithms out of the box, optimized for throughput and stability. You can also **[upload your own custom algorithms](https://docs.neuracore.com/custom-models/)** directly using our flexible plugin interface.

| Algorithm | Cloud Training | Inference Speed (ms) | Status |
| :--- | :---: | :---: | :---: |
| **Behavioral Cloning (CNN-MLP)** | ✅ | 5-10 | Production |
| **Diffusion Policy** | ✅ | 15-30 | Production |
| **Action Chunking Transformer (ACT)** | ✅ | 20-40 | Production |
| **Flow Matching (pi0)** | ✅ | 25-50 | Beta |
| **Bring Your Own (Custom Model)** | ✅ | N/A | [Upload Yours →](https://docs.neuracore.com/custom-models/) |

## 📑 Citation

If Neuracore accelerates your robotics research or product development, we kindly ask that you cite our framework:

```bibtex
@software{Neuracore,
  author = {Neuracore Team},
  title = {Neuracore},
  month = {January},
  year = {2026},
  url = {https://github.com/NeuracoreAI/neuracore}
}
```

## 📜 License

Neuracore is available under the **[MIT License](https://github.com/NeuracoreAI/neuracore/blob/main/LICENSE)**.

See the [`LICENSE.md`](https://github.com/NeuracoreAI/neuracore/blob/main/LICENSE) file for the complete terms and conditions regarding distribution, modification, and commercial use.

## 📞 Contact

For bug reports and feature requests related to Neuracore software, please visit [GitHub Issues](https://github.com/NeuracoreAI/neuracore/issues). For questions, discussions, and community support, join our active community on [Discord](https://discord.gg/DF5m8V6nbD). We're here to help with all things open-source robotics!
