# Video

[![](https://www.tensorflow.org/images/GitHub-Mark-32px.png)View source on GitHub](https://www.github.com/wandb/client/tree/master/wandb/data_types.py#L1322-L1490)

Wandb representation of video.

```text
Video(
    data_or_path, caption=None, fps=4, format=None
)
```

| Arguments |  |
| :--- | :--- |
|  `data_or_path` |  \(numpy array, string, io\) Video can be initialized with a path to a file or an io object. The format must be "gif", "mp4", "webm" or "ogg". The format must be specified with the format argument. Video can be initialized with a numpy tensor. The numpy tensor must be either 4 dimensional or 5 dimensional. Channels should be \(time, channel, height, width\) or \(batch, time, channel, height width\) |
|  `caption` |  \(string\) caption associated with the video for display |
|  `fps` |  \(int\) frames per second for video. Default is 4. |
|  `format` |  \(string\) format of video, necessary if initializing with path or io object. |

## Methods

### `encode` <a id="encode"></a>

[View source](https://www.github.com/wandb/client/tree/master/wandb/data_types.py#L1383-L1417)

```text
encode()
```

| Class Variables |  |
| :--- | :--- |
|  EXTS |  |
|  artifact\_type |  \`'video-file'\` |

