# Deep_repro

Industrial tools used to train and deploy machine learning models are valued for their reliability, flexibility, and ease of use. Drawing from our experience working with large, constantly evolving codebases (particularly in deep learning research projects) we would like to share a simple yet effective setup for making experiments both traceable and reproducible.

This repo is a more intricate example of reproducibility in deep learning, a standard example using Linear Regression is available in the [Linear_regression_reproducibility](https://github.com/J-ally/Deep_repro_LR) repository.

Slides for the presentation are available in the /slides folder.

## Structure of the repo

The important files of the repo are the following :
- `pyproject.toml`, `uv.lock` and `.python-version`: UV configuration files. It is used by uv to create the virtual environment and install the dependencies.
- `dataops/pretraitment.py`: the script to download and preprocess the dataset.
- `train.py`: the main script to run the training of the model, it contains the main function and the training loop.
- `evaluate.py`: the script to evaluate a model, it takes as input the run_id of the mlflow run to evaluate.
- `conf/` folder: the configuration files for the experiment

# Installing everything

Once uv is installed ([uv install doc](https://docs.astral.sh/uv/getting-started/installation/)), to install the required dependencies, you can use the following command:
```bash
uv sync
```

Then you need to download the dataset :
```bash
uv run dataops/pretraitment.py
```

# Running the code
To run the code, you can use the following command:

```bash
uv run train.py
```

## Exercises (TODOs)

The code contains numbered `##TODO n##` markers to complete. Each is linked below with a short description:

- [TODO 1](conf/model/cnn.yaml#L1) - write the CNN model config following `mlp.yaml` and the `SimpleCNN` class.
- [TODO 2](train.py#L136) — complete the `@hydra.main` decorator parameters (config path/name).
- [TODO 3](train.py#L119) — log the best checkpoint as an MLflow artifact.
- [TODO 4](train.py#L125) — log the periodic checkpoint as an MLflow artifact.
- [TODO 5](train.py#L146) — instantiate the data object from the Hydra config.
- [TODO 6](train.py#L167) — log training parameters and model hyperparameters to MLflow.
- [TODO 7](evaluate.py#L21) — complete the `@hydra.main` decorator parameters (config path/name).
- [TODO 8](evaluate.py#L37) — complete the artifact URIs for the config and best checkpoint.
- [TODO 9](evaluate.py#L50) — instantiate the data object from the Hydra config.
- [TODO 10](evaluate.py#L130) — log the confusion matrix as an MLflow artifact.
- [TODO 11](train.py#L155) — uncomment the MLflow tracking URI to compete on the shared dashboard (also in [evaluate.py](evaluate.py#L28)). **This otpion is onlyh available during the in person workshop. If you're using this material by yourself maintain the local tracking**

# Inspecting the results

Once the python is loaded correctly in your shell (if not automatically done, you can activate it with $ source .venv/bin/activate at the root of the repo), you can launch MLflow. To inspect the results, you can use the following command:

```bash
mlflow ui
```

If there is already a process using the port and you can stop it

```bash
lsof -ti :5000 | xargs kill -9
```

# Evaluating a model

To evaluate a model, you can use the following command (obtaining the run_id from the mlflow ui in the artifacts section of the run) :

```bash
uv run evaluate.py run_id=<run_id>
```

## A note on the dataset label description
Each example is assigned to one of the following labels:
- 0 T-shirt/top
- 1 Trouser
- 2 Pullover
- 3 Dress
- 4 Coat
- 5 Sandal
- 6 Shirt
- 7 Sneaker
- 8 Bag
- 9 Ankle boot

# Correction

Correction for exercises is available on the `correction` branch