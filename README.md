# Run Python (jobtools) Action

Runs Python code using [`jobtools`](https://pypi.org/project/jobtools/) command line, which allows running a generic Python function from an script file or Python package.

## When to use it

Use `jobtools-action` to run a Python function in an script or library using the command line with automatic arguments parsing from it.

## Getting Started

### Inputs

| name                       | Description | Required |
|----------------------------|-------------|----------|
| script               | Path to the script to run or to the module (namespace) you want to execute | Yes |
| function             | Name of the function to execute. | yes |
| args                 | Arguments to pass to the `function` indicated before. Use the pattern `--argument-name` to pass arguments. Argument naming matches the names of the argument in the function. `_` in Python arguments are matched with `-` in the command line. Optional arguments are not required. | No |
| workingFolder        | Path from where the code should be executed. If missing, the current `$PWD` is used. | No | 
| installJobtools      | If `jobtools` utility should be installed. Defaults to `true`. | No |

### Remarks

For details about how `jobtools` works, check [https://pypi.org/project/jobtools/](https://pypi.org/project/jobtools/).

### Example usage

**#1**
> Run the function `compute` from the file `pca.py` with arguments `data_path` as string and `number_components` as integer.

```yml
name: Run Python (jobtools)
uses: pyrunit/jobtools-action@v1.0.0
with:
    script: pca.py
    function: compute
    args: --data-path /data/set.csv --number-components 5
```

**#2**
> Runs the function `run_module` from the file `trainer.py` where the parameters are indicated in a `YAML` file. The function `run_module` has a parameter named `params` of type `SimpleNamespace`.

```yml
name: Run Python (jobtools)
uses: pyrunit/jobtools-action@v1.0.0
with:
    script: trainer.py
    function: train
    args: --params train.params.yml
```

**#3**
> Runs the function `train` from the file `regressor/train/trainer.py` where the parameters are indicated in a `YAML` file. The function `run_module` has a parameter named `params` of type `SimpleNamespace`. `regressor` is the name of a Python package.

```yml
name: Run Python (jobtools)
uses: pyrunit/jobtools-action@v1.0.0
with:
    script: regressor.train.trainer
    function: train
    args: --params train.params.yml
```