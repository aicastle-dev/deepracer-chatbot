# Input parameters of the AWS DeepRacer reward function

The AWS DeepRacer reward function takes a dictionary object as the input.

```python
def reward_function(params) :
    
    reward = ...

    return float(reward)
```

The `params` dictionary object contains the following key-value pairs:


| **Parameter**              | **Type**         | **Description**                                                                                                                                      | **Range**                     |
|----------------------------|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------|
| **`all_wheels_on_track`**  | `Boolean`        | Whether all wheels are on the track.                                                                                                                 | `True/False`                  |
| **`x, y`**                 | `float`          | Agent's position in meters along the x and y axes.                                                                                                   | `0:N`                         |
| **`closest_objects`**      | `[int, int]`     | Indices of the two closest objects (behind and ahead).                                                                                               | `[0:N-1, 0:N-1]`              |
| **`closest_waypoints`**    | `[int, int]`     | Indices of the two closest waypoints (behind and ahead).                                                                                             | `[0:Max-1, 0:Max-1]`          |
| **`distance_from_center`** | `float`          | Distance from the track center.                                                                                                                      | `0:track_width/2`             |
| **`is_crashed`**           | `Boolean`        | Whether the agent has crashed.                                                                                                                       | `True/False`                  |
| **`is_left_of_center`**    | `Boolean`        | Whether the agent is left of the track center.                                                                                                       | `True/False`                  |
| **`is_offtrack`**          | `Boolean`        | Whether the agent is off the track.                                                                                                                  | `True/False`                  |
| **`is_reversed`**          | `Boolean`        | Whether the agent is driving in reverse.                                                                                                             | `True/False`                  |
| **`heading`**              | `float`          | Agent's yaw in degrees relative to the x-axis.                                                                                                       | `-180:180`                    |
| **`objects_distance`**     | `[float, ...]`   | Distances of objects relative to the track start.                                                                                                    | `[0:track_length, ...]`       |
| **`objects_heading`**      | `[float, ...]`   | Headings of objects in degrees.                                                                                                                      | `[-180:180, ...]`             |
| **`objects_left_of_center`** | `[Boolean, ...]` | Whether objects are left of the track center.                                                                                                        | `[True/False, ...]`           |
| **`objects_location`**     | `[(float, float), ...]` | Locations of objects as `(x, y)` coordinates.                                                                                                       | `[(x, y), ...]`               |
| **`objects_speed`**        | `[float, ...]`   | Speeds of objects in meters per second.                                                                                                              | `[0:12.0, ...]`               |
| **`progress`**             | `float`          | Percentage of track completed.                                                                                                                       | `0:100`                       |
| **`speed`**                | `float`          | Agent's speed in meters per second.                                                                                                                  | `0:5.0`                       |
| **`steering_angle`**       | `float`          | Steering angle in degrees.                                                                                                                           | `-30:30`                      |
| **`steps`**                | `int`            | Number of steps completed.                                                                                                                           | `0:N`                         |
| **`track_length`**         | `float`          | Total track length in meters.                                                                                                                        | `[0:Lmax]`                    |
| **`track_width`**          | `float`          | Width of the track in meters.                                                                                                                        | `0:D_track`                   |
| **`waypoints`**            | `[(float, float), ...]` | Ordered list of track waypoints as `(x, y)` coordinates.                                                                                            | `[(x, y), ...]`               |

---