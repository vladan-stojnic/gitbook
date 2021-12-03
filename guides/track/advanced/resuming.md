# Resume Runs

You can have wandb automatically resume runs by passing `resume=True` to `wandb.init()`. If your process doesn't exit successfully, the next time you run it wandb will start logging from the last step.

{% tabs %}
{% tab title="Keras" %}
```python
import keras
import numpy as np
import wandb
from wandb.keras import WandbCallback

wandb.init(project="preemptible", resume=True)

if wandb.run.resumed:
    # restore the best model
    model = keras.models.load_model(wandb.restore("model-best.h5").name)
else:
    a = keras.layers.Input(shape=(32,))
    b = keras.layers.Dense(10)(a)
    model = keras.models.Model(input=a, output=b)

model.compile("adam", loss="mse")
model.fit(np.random.rand(100, 32), np.random.rand(100, 10),
    # set the resumed epoch
    initial_epoch=wandb.run.step, epochs=300,
    # save the best model if it improved each epoch
    callbacks=[WandbCallback(save_model=True, monitor="loss")])
```


{% endtab %}

{% tab title="Pytorch" %}
```python
import wandb
import torch
import torch.nn as nn
import torch.optim as optim

PROJECT_NAME = 'pytorch-resume-run'
CHECKPOINT_PATH = './checkpoint.tar'
N_EPOCHS = 100

# Dummy data
X = torch.randn(64, 8, requires_grad=True)
Y = torch.empty(64, 1).random_(2)
model = nn.Sequential(
    nn.Linear(8, 16), 
    nn.ReLU(), 
    nn.Linear(16, 1), 
    nn.Sigmoid()
)
metric = nn.BCELoss()
optimizer = optim.SGD(model.parameters(), lr=0.01)
epoch = 0
run = wandb.init(project=PROJECT_NAME, resume=True)
if wandb.run.resumed:
    checkpoint = torch.load(wandb.restore(CHECKPOINT_PATH))
    model.load_state_dict(checkpoint['model_state_dict'])
    optimizer.load_state_dict(checkpoint['optimizer_state_dict'])
    epoch = checkpoint['epoch']
    loss = checkpoint['loss']
    
model.train()
while epoch < N_EPOCHS:
    optimizer.zero_grad()
    output = model(X)
    loss = metric(output, Y)
    wandb.log({'loss': loss.item()}, step=epoch)
    loss.backward()
    optimizer.step()
    
     torch.save({ # Save our checkpoint loc
        'epoch': epoch,
        'model_state_dict': model.state_dict(),
        'optimizer_state_dict': optimizer.state_dict(),
        'loss': loss,
        }, CHECKPOINT_PATH)
    wandb.save(CHECKPOINT_PATH) # saves checkpoint to wandb
    epoch += 1
```
{% endtab %}
{% endtabs %}

Automatic resuming only works if the process is restarted on top of the same filesystem as the failed process. If you can't share a filesystem, we allow you to set the WANDB\_RUN\_ID: a globally unique string (per project) corresponding to a single run of your script. It must be no longer than 64 characters. All non-word characters will be converted to dashes.

```python
# store this id to use it later when resuming
id = wandb.util.generate_id()
wandb.init(id=id, resume="allow")
# or via environment variables
os.environ["WANDB_RESUME"] = "allow"
os.environ["WANDB_RUN_ID"] = wandb.util.generate_id()
wandb.init()
```

If you set `WANDB_RESUME` equal to `"allow"`, you can always set `WANDB_RUN_ID` to a unique string and restarts of the process will be handled automatically. If you set `WANDB_RESUME` equal to `"must"`, wandb will throw an error if the run to be resumed does not exist yet instead of auto-creating a new run.

{% hint style="warning" %}
If multiple processes use the same `run_id` concurrently unexpected results will be recorded and rate limiting will occur.
{% endhint %}

{% hint style="info" %}
If you resume a run and you have `notes`** **specified in `wandb.init()`, those notes will overwrite any notes that you have added in the UI.
{% endhint %}

{% hint style="info" %}
Note that resuming a run which was executed as part of a Sweep is not supported.
{% endhint %}

### Preemptible Sweeps

If you are running a sweep agent in a compute environment that is subject to preemption  (e.g., a SLURM job in a preemptible queue, an EC2 spot instance, or a Google Cloud preemptible VM), you can automatically requeue your interrupted sweep runs, ensuring they will be retried until they run to completion.

When you learn your current run is about to be preempted, call&#x20;

```
wandb.mark_preempting()
```

to immediately signal to the W\&B backend that your run believes it is about to be preempted. If a run that is marked preempting exits with status code 0, W\&B will consider the run to have terminated successfully and it will not be requeued. If a preempting run exits with a nonzero status, W\&B will consider the run to have been preempted, and it will automatically append the run to a run queue associated with the sweep. If a run exits with no status, W\&B will mark the run preempted 5 minutes after the run's final heartbeat, then add it to the sweep run queue. Sweep agents will consume runs off the run queue until the queue is exhausted, at which point they will resume generating new runs based on the standard sweep search algorithm.&#x20;

By default, requeued runs begin logging from their initial step. To instruct a run to resume logging at the step where it was interrupted, initialize the resumed run with `wandb.init(resume=True)`.

