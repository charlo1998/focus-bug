# Focus Bug: Learning Environmental Awareness for Efficient Mapless Navigation

Focus Bug is a lightweight and efficient mapless navigation framework designed for tiny robots (nano drones, micro rovers) operating under severe size, weight, and power (SWaP) constraints.

The key idea:
➡️ Learn to process only the critical sensory information
➡️ Feed this minimal set to a classical navigation pipeline
➡️ Achieve robust, real-time navigation even in cluttered and dynamic environments.

Focus Bug matches the high success rate and robustness of classical navigation while reducing computation tine by a factor of 2.6 on average.

This repository contains the implementation of Focus Bug from our IROS 2025 paper:
📄 Focus Bug: Learning Environmental Awareness for Efficient Mapless Navigation


## System requirements:
This project uses the AirLearning RL environment : [link](https://github.com/harvard-edge/airlearning-rl/tree/dcd8a39f77992873f49b6872aa534a64a2bfa23a)
The following instructions were tested on Windows 10, Ubuntu 16.04 WSL (Windows 10)

* Windows 10
* Tensorflow-gpu 1.8 (Tested)
* CUDA/CuDNN 

([Here](https://medium.com/@lmoroney_40129/installing-tensorflow-with-gpu-on-windows-10-3309fec55a00) is a really good step by step instruction to install Tensorflow/CUDA/CuDNN on Windows 10)

P.S: For Ubuntu users, we have tested this on Ubuntu 16.04, 18.04, Ubuntu Mate platforms. The instructions are the same as below with one caveat:-You need two machines. The first machine will render the [Air Learning Environment Generator](https://github.com/harvard-edge/airlearning-ue4/tree/b4f27ea457936609745ddad1191ab8c54f8799ac). This portion is currently tested on Windows 10 machine (We will port it to Ubuntu soon). The second machine will be used to train the reinforcment learning algorithm. This second machine can be Windows 10 or Ubuntu. 

On the other hand, if you have a Windows 10 machine, you can run both rendering and RL training on a single machine. So we are providing instruction to install the RL training on Windows 10 here.

## Installation Instruction

### Step 1: Install Dependencies
Assuming you have installed Python, Pip, Tensorflow/CUDA/CuDNN from correctly from [here](https://medium.com/@lmoroney_40129/installing-tensorflow-with-gpu-on-windows-10-3309fec55a00), get the following packages:

```pip install msgpack-rpc-python airsim keras-rl h5py Pillow gym opencv-python eventlet matplotlib PyDrive pandas```

### Step 2: Install Air Learning RL
Clone the Air Learning Project

```$ git clone --recursive https://github.com/harvard-edge/airlearning.git```

```$ cd airlearning/airlearning-rl```

Lets call the directory where airlearning is cloned as <AIRLEARNING_ROOT>
### Step 3: Setup the machine_dependent_settings.py file

You need to point to the directory where Unreal Project files are installed. Please install them before you follow the instructions below.The instructions for installing Air Learning Environment Generator is [here](https://github.com/harvard-edge/airlearning-ue4/tree/b4f27ea457936609745ddad1191ab8c54f8799ac). 

``` $ cd <AIRLEARNING_ROOT>\airlearning-rl\settings_folder\```

``` $ vim machine_dependent_settings.py```

Here is a sample machine_dependent_settings.py file. Please use this as a template and point to the location where you have installed the airlearning-ue4 project.

```
json_file_addr = "<AIRLEARNING_ROOT>\Content\JsonFiles\EnvGenConfig
game_file = "<AIRLEARNING_ROOT>\airlearning-ue4\AirLearning.uproject"
unreal_host_shared_dir = ""
unreal_exe_path = "C:\\Program Files\\Epic Games\\UE_4.18\\Engine\\Binaries\\Win64\\UE4Editor.exe"
```

### Step 4: Train

Run the training 

``` 
$ cd <AIRLEARNING_ROOT>\airlearning-rl\runtime\
$ python collect_data.py
```

This should start the AirLearning game mode and start the training

# 🚀 Key Features

DRL agent that learns to select only the relevant LiDAR sectors

Hybrid navigation stack integrating:

Tangent Bug (global planner)

Dynamic Window Approach (DWA)

Classical potential fields (for comparison)

Vector-Field Histogram inspired representation to massively reduce observation & action spaces

Simulation in AirSim via AirLearning

Real robot deployment on the Agilex Limo rover using CPU-only compute

Generalizes across embodiments (drone → rover)

87% less LiDAR data used on average

2.6× faster processing

57% fewer collisions than end-to-end RL baselines

# Citation
if you use this code in your research, please citeL
(citation pending, IROS 2025 proceedings to be published).

# License

This project is released under the MIT License.

