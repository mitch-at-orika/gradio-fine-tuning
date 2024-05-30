# Gradio Fine-Tuning Dataset Project

This repository is intended to be a collaborative effort to generate a dataset that can be used for fine-tuning a lightweight LLM to support users building out apps using the [Gradio](https://github.com/gradio-app/gradio) library. The dataset will be designed to help users leverage the latest features and methods of Gradio.

## Project Structure

- **data/**
  - **latest-repo/**: Contains data extracted from the latest Gradio repository (gitignored).
  - **latest-docs/**: Contains data extracted from the latest Gradio documentation (gitignored).
  - **existing-queries/**: Contains data from existing user queries (gitignored).
  - **chat/**: Contains data from Discord chat and use calls (gitignored).

- **datasets/**: Contains the final JSONL dataset to be used for fine-tuning. This is tracked in the repository.

- **notebooks/**: Jupyter notebooks that apply different methods to various LLM APIs based on the data sources.

- **evaluation/**: Scripts and notebooks to conduct L1 evaluations on the dataset.

### Managing Datasets

The `datasets` directory contains the current best attempt at the dataset. To update this:

1. Run the `Get_Data.ipynb` notebook to populate the `data/` directories.
2. Run the notebooks you want to populate the `datasets/raw` directory.
3. Use aggregation scripts to compile the data into a single JSONL file.
4. Save the compiled dataset in the `datasets` directory.

## Contribution Guidelines

1. Fork the repository and clone it locally.
2. Create a new branch for your feature or bugfix.
3. Commit your changes and push them to your fork.
4. Create a pull request to merge your changes into the main repository.

## Getting Started

To get started, explore the  directory for Jupyter notebooks that show examples of how to process and generate data from various sources. You can also check the  directory for the current data sources and the  directory for scripts to combine them.

## Plan for finetuning

Planning to use axolotl and do QLORA on llama-3-8B using sharegpt and alpaca conversation prompt input style.

Here is first hack at the config.yml for axolotl.

base_model: meta-llama/Meta-Llama-3-8B
model_type: AutoModelForCausalLM
tokenizer_type: AutoTokenizer

load_in_8bit: false
load_in_4bit: true
strict: false

datasets:
  - path: _synth_data/gradio_QA_data.jsonl
    type: sharegpt
    conversation: alpaca
dataset_prepared_path:
val_set_size: 0
output_dir: ./outputs/qlora-out

adapter: qlora
lora_model_dir:

sequence_len: 4096
sample_packing: true
pad_to_sequence_len: true

lora_r: 32
lora_alpha: 16
lora_dropout: 0.05
lora_target_modules:
lora_target_linear: true
lora_fan_in_fan_out:

wandb_project:
wandb_entity:
wandb_watch:
wandb_name:
wandb_log_model:

gradient_accumulation_steps: 4
micro_batch_size: 2
num_epochs: 4
optimizer: paged_adamw_32bit
lr_scheduler: cosine
learning_rate: 0.0002

train_on_inputs: false
group_by_length: false
bf16: auto
fp16:
tf32: false

gradient_checkpointing: true
early_stopping_patience:
resume_from_checkpoint:
local_rank:
logging_steps: 1
xformers_attention:
flash_attention: true

warmup_steps: 10
evals_per_epoch: 4
eval_table_size:
saves_per_epoch: 1
debug:
deepspeed:
weight_decay: 0.0
fsdp:
fsdp_config:
special_tokens:
  pad_token: "<|end_of_text|>"