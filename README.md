# 2024 IR Final Project
This is a repo for NTU IR Final Project

- Related Laws for Legal Questions:
[Kaggle Page](https://www.kaggle.com/competitions/ntu-csie-2024-ir-final-project/)

- Our experiment was conducted on Ubuntu 24.04.1 LTS with two RTX 4090 GPUs, and Python version 3.11.10.


# Installation & Requirement
- LLaMA-Factory
    - Please refer [here](https://github.com/hiyouga/LLaMA-Factory) to install LLaMA-Factory

```
git clone --depth 1 https://github.com/hiyouga/LLaMA-Factory.git
cd LLaMA-Factory
pip install -e ".[torch,metrics]"
```

- Install some requirements
```
pip install -r requirements.txt
```

## Data Preprocessing
- Please download training/test data from Kaggle Page.
- Please download Taiwan Law from [here.](https://drive.google.com/drive/folders/100dNvI1PqirE5q5WL_vTNQ46OkBFX6EG)

Put all of them under data directory so you should get:
```
    2024_IR_Final/
    ├──data/
    |  ├──train_data.jsonl
    |  ├──test_data.jsonl
    |  ├──law.zip
    |  ├──law (unzip law.zip)
    |  ├──law.json
    ├──LLaMA-Factory/

```
- Using `law_process.ipynb` to generate law.json.
- Using `arrage_train_step1.ipynb` to prepare Training Data for step1.
- Using `arrage_train_step2.ipynb` to prepare Training Data for step2.


# Training and Merge LoRA for stage 1

- Place `law_data_step1.json` and `dataset_info.json` under your `LLaMA-Factory/data`
- Place `train_lora/taiwanllm_lora_sft.yaml` under your `LLaMA-Factory/examples/train_lora`
- Place `merge_lora/taiwanllm_lora_sft.yaml` under your `LLaMA-Factory/examples/merge_lora`

```
cd LLaMA-Factory
llamafactory-cli train examples/train_lora/llama3_lora_sft.yaml
llamafactory-cli export examples/merge_lora/llama3_lora_sft.yaml
```

# Training and Merge LoRA for stage 2

- Place `law_data_step2.json` under your `LLaMA-Factory/data`
- Place `train_lora/taiwanllm_lora_sft_stage2.yaml` under your `LLaMA-Factory/examples/train_lora`
- Place `merge_lora/taiwanllm_lora_sft_stage2.yaml` under your `LLaMA-Factory/examples/merge_lora`

```
cd LLaMA-Factory
llamafactory-cli train examples/train_lora/llama3_lora_sft_stage2.yaml
llamafactory-cli export examples/merge_lora/llama3_lora_sft_stage2.yaml
```

# Inference
- Use `inference_step1.ipynb` to generate step1 result. (public: 0.223)
- Use `inference_step2.ipynb` to generate step2 result. (public: 0.196)