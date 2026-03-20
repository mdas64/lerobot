# SmolVLA LIBERO Fine-tuning Ablation Study

<!-- ## Overview -->
<!-- Brief description of what you're doing, the task, and the research question -->


## Setup
This experiment is built on top of [LeRobot](link-to-original-repo). The notebook (```training-smolvla.ipynb```) has the installation tools and templates for installing the frameworks, fine-tuning the policy, computing success rates, generating reward curves, and generating videos for results. Scripts for dataset analysis, training, and evalution are provided as specific cells in the Jupyter Notebook.

### Requirements
<!-- Hardware, Colab tier, GPU, VRAM -->
These experiments use an A100 GPU from the Google Colab Pro plan.

### Installation
<!-- Point to parent repo's install steps or list specific ones -->
Execute each cell in the notebook for installation. The user should setup Hugging Face and Weights and Biases accounts on their own to interface with the notebook.

## Repository Structure

```
lerobot/lerobot/
├── README.md
├── training-smolvla.ipynb
```
<!-- └── results/
    ├── loss_curves/
    └── videos/ -->


## Reproducing Experiments

### Base Training Command
<!-- Paste your full base training command here -->
The specific training command is:

```
# No LoRA
!cd lerobot && MUJOCO_GL=egl PYOPENGL_PLATFORM=egl MPLBACKEND=agg python src/lerobot/scripts/lerobot_train.py \
  --policy.path=lerobot/smolvla_base \
  --dataset.repo_id=HuggingFaceVLA/libero \
  --env.type=libero \
  --env.task=libero_object \
  --batch_size=4 \
  --steps=20000 \
  --eval_freq=0 \
  --log_freq=100 \
  --save_freq=4000 \
  --seed=1000 \
  --wandb.enable=true \
  --wandb.project=smolvla-libero \
  --output_dir=outputs/train/ablation_no_lora_2 \
  --job_name=ablation_no_lora_2 \
  --policy.device=cuda \
  --policy.push_to_hub=false \
  --rename_map='{"observation.images.image": "observation.images.camera1", "observation.images.image2": "observation.images.camera2"}' \
  2>&1 | tee /content/training_log_no_lora.txt
```

### Experiment Configurations

You can duplicate the exact experiments using the params as follows:

| Run | LoRA | LoRA Rank | Batch Size | Steps | Hugging Face Link |
|-----|------|-----------|------------|-------|-----------------|
| smolvla_long | No | | 4| 10000| |
| ablation_lora_4 | Yes | 16 | 16 | 10000| |
| ablation_no_lora_2 | No | | 4 | 20000| https://huggingface.co/milpdio/ablation_no_lora_2|
| ablation_no_lora_3 | No | | 4 | 40000 | https://huggingface.co/milpdio/ablation_no_lora_3 |
| ablation_lora_5 | Yes | 16 | 4 | 20000| https://huggingface.co/milpdio/ablation_lora_5 |


<!-- ## Results -->



<!-- ### Training Loss -->
<!-- Include or link to loss curve plots -->


<!-- ### Success Rates

| Run | LoRA | Batch Size | Steps | Train Loss | Success Rate |
|-----|------|------------|-------|------------|-------------|
| smolvla_long | | | | | |
| ablation_lora_4 | | | | | |
| ablation_no_lora_2 | | | | | |
| ablation_lora_5 | | | | | |

--> 

<!-- ### Videos -->
<!-- Link to generated result videos if applicable -->


<!-- ## Analysis -->
<!-- Key findings from your ablation study -->


<!-- ## Notes -->
<!-- Any known issues, caveats, or things the reader should know -->


