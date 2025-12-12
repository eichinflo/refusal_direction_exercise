# Exercise: Refusal in Language Models Is Mediated by a Single Direction

**Content warning**: This repository contains text that is offensive, harmful, or otherwise inappropriate in nature.

This repository contains code that is derived from the code supplements of the paper "Refusal in Language Models Is Mediated by a Single Direction".

- [Paper](https://arxiv.org/abs/2406.11717)
- [Blog post](https://www.lesswrong.com/posts/jGuXSZgv6qfdhMCuJ/refusal-in-llms-is-mediated-by-a-single-direction)

To run the code for this exercise, we advice you to run it in Google Colab which comes with enough free resources for the models we're using. Alternatively, you can also run it on your own hardware.

## Google Colab (recommended)

The exercise is contained in a Jupyter notebook (see: [`exercise.ipynb`](https://github.com/eichinflo/refusal_direction_exercise/blob/main/exercise.ipynb)). We designed this exercise such that you can run it in Google Colab (basically a cloud solution to running Jupyter notebooks) directly. To run it, you will need access to accounts for Google and Huggingface (both free). Then, you can navigate to [this notebook](https://colab.research.google.com/drive/14khwtjUrguBYZx8R2TgUtBsXScXX3YZB?usp=sharing), create a copy, and start working on the exercise.

## Run Jupyter Notebook locally

If you have your own GPU setup, you can simply fork this repo and start working on [`exercise.ipynb`](https://github.com/eichinflo/refusal_direction_exercise/blob/main/exercise.ipynb). You might want to check Manual Setup below in case the notebook fails to set up the correct environment.


## Manual Setup

If you want to run/play with the code by yourself in your own environment, you can use the following to get started:

```bash
git clone https://github.com/andyrdt/refusal_direction.git
cd refusal_direction
source setup.sh
```

The setup script will prompt you for a HuggingFace token (required to access gated models) and a Together AI token (required to access the Together AI API, which is used for evaluating jailbreak safety scores).
It will then set up a virtual environment and install the required packages.

### Reproducing main results from paper

To reproduce the main results from the paper, run the following command:

```bash
python3 -m pipeline.run_pipeline --model_path {model_path}
```
where `{model_path}` is the path to a HuggingFace model. For example, for Llama-3 8B Instruct, the model path would be `meta-llama/Meta-Llama-3-8B-Instruct`.

The pipeline performs the following steps:
1. Extract candiate refusal directions
    - Artifacts will be saved in `pipeline/runs/{model_alias}/generate_directions`
2. Select the most effective refusal direction
    - Artifacts will be saved in `pipeline/runs/{model_alias}/select_direction`
    - The selected refusal direction will be saved as `pipeline/runs/{model_alias}/direction.pt`
3. Generate completions over harmful prompts, and evaluate refusal metrics.
    - Artifacts will be saved in `pipeline/runs/{model_alias}/completions`
4. Generate completions over harmless prompts, and evaluate refusal metrics.
    - Artifacts will be saved in `pipeline/runs/{model_alias}/completions`
5. Evaluate CE loss metrics.
    - Artifacts will be saved in `pipeline/runs/{model_alias}/loss_evals`

For convenience, we have included pipeline artifacts for the smallest model in each model family:
- [`qwen/qwen-1_8b-chat`](/pipeline/runs/qwen-1_8b-chat/)
- [`google/gemma-2b-it`](/pipeline/runs/gemma-2b-it/)
- [`01-ai/yi-6b-chat`](/pipeline/runs/yi-6b-chat/)
- [`meta-llama/llama-2-7b-chat-hf`](/pipeline/runs/llama-2-7b-chat-hf/)
- [`meta-llama/meta-llama-3-8b-instruct`](/pipeline/runs/meta-llama-3-8b-instruct/)


## Citing this work

If you find this work useful in your research, please consider citing their [paper](https://arxiv.org/abs/2406.11717):
```tex
@article{arditi2024refusal,
  title={Refusal in Language Models Is Mediated by a Single Direction},
  author={Andy Arditi and Oscar Obeso and Aaquib Syed and Daniel Paleka and Nina Panickssery and Wes Gurnee and Neel Nanda},
  journal={arXiv preprint arXiv:2406.11717},
  year={2024}
}
```
