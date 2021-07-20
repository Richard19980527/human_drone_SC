# FD-MAPPO (Cubic Map)
Additional materials for paper "Human-Drone Collaborative Spatial Crowdsourcing by Memory-Augmented 
Distributed Multi-Agent Deep Reinforcement Learning" submitted to ICDE 2022.
## :page_facing_up: Description
FD-MAPPO (Cubic Map) is a novel deep reinforcement learning (DRL) framework for human-drone collaborative SC tasks. It consists of a fully decentralized MADRL framework, called FD-MAPPO, as a novel multi-actor-multi-learner architecture without any centralized control module based on PPO. It also contains a novel memory structure, called Cubic Map, to enable novel sparse cubic writing and contextual attentive reading operations.
## :wrench: Dependencies
- Python >= 3.7 (Recommend to use [Anaconda](https://www.anaconda.com/download/#linux) or [Miniconda](https://docs.conda.io/en/latest/miniconda.html))
- [PyTorch == 1.9](https://pytorch.org/)
- NVIDIA GPU (RTX 3090) + [CUDA 11](https://developer.nvidia.com/cuda-downloads)
### Installation
1. Clone repo
    ```bash
    git clone https://github.com/
    cd peo_uav_sc
    ```
2. Install dependent packages
    ```
    pip install -r requirements.txt
    ```
## :zap: Quick Inference

Get the usage information of the project
```bash
cd peo_uav_sc_code
python main.py -h
```
Then the usage information will be shown as following
```
usage: main.py [-h] env_name method_name mode

positional arguments:
  env_name     the name of environment (KAIST or NCSU)
  method_name  the name of method (fd_mappo_cubicmap)
  mode         train or test
 
optional arguments:
  -h, --help   show this help message and exit
```
Test the trained models provided in [peo_uav_sc_log](https://github.com/Richard19980527/peo_uav_sc/peo_uav_sc_log)
```
python main.py KAIST fd_mappo_cubicmap test
python main.py NCSU fd_mappo_cubicmap test
```
## :computer: Training

We provide complete training codes for FD-MAPPO (Cubic Map).<br>
You could adapt it to your own needs.

1. If you don't have NVIDIA RTX 3090, you should comment these two lines in file<br>
<font color=#0099ff>peo_uav_sc/peo_uav_sc_code/util.py</font>
	```
	[24]  torch.backends.cuda.matmul.allow_tf32 = False
	[25]  torch.backends.cudnn.allow_tf32 = False
	```
2. You can modify the config files for environments<br>
<font color=#0099ff>peo_uav_sc/peo_uav_sc_code/environment/KAIST/conf.py</font><br>
<font color=#0099ff>peo_uav_sc/peo_uav_sc_code/environment/NCSU/conf.py</font>.<br>
For example, you can control the number of drones in the environment by modifying this line
	```
	[43]  'uav_num': 6,
	```
3. You can modify the config file for method<br>
<font color=#0099ff>peo_uav_sc/peo_uav_sc_code/method/fd_mappo_cubicmap/conf.py</font>.<br>
For example, you can control the hyperparameters studied in paper by modifying these two lines
	```
	[34]  'M_size': [16, 16, 16],  # Z, X, Y
	[35]  'mtx_size': 3,  # X' (Y')
	```
4. Training
	```
	python main.py KAIST fd_mappo_cubicmap train
	python main.py NCSU fd_mappo_cubicmap train
	```
	The log files will be stored in <font color=#0099ff>peo_uav_sc_log</font>.
## :checkered_flag: Testing
1. Before testing, you should modify the file <font color=#0099ff>peo_uav_sc/peo_uav_sc_code/env_mathod_set.py</font> to ensure the datetime of the version you want to test is right.
	```
	[2]  'KAIST/fd_mappo_cubicmap': '2021-05-27/23-48-01',
	[3]  'NCSU/fd_mappo_cubicmap': '2021-05-20/16-56-41',
	```
2. Testing
	```
	python main.py KAIST fd_mappo_cubicmap test
	python main.py NCSU fd_mappo_cubicmap test
	```
## :scroll: Acknowledgement

This work is supported by the National Natural Science Foundation of China (No. 62022017). 
<br>
Corresponding author: Chi Harold Liu.

## :e-mail: Contact

If you have any question, please email `2656886245@qq.com`.
