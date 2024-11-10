## About

This project demonstrates a failure to fine-tune Llama 3.1 with DPO (Direct Preference Optimization) on a custom dataset. It is a slightly modified copy of https://github.com/omarmnfy/Finetune-Llama3-using-Direct-Preference-Optimization/blob/main/Finetune-Llama3-using-DPO.ipynb under the same Apache 2.0 license.

Tested on WSL Ubuntu with RTX 4090 GPU.

## Installation

1. Download or git clone this project.
2. Create venv with "python -m venv .venv-zelreq" then activate it with "source .venv-zelreq/bin/activate".
3. Install *specific* requirements with "pip install -r zel-requirements.txt".

## Reproduce DPO fail on a custom dataset

Custom dataset: https://huggingface.co/datasets/ZSvedic/phi3-arena-short-dpo/viewer/default/train?row=2

4. Open [Zel-Finetune-Llama3-using-DPO.ipynb](Zel-Finetune-Llama3-using-DPO.ipynb) in VSCode (or some other IDE to run .ipynb notebooks), set kernel to before mentioned ".venv-zelreq" venv.
5. Run all cells in the notebook. Llama 3.1 is being quantized, LoRA is applied, and it is fine-tuned on the dataset which should teach model to prefer shorter answers.
6. Notice that:
   - DPO seems to work fine; loss and accuracy both improve very fast after 30 iterations.
   - After a total run of 150 iterations, the fine-tuned model is merged, saved, and tested again.
   - Unfortunately, in the end testing, fine-tuned model doesn't produce shorter answers. In the phi3-arena-short-dpo dataset, 43% of answers are shorter than 54 characters, which is not the case with fine-tuned model.

## Reproduce DPO success on an original dataset

Original dataset: https://huggingface.co/datasets/Intel/orca_dpo_pairs/viewer/default/train

7. Now open [Original-Finetune-Llama3-using-DPO.ipynb](Original-Finetune-Llama3-using-DPO.ipynb) in VSCode, set kernel to before mentioned ".venv-zelreq" venv.
8. Run all cells in the notebook. Llama 3.1 is being quantized, LoRA is applied, and it is fine-tuned on the Orca dataset.
9. After "BrevDPOLlama" is "saved, you can test it with <https://github.com/EleutherAI/lm-evaluation-harness>. On IFEval it scores better than the base model, so the DPO was successful.
