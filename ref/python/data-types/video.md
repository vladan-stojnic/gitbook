# Video



[![](https://www.tensorflow.org/images/GitHub-Mark-32px.png)View source on GitHub](https://www.github.com/wandb/client/tree/v0.10.32/wandb/sdk/data_types.py#L957-L1135)



Wandb representation of video.

```python
Video(
    data_or_path: Union['np.ndarray', str, 'TextIO'],
    caption: Optional[str] = None,
    fps: int = 4,
    format: Optional[str] = None
)
```





| Arguments |  |
| :--- | :--- |
|  `data\_or\_path` |  (numpy array, string, io) Video can be initialized with a path to a file or an io object. The format must be "gif", "mp4", "webm" or "ogg". The format must be specified with the format argument. Video can be initialized with a numpy tensor. The numpy tensor must be either 4 dimensional or 5 dimensional. Channels should be (time, channel, height, width) or (batch, time, channel, height width) |
|  `caption` |  (string) caption associated with the video for display |
|  `fps` |  (int) frames per second for video. Default is 4. |
|  `format` |  (string) format of video, necessary if initializing with path or io object. |



## Methods

<h3 id="encode"><code>encode</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.10.32/wandb/sdk/data_types.py#L1026-L1063)

```python
encode() -> None
```








| Class Variables |  |
| :--- | :--- |
|  EXTS<a id="EXTS"></a> |   |

