# File



[![](https://www.tensorflow.org/images/GitHub-Mark-32px.png)View source on GitHub](https://www.github.com/wandb/client/tree/v0.10.33/wandb/apis/public.py#L1662-L1765)



File is a class associated with a file saved by wandb.

```python
File(
    client, attrs
)
```







| Attributes |  |
| :--- | :--- |



## Methods

<h3 id="delete"><code>delete</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.10.33/wandb/apis/public.py#L1745-L1758)

```python
delete()
```




<h3 id="download"><code>download</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.10.33/wandb/apis/public.py#L1722-L1743)

```python
download(
    root=".", replace=(False)
)
```

Downloads a file previously saved by a run from the wandb server.


| Arguments |  |
| :--- | :--- |
|  replace (boolean): If `True`, download will overwrite a local file if it exists. Defaults to `False`. root (str): Local directory to save the file. Defaults to ".". |



| Raises |  |
| :--- | :--- |
|  `ValueError` if file already exists and replace=False |





