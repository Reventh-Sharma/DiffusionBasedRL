# DiTP: Transformer-Based Diffusion Model for Trajectory Planning

## Motivation

Reinforcement Learning has been the go-to learning paradigm for trajectory planning, where the model predicts (state, action) pairs from start to goal state. Recent works, including Diffuser[1], have proposed modeling trajectory planning as a generation problem which can be controlled with classifier guidance. However, existing methods have three major limitations: 

1. The backbone used for training diffusion models is not suitable for sequential prediction tasks
2. Lack of open-source and easy-to-use library for training diffusion models for planning, and,
3. Lack of application in complex planning situations.

We propose DiTP: A transfomer-based path-planning algorithm using diffusion. DiTP has SOTA performance increase as compared to traditional model-free RL algorithm (IQL) and Diffuser (UNet+Diffusion) in complex maze2D environment. Our final report is available [here](Diffusion_based_path_planning.pdf).

## Setup
## Instructions

To get started with the repository, follow these steps:

1. Clone the repository and pull the latest changes:
   ```
        git clone https://github.com/dsrivastavv/DiffusionBasedRL.git
        cd DiffusionBasedRL
        git pull
   ```

3. Pull the Docker image from Docker Hub or build it from the Dockerfile:
   ```
        docker pull revenths/diffuser:latest
   ```
   or alternatively build image using:
   ```
        docker build -t revenths/diffuser:latest .
   ```

4. Run the Docker container with the mounted repository directory:
   ```
        docker run -it -v <path_to_DiffusionBasedRL_on_local>:/root/DiffusionBasedRL --runtime=nvidia revenths/diffuser:latest
   ```

5. Inside the container within directory: DiffusionBasedRL, you can train the Diffuser models using the following commands:
   - To train Diffuser:UNET:
   ```
          nohup python3 -u -m scripts.train --config config.maze2d --dataset <maze2d-large-v1/maze2d-medium-v1/maze2d-umaze-v1> > trainlogs_unet.log &
   ```

   - To train Diffuser:DiT:
   ```
          nohup python3 -u -m scripts.train --config config.maze2d_dit --dataset <maze2d-large-v1/maze2d-medium-v1/maze2d-umaze-v1> > trainlogs_dit.log &
   ```

6. You can download the pretrained model weights from [Model Pretrained Weights](https://drive.google.com/file/d/1teqHRoQ7rU0xKZCDlMy5t-kNj7MSwTQv/view?usp=drive_link).

7. Unzip the zip file

8. For inference, run below commands. This will create a `scorelist.json` file in the DiffusionBasedRL directory.
    ```
           python3 -m scripts.maze2dtable --config config.maze2d --dataset maze2d-umaze-v1 --numepisodes 100
           python3 -m scripts.maze2dtable --config config.maze2d --dataset maze2d-medium-v1 --numepisodes 100
           python3 -m scripts.maze2dtable --config config.maze2d --dataset maze2d-large-v1 --numepisodes 100
           python3 -m scripts.maze2dtable --config config.maze2d_dit --dataset maze2d-umaze-v1 --numepisodes 100
           python3 -m scripts.maze2dtable --config config.maze2d_dit --dataset maze2d-medium-v1 --numepisodes 100
           python3 -m scripts.maze2dtable --config config.maze2d_dit --dataset maze2d-large-v1 --numepisodes 100
    ```


## Citations

* [[1](https://arxiv.org/pdf/2205.09991.pdf)] Planning with Diffusion for Flexible Behavior Synthesis 
* [[2](https://arxiv.org/pdf/2310.07842.pdf)] DiPPeR: Diffusion-based 2D Path Planner applied on Legged Robots 
* [[3](https://openreview.net/forum?id=hclEbdHida)] DiffScene 
* [[4](https://arxiv.org/pdf/1904.01201.pdf)] Habitat: A Platform for Embodied AI Research 
* [[5](https://arxiv.org/abs/2212.09748)] DiT: Scalable Diffusion Models with Transformers, William Peebles and Saining Xie
