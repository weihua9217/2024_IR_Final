# 2024 IR Final Project

Related Laws for Legal Questions:
[Kaggle Page](https://www.kaggle.com/competitions/ntu-csie-2024-ir-final-project/)

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
- Using `arrage_train_step1.ipynb` to prepare Training Data.
- Using `law_process.ipynb` to generate law.json.


# Training and Merge LoRA

- Place `law_data_step1.json` and `dataset_info.json` under your `LLaMA-Factory/data`
- Place `train_lora/taiwanllm_lora_sft.yaml` under your `LLaMA-Factory/examples/train_lora`
- Place `merge_lora/taiwanllm_lora_sft.yaml` under your `LLaMA-Factory/examples/merge_lora`

```
cd LLaMA-Factory
llamafactory-cli train examples/train_lora/llama3_lora_sft.yaml
llamafactory-cli export examples/merge_lora/llama3_lora_sft.yaml
```

# Inference
- Use `inference_step1.ipynb` to generate final result.