# Pixels to Predictions: QLoRA Fine-Tuning of SmolVLM for Multimodal Science Multiple-Choice Reasoning

This repository contains the final clean notebook for the NYU DL Vision Challenge submission by Siva Srinivas Venigalla (`sv2881`).

## Project Summary

The task is multimodal scientific multiple-choice reasoning for the Kaggle competition `Pixels to Predictions`. Each example combines an image, a question, answer choices, optional `hint` and `lecture` text, and metadata such as subject and skill.

The final system uses:

- `HuggingFaceTB/SmolVLM-500M-Instruct`
- QLoRA adaptation with 4-bit NF4 loading
- LoRA rank `8`, alpha `16`, dropout `0.05`
- Deterministic multiple-choice likelihood scoring instead of free-form generation

Final public leaderboard score: `0.86317`

## Repository Layout

```text
pixels-to-predictions-sv2881/
├── README.md
├── requirements.txt
├── notebooks/
│   └── sv2881_pixels_to_predictions_final_clean.ipynb
├── submissions/
├── results/
│   └── ablation_results.csv
└── figures/
```

## Reproducible Rerun Steps

1. Clone this repository.
2. Install dependencies from `requirements.txt`.
3. Download or mount the Kaggle competition data in the expected folder.
4. Download the final LoRA adapter from the model-weights link and place it where the notebook can find it.
5. Open `notebooks/sv2881_pixels_to_predictions_final_clean.ipynb`.
6. Run the environment setup cell.
7. Run the inference cells to regenerate `submission_final_epoch4_086317.csv`.
8. Upload the generated CSV to Kaggle.

## Dataset Expectations

The notebook expects the competition files to include:

- `train.csv`
- `val.csv`
- `test.csv`
- `sample_submission.csv`
- the corresponding image folders

The clean notebook is written for Google Colab and looks for data under paths such as `/content/drive/MyDrive/pixels-to-predictions`.

## Final Configuration

- Base model: `HuggingFaceTB/SmolVLM-500M-Instruct`
- Quantization: `4-bit NF4`
- LoRA rank: `8`
- LoRA alpha: `16`
- LoRA dropout: `0.05`
- Target modules: `q_proj`, `k_proj`, `v_proj`, `o_proj`, `gate_proj`, `up_proj`, `down_proj`
- Trainable parameters: approximately `4.78M`
- Final checkpoint: cautious continuation through epoch `4`
- Inference: likelihood scoring over valid answer choices

## Links

- GitHub repository: https://github.com/sv2881/pixels-to-predictions-sv2881
- Model weights / LoRA adapter: add your adapter link here
