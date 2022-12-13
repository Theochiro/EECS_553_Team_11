# EECS 553 Team 11 Final Project
This repository is our reproduction work of the ICML 2022 paper [Plan Your Target and Learn Your Skills: Transferable State-Only Imitation Learning via Decoupled Policy Optimization](https://proceedings.mlr.press/v162/liu22x/liu22x.pdf). Our code is largely based on the code provided by the original authors (check [here](https://github.com/apexrl/DePO) for Mujoco experiments and [here](https://github.com/apexrl/DePO_NGSIM) for NGSIM experiments), while we made quite a few necessary changes to make the code runnable.

## Running Commands for Mujoco Experiments
After cloning our project, please go to the `DePO` folder first: `cd DePO/`.\
The main entry is `run_experiments.py`, with the assigned experiment yaml file in `\exp_specs`: python run_experiment.py -e your_yaml_path
#### Training DePO for hopper:
`python run_experiment.py -e exp_specs/dpo_exps/dpo_hopper_4_weightedmle_qsa_weight.yaml`
#### Training BCO for hopper (Baseline method 1):
`python run_experiment.py -e exp_specs/dpo_exps/bco_hopper_4.yaml`
#### Training GAIfO for hopper (Baseline method 2):
`python run_experiment.py -e exp_specs/dpo_exps/gailfo_hopper_4.yaml`

## Running Commands for Experiments on NGSIM Dataset
After cloning our project, please go to the `DePO_NGSIM` folder first: `cd DePO_NGSIM`.\
Then go to this [address](https://drive.google.com/file/d/1nWunYJonb0PhGluyc1-5B_SSgXaxBKGv/edit) and download the dataset. Place the downloaded folder in `pytorch-PPUU/traffic-data` directory.\
\
Create the observations from the NGSIM trajectories and the simulator to train both the world and agent models:\
`cd pytorch-PPUU/`\
`for t in 0 1 2; do python generate_trajectories.py -map i80 -time_slot $t; done`
\
\
Load data:\
`python dataloader.py`\
\
Then transform the dataset so that it can fit in [ILSwiss framework](https://github.com/Ericonaldo/ILSwiss):\
`cd ../ILSwiss/`\
`python run_experiment.py -e exp_specs/expert_ppuu.yaml`\
`python run_experiment.py -e exp_specs/expert_ppuu_multitype.yaml`

Co-training of DePO on multiple action spaces:\
`python run_experiment.py -e exp_specs/dpo_ppuu_multitype.yaml`

Training Baseline method GAIfO:\
`python run_experiment.py -e exp_specs/gailfo_ppuu.yaml`
