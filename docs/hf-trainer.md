# 🤗 Integration with HF Trainer

The [`src/ezpz/hf_trainer.py`](/src/ezpz/hf_trainer.py) module provides a
mechanism for distributed training with 🤗 [huggingface /
transformers](https://github.com/huggingface/transformers).

In particular, it allows for distributed training using the
[`transformers.Trainer`](https://huggingface.co/docs/transformers/main/en/main_classes/trainer#transformers.Trainer)
object with **_any_** (compatible) combination of
{[`models`](https://huggingface.co/models),
[`datasets`](https://huggingface.co/datasets)}.

## Usage

1. Setup environment (on ANY {Intel, NVIDIA, AMD} accelerator)

    ```bash
    source <(curl 'https://raw.githubusercontent.com/saforem2/ezpz/refs/heads/main/src/ezpz/bin/utils.sh')
    ezpz_setup_env
    ```

2. Install 🍋 `ezpz` (from GitHub):

    ```bash
    python3 -m pip install -e "git+https://github.com/saforem2/ezpz" --require-virtualenv
    ```

3. Launch training:

    ```bash
    launch python3 -m ezpz.hf_trainer \
      --dataset_name stanfordnlp/imdb \                 # Example dataset
      --model_name_or_path meta-llama/Llama-3.2-1B \    # Example model
      --bf16 \                                          # TrainingArguments
      --do_train \
      --block_size=8 \
      --gradient_checkpointing \
      --per_device_train_batch_size=1 \
      --deepspeed=ds_configs/zero_stage1_config.json \
      --output_dir=trainer_output-$(date "+%Y-%m-%d-%H%M%S")
    ```
