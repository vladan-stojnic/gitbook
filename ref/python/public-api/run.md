# Run



[![](https://www.tensorflow.org/images/GitHub-Mark-32px.png)View source on GitHub](https://www.github.com/wandb/client/tree/v0.12.6/wandb/apis/public.py#L1371-L1970)



A single run associated with an entity and project.

```python
Run(
    client, entity, project, run_id, attrs={}
)
```







| Attributes |  |
| :--- | :--- |



## Methods

<h3 id="create"><code>create</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.12.6/wandb/apis/public.py#L1457-L1497)

```python
@classmethod
create(
    api, run_id=None, project=None, entity=None
)
```

Create a run for the given project


<h3 id="delete"><code>delete</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.12.6/wandb/apis/public.py#L1612-L1646)

```python
delete(
    delete_artifacts=(False)
)
```

Deletes the given run from the wandb backend.


<h3 id="display"><code>display</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.12.6/wandb/apis/public.py#L736-L747)

```python
display(
    height=420, hidden=(False)
) -> bool
```

Display this object in jupyter


<h3 id="file"><code>file</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.12.6/wandb/apis/public.py#L1708-L1717)

```python
file(
    name
)
```

Arguments:
    name (str): name of requested file.

| Returns |  |
| :--- | :--- |
|  A `File` matching the name argument. |



<h3 id="files"><code>files</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.12.6/wandb/apis/public.py#L1696-L1706)

```python
files(
    names=[], per_page=50
)
```

Arguments:
    names (list): names of the requested files, if empty returns all files
    per_page (int): number of results per page

| Returns |  |
| :--- | :--- |
|  A `Files` object, which is an iterator over `File` obejcts. |



<h3 id="history"><code>history</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.12.6/wandb/apis/public.py#L1742-L1781)

```python
history(
    samples=500, keys=None, x_axis="_step", pandas=(True), stream="default"
)
```

Returns sampled history metrics for a run.  This is simpler and faster if you are ok with
the history records being sampled.

| Arguments |  |
| :--- | :--- |
|  samples (int, optional): The number of samples to return pandas (bool, optional): Return a pandas dataframe keys (list, optional): Only return metrics for specific keys x_axis (str, optional): Use this metric as the xAxis defaults to _step stream (str, optional): "default" for metrics, "system" for machine metrics |



| Returns |  |
| :--- | :--- |
|  If pandas=True returns a `pandas.DataFrame` of history metrics. If pandas=False returns a list of dicts of history metrics. |



<h3 id="load"><code>load</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.12.6/wandb/apis/public.py#L1499-L1557)

```python
load(
    force=(False)
)
```




<h3 id="log_artifact"><code>log_artifact</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.12.6/wandb/apis/public.py#L1879-L1911)

```python
log_artifact(
    artifact, aliases=None
)
```

Declare an artifact as output of a run.


| Arguments |  |
| :--- | :--- |
|  artifact (`Artifact`): An artifact returned from `wandb.Api().artifact(name)` aliases (list, optional): Aliases to apply to this artifact |



| Returns |  |
| :--- | :--- |
|  A `Artifact` object. |



<h3 id="logged_artifacts"><code>logged_artifacts</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.12.6/wandb/apis/public.py#L1839-L1841)

```python
logged_artifacts(
    per_page=100
)
```




<h3 id="save"><code>save</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.12.6/wandb/apis/public.py#L1648-L1649)

```python
save()
```




<h3 id="scan_history"><code>scan_history</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.12.6/wandb/apis/public.py#L1783-L1837)

```python
scan_history(
    keys=None, page_size=1000, min_step=None, max_step=None
)
```

Returns an iterable collection of all history records for a run.


#### Example:

Export all the loss values for an example run

```python
run = api.run("l2k2/examples-numpy-boston/i0wt6xua")
history = run.scan_history(keys=["Loss"])
losses = [row["Loss"] for row in history]
```




| Arguments |  |
| :--- | :--- |
|  keys ([str], optional): only fetch these keys, and only fetch rows that have all of keys defined. page_size (int, optional): size of pages to fetch from the api |



| Returns |  |
| :--- | :--- |
|  An iterable collection over history records (dict). |



<h3 id="snake_to_camel"><code>snake_to_camel</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.12.6/wandb/apis/public.py#L732-L734)

```python
snake_to_camel(
    string
)
```




<h3 id="to_html"><code>to_html</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.12.6/wandb/apis/public.py#L1956-L1964)

```python
to_html(
    height=420, hidden=(False)
)
```

Generate HTML containing an iframe displaying this run


<h3 id="update"><code>update</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.12.6/wandb/apis/public.py#L1582-L1610)

```python
update()
```

Persists changes to the run object to the wandb backend.


<h3 id="upload_file"><code>upload_file</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.12.6/wandb/apis/public.py#L1719-L1740)

```python
upload_file(
    path, root="."
)
```

Arguments:
    path (str): name of file to upload.
    root (str): the root path to save the file relative to.  i.e.
        If you want to have the file saved in the run as "my_dir/file.txt"
        and you're currently in "my_dir" you would set root to "../"

| Returns |  |
| :--- | :--- |
|  A `File` matching the name argument. |



<h3 id="use_artifact"><code>use_artifact</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.12.6/wandb/apis/public.py#L1847-L1877)

```python
use_artifact(
    artifact, use_as=None
)
```

Declare an artifact as an input to a run.


| Arguments |  |
| :--- | :--- |
|  artifact (`Artifact`): An artifact returned from `wandb.Api().artifact(name)` use_as (string, optional): A string identifying how the artifact is used in the script. Used to easily differentiate artifacts used in a run, when using the beta wandb launch feature's artifact swapping functionality. |



| Returns |  |
| :--- | :--- |
|  A `Artifact` object. |



<h3 id="used_artifacts"><code>used_artifacts</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.12.6/wandb/apis/public.py#L1843-L1845)

```python
used_artifacts(
    per_page=100
)
```




<h3 id="wait_until_finished"><code>wait_until_finished</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.12.6/wandb/apis/public.py#L1559-L1580)

```python
wait_until_finished()
```






