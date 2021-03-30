# Databricks

W&B integrates with [Databricks](https://www.databricks.com/) by customizing the W&B Jupyter notebook experience in the Databricks environment.

## Databricks Configuration <a id="databricks-configuration"></a>

### Install wandb in the cluster <a id="install-wandb-in-the-cluster"></a>

Navigate to your cluster configuration, choose your cluster, click on Libraries, then on Install New, Choose PyPI and add the package `wandb`.

### Authentication <a id="authentication"></a>

In order to authenticate your W&B account you can add a databricks secret which your notebooks can query.

```text
# install databricks clipip install databricks-cli​# Generate a token from databricks UIdatabricks configure --token​# Create a scope with one of the two commands (depending if you have security features enabled on databricks):# with security add-ondatabricks secrets create-scope --scope wandb# without security add-ondatabricks secrets create-scope --scope wandb --initial-manage-principal users​# Add your api_key from: https://app.wandb.ai/authorizedatabricks secrets put --scope wandb --key api_key
```

## Examples <a id="examples"></a>

### Simple <a id="simple"></a>

```text
import osimport wandb​api_key = dbutils.secrets.get("wandb", "api_key")wandb.login(key=api_key)​wandb.init()wandb.log({"foo": 1})
```

### Sweeps <a id="sweeps"></a>

Setup required \(temporary\) for notebooks attempting to use wandb.sweep\(\) or wandb.agent\(\):

```text
import os# These will not be necessary in the futureos.environ['WANDB_ENTITY'] = "my-entity"os.environ['WANDB_PROJECT'] = "my-project-that-exists"
```

We cover more details of how to run a sweep in a notebook here:[Sweep from Jupyter Notebook/sweeps/python-api](https://docs.wandb.ai/sweeps/python-api)

