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

