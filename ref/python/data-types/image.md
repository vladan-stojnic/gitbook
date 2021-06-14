# Image



[![](https://www.tensorflow.org/images/GitHub-Mark-32px.png)View source on GitHub](https://www.github.com/wandb/client/tree/v0.10.32/wandb/sdk/data_types.py#L1672-L2140)



Wandb class for images.

```python
Image(
    data_or_path: "ImageDataOrPathType",
    mode: Optional[str] = None,
    caption: Optional[str] = None,
    grouping: Optional[str] = None,
    classes: Optional[Union['Classes', Sequence[dict]]] = None,
    boxes: Optional[Union[Dict[str, 'BoundingBoxes2D'], Dict[str, dict]]] = None,
    masks: Optional[Union[Dict[str, 'ImageMask'], Dict[str, dict]]] = None
) -> None
```





| Arguments |  |
| :--- | :--- |
|  `data_or_path` |  (numpy array, string, io) Accepts numpy array of image data, or a PIL image. The class attempts to infer the data format and converts it. |
|  `mode` |  (string) The PIL mode for an image. Most common are "L", "RGB", "RGBA". Full explanation at https://pillow.readthedocs.io/en/4.2.x/handbook/concepts.html#concept-modes. |
|  `caption` |  (string) Label for display of image. |



## Methods

<h3 id="all_boxes"><code>all_boxes</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.10.32/wandb/sdk/data_types.py#L2089-L2110)

```python
@classmethod
all_boxes(
    images: Sequence['Image'],
    run: "LocalRun",
    run_key: str,
    step: Union[int, str]
) -> Union[List[Optional[dict]], bool]
```




<h3 id="all_captions"><code>all_captions</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.10.32/wandb/sdk/data_types.py#L2112-L2116)

```python
@classmethod
all_captions(
    images: Sequence['Media']
) -> Union[bool, Sequence[Optional[str]]]
```




<h3 id="all_masks"><code>all_masks</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.10.32/wandb/sdk/data_types.py#L2066-L2087)

```python
@classmethod
all_masks(
    images: Sequence['Image'],
    run: "LocalRun",
    run_key: str,
    step: Union[int, str]
) -> Union[List[Optional[dict]], bool]
```




<h3 id="guess_mode"><code>guess_mode</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.10.32/wandb/sdk/data_types.py#L1960-L1974)

```python
guess_mode(
    data: "np.ndarray"
) -> str
```

Guess what type of image the np.array is representing


<h3 id="to_uint8"><code>to_uint8</code></h3>

[View source](https://www.github.com/wandb/client/tree/v0.10.32/wandb/sdk/data_types.py#L1976-L1998)

```python
@classmethod
to_uint8(
    data: "np.ndarray"
) -> "np.ndarray"
```

Converts floating point image on the range [0,1] and integer images
on the range [0,255] to uint8, clipping if necessary.





| Class Variables |  |
| :--- | :--- |
|  `MAX_DIMENSION`<a id="MAX_DIMENSION"></a> |  `65500` |
|  `MAX_ITEMS`<a id="MAX_ITEMS"></a> |  `108` |

