# input parameters sample

[**reference**](https://github.com/ai-castle/deepracer-lecture-public-data/blob/main/section_08/Track_Waypoints_Visualization.ipynb)

- Track Information : https://github.com/aws-deepracer-community/deepracer-race-data/tree/main/raw_data/tracks

- Colab 에서 실행 가능

- 도구 정의

```python
!git clone https://github.com/aws-deepracer-community/deepracer-race-data.git

import os
import numpy as np
import matplotlib.pyplot as plt

def track_show(npy_name, index_interval = 5, index_fontsize=10):
    npy_folder_path = "deepracer-race-data/raw_data/tracks/npy"
    numpy_file_path = os.path.join(npy_folder_path, npy_name)
    track_arr = np.load(numpy_file_path)

    # Get track waypoints
    track_C = track_arr[:,[0,1]]  # Center coordinate of the track
    track_L = track_arr[:,[2,3]]  # Left coordinate of the track
    track_R = track_arr[:,[4,5]]  # Right coordinate of the track

    # Visualization
    w = track_C[:,0].max() - track_C[:,0].min()
    h = track_C[:,1].max() - track_C[:,1].min()
    plt.figure(figsize = (10, 10 * (h/w)))
    plt.scatter(track_C[:,0],track_C[:,1], s = 15)
    plt.plot(track_L[:,0],track_L[:,1], c='gray')
    plt.plot(track_R[:,0],track_R[:,1], c='gray')

    # Show indices
    for i, (x, y) in enumerate(track_C) :
        if i % index_interval == 0 :
            plt.text(x+0.1, y, i, fontsize=index_fontsize)

    # Output
    plt.title(npy_name)
    plt.show()
```

- Visualization Example

```python
track_show(
    npy_name = "reInvent2019_track.npy",   # Name of the numpy file containing the track waypoints
    index_interval = 5,     # Interval between the indices of the waypoints
    index_fontsize = 10,    # Font size of the waypoint indices
)
```