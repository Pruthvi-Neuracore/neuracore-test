<p>
  <a href="https://www.neuracore.com" target="_blank">
    <img width="100%" src="./docs/assets/neuracore_logo.jpg" alt="Neuracore banner"></a>
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

[Neuracore](https://www.neuracore.com/) provides a **unified platform** for the entire lifecycle of Physical and Embodied AI. Built on years of foundational research. Neuracore is **fast**, **accurate**, and **scalable**. Constantly updated for performance and flexibility, our platform excels at high-frequency synchronized data logging, real-time visualization, cloud-native policy training, and low-latency edge deployment.

**Try Neuracore now:** [Sign up for a free account](https://www.neuracore.com/) and start training your robots in minutes. 

Find comprehensive guides in the [Neuracore Docs](https://docs.neuracore.com/), get support via [GitHub Issues](https://github.com/NeuracoreAI/neuracore/issues), and join the conversation on [Discord](https://discord.gg/DF5m8V6nbD).

Request an [Enterprise License](mailto:licensing@neuracore.com) for tailored solutions and commercial deployment.

<a href="https://www.neuracore.com/platform" target="_blank">
  <img width="100%" src="https://github.com/user-attachments/assets/5f6e9f12-185f-4050-9e71-2e5712d49b03" alt="Neuracore Data Synchronization">
</a>



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

## ✨ Key Features

🚀 **Collect**: Streaming data logging with custom data types
📊 **Visualize**: Dataset visualization and synchronization
☁️ **Train**: Train robot learning algorithms on cloud
🤖 **Deploy**: Policy inference and deployment

<br>


## 📄 Documentation

See below for quickstart installation and usage examples. For comprehensive guidance on teleoperation, data logging, training, and deployment, refer to our full [Neuracore Docs](https://docs.neuracore.com/).

<details open>
<summary><b>Install</b></summary>

Install the `neuracore` package including all requirements in a [**Python>=3.10**](https://www.python.org/) environment.

[![PyPI - Version](https://img.shields.io/pypi/v/neuracore?logo=pypi&logoColor=white)](https://pypi.org/project/neuracore/) [![Neuracore Downloads](https://static.pepy.tech/badge/neuracore)](https://pepy.tech/project/neuracore) [![PyPI - Python Version](https://img.shields.io/pypi/pyversions/neuracore?logo=python&logoColor=gold)](https://pypi.org/project/neuracore/)

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

For alternative environments consult the [Neuracore Quickstart Guide](https://docs.neuracore.com/quickstart/).

</details>

<details>
<summary><b>Usage</b></summary>

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

The Neuracore CLI allows you to manage datasets, hardware, and cloud training directly from your terminal. This is the fastest way to verify your system and trigger cloud-based AI jobs.

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

</details>


## 💻 Supported Models

Neuracore supports state-of-the-art robot learning algorithms out of the box, optimized for throughput and stability. You can also **[upload your own custom algorithms](https://docs.neuracore.com/custom-models/)**  Our Platform provides a flexible plugin interface to collect, train, evaluate, and deploy any policy architecture on our cloud infrastructure.

Neuracore natively supports leading foundation models and visuomotor policies for offline and online training. View our [Model Zoo Docs](https://docs.neuracore.com/models/) for full tuning and benchmarking details.

| Algorithm | Architecture | Cloud Training | Inference Speed (ms) | Status |
| :--- | :--- | :---: | :---: | :---: |
| **CNN-MLP** | Behavioural Cloning | ✅ | 5-10 | Production |
| **Diffusion Policy** | Energy-Based Diffusion | ✅ | 15-30 | Production |
| **ACT** | Action Chunking Transformer | ✅ | 20-40 | Production |
| **pi0** | Flow Matching (VLA) | ✅ | 25-50 | Beta |
| **Custom Model** | Bring Your Own | ✅ | — | [Upload Yours →](https://docs.neuracore.com/custom-models/) |

<br>

## 🧩 Integrations

Neuracore integrates seamlessly with leading robotics simulators and machine learning platforms.

<br>

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
```

<br>

## 📜 License

Neuracore is available under two licenses:
- **AGPL-3.0 License**: Open-source for non-commercial use.
- **Enterprise License**: For commercial products and priority support. Contact [licensing@neuracore.com](mailto:licensing@neuracore.com).

<br>

## 📞 Contact

For bug reports and feature requests related to Neuracore software, please visit [GitHub Issues](https://github.com/NeuracoreAI/neuracore/issues). For questions, discussions, and community support, join our active community on [Discord](https://discord.gg/DF5m8V6nbD). We're here to help with all things Neuracore!

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
