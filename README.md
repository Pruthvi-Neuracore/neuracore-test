<div align="center">
  <p>
    <a href="https://www.neuracore.com" target="_blank">
      <img width="100%" src="./docs/assets/neuracore_logo.jpg" alt="Neuracore banner"></a>
  </p>



<div>
    <a href="https://pepy.tech/project/neuracore"><img src="https://static.pepy.tech/badge/neuracore" alt="Neuracore Downloads"></a>
    <a href="https://discord.gg/DF5m8V6nbD"><img alt="Neuracore Discord" src="https://img.shields.io/discord/1462855035695267861?logo=discord&logoColor=white&label=Discord&color=blue"></a>
    <a href="https://www.linkedin.com/company/neuracore/"><img alt="Neuracore LinkedIn" src="https://img.shields.io/badge/LinkedIn-Blue?style=flat&logo=linkedin&logoColor=white&label=LinkedIn&color=blue"></a>
    <a href="https://www.neuracore.com/try-on-colab"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open Neuracore In Colab"></a>
</div>
</div>
<br>

<div align="center">

</br> 


</div>

## 🤖 What is Neuracore?

[Neuracore](https://www.neuracore.com/) provides an all-in-one, high-performance **Robot Learning Platform** for the entire lifecycle of embodied AI. Built on high-frequency streaming infrastructure, Neuracore is **fast**, **accurate**, and **scalable**. It serves as a single, unified environment to **collect** multi-modal data, **train** state-of-the-art (SOTA) policies on the cloud, and **deploy** intelligent robot solutions to the edge with ultra-low latency.

Find detailed documentation in the [Neuracore Docs](https://docs.neuracore.com/). Get support via [GitHub Issues](https://github.com/NeuracoreAI/neuracore/issues). Join discussions on [Discord](https://discord.gg/DF5m8V6nbD) and the [Neuracore Community Forums](https://community.neuracore.com/)!

Request an [Enterprise License](mailto:licensing@neuracore.com) for commercial use at Neuracore Licensing.

<a href="https://www.neuracore.com/platform" target="_blank">
  <img width="100%" src="https://github.com/user-attachments/assets/5f6e9f12-185f-4050-9e71-2e5712d49b03" alt="Neuracore Data Synchronization">
</a>

## 🌟 Key Features

- 🚀 **Collect**: Stream high-frequency joints, RGB-D, and multi-modal sensor data with the background **Data Daemon**.
- 📊 **Visualize**: Synchronize and monitor complex robotic datasets in real-time through a unified dashboard.
- ☁️ **Train**: Launch state-of-the-art policy training (**Diffusion Policy**, **ACT**) on scalable cloud infrastructure.
- 🤖 **Deploy**: Execute low-latency robot control with optimized inference engines for production environments.


## 📚 Documentation

See below for quickstart installation and usage examples. For comprehensive guidance on training, validation, prediction, and deployment, refer to our full [Neuracore Docs](https://docs.neuracore.com/).

<details open>
<summary>Install</summary>

Install the `neuracore` package in a [**Python>=3.10**](https://www.python.org/) environment.

```bash
# Basic installation for data logging
pip install neuracore

# Installation for ML and policy training
pip install neuracore[ml]

# Installation for bulk dataset imports (LeRobot, TFDS, etc.)
pip install neuracore[import]
```

Consult the [Quickstart Guide](https://docs.neuracore.com/quickstart/) for specialized environments (Conda, Docker).

</details>

<details open>
<summary>Usage</summary>

### 🐍 Python API

Stream high-frequency data and deploy policies in minutes.

```python
import neuracore as nc

# Login and setup robot
nc.login()
nc.connect_robot(robot_name="MyRobot", urdf_path="/path/to/robot.urdf")

# High-frequency data logging
nc.start_recording()
nc.log_joint_positions(positions={'j1': 0.1})
nc.log_rgb(name="camera", rgb=image_array)
nc.stop_recording()

# Deploy policy for real-time inference
policy = nc.policy(train_run_name="MyJob")
action = policy.predict()
```

### 💻 CLI

Control the background **Data Daemon** and monitor training runs.

```bash
# Start background worker
nc-data-daemon start

# List active cloud training jobs
neuracore training list --cloud
```

</details>

<details>
<summary>Get Support</summary>

- **Documentation**: [docs.neuracore.com](https://docs.neuracore.com/)
- **Tutorials**: [Get Started with Neuracore](./docs/tutorial.md)
- **Discord**: [Join the Community](https://discord.gg/DF5m8V6nbD)
- **Issues**: [GitHub Bug Reports](https://github.com/NeuracoreAI/neuracore/issues)

</details>


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

<div align="center">
  <a href="https://github.com/NeuracoreAI"><img src="https://github.com/ultralytics/assets/raw/main/social/logo-social-github.png" width="3%" alt="Neuracore GitHub"></a>
  <img src="https://github.com/ultralytics/assets/raw/main/social/logo-transparent.png" width="3%" alt="space">
  <a href="https://www.linkedin.com/company/neuracore/"><img src="https://github.com/ultralytics/assets/raw/main/social/logo-social-linkedin.png" width="3%" alt="Neuracore LinkedIn"></a>
  <img src="https://github.com/ultralytics/assets/raw/main/social/logo-transparent.png" width="3%" alt="space">
  <a href="https://twitter.com/neuracore"><img src="https://github.com/ultralytics/assets/raw/main/social/logo-social-twitter.png" width="3%" alt="Neuracore Twitter"></a>
  <img src="https://github.com/ultralytics/assets/raw/main/social/logo-transparent.png" width="3%" alt="space">
  <a href="https://www.youtube.com/@neuracore"><img src="https://github.com/ultralytics/assets/raw/main/social/logo-social-youtube.png" width="3%" alt="Neuracore YouTube"></a>
  <img src="https://github.com/ultralytics/assets/raw/main/social/logo-transparent.png" width="3%" alt="space">
  <a href="https://discord.gg/DF5m8V6nbD"><img src="https://github.com/ultralytics/assets/raw/main/social/logo-social-discord.png" width="3%" alt="Neuracore Discord"></a>
</div>
