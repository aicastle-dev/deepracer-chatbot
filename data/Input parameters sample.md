# input parameters example

[**reference**](https://github.com/ai-castle/deepracer-lecture-public-data/blob/main/section_08/Input_params_samples.ipynb)

아래는 `reward_function` 인자로 들어가는 `params` 딕셔너리에 담겨있는 정보를 추출했을 때 나오는 예시


## [1] Time Trial : 트랙 위에 장애물이 없는 경우
```python
params = {
    'steps': 2,
    'steering_angle': -30.0,
    'speed': 0.784,
    'x': 0.322,
    'y': 2.691,
    'heading': -84.006,
    'distance_from_center': 0.0,
    'is_left_of_center': False,
    'progress': 0.606,
    'all_wheels_on_track': True,
    'is_reversed': False,
    'track_width': 1.067,
    'track_length': 23.118,
    'closest_waypoints': [0, 1],
    'closest_objects': [0, 0],
    'objects_location': [],
    'objects_left_of_center': [],
    'objects_speed': [],
    'objects_heading': [],
    'objects_distance_from_center': [],
    'objects_distance': [],
    'is_crashed': False,
    'is_offtrack': False,
    'waypoints': [(0.308, 2.831), (0.324, 2.68), ... , (0.301, 2.982), (0.308, 2.831)]
}
 ```

> Tip : step2가 2는 에피소드의 첫번째 스탭을 의미.


## [2] Object Avoidance : 트랙 위에 장애물(상자)가 존재하는 경우
```python
params = {
    'steps': 68,
    'steering_angle': -18.591,
    'speed': 0.837,
    'x': 2.453,
    'y': 0.53,
    'heading': -62.121,
    'distance_from_center': 0.795,
    'is_left_of_center': False,
    'progress': 13.47,
    'all_wheels_on_track': False,
    'is_reversed': False,
    'track_width': 1.067,
    'track_length': 23.118,
    'closest_waypoints': [20, 21],
    'closest_objects': [2, 0],
    'objects_location': [[4.581, -0.081], [7.975, 4.329], [4.254, 4.984]],
    'objects_left_of_center': [False, True, False],
    'objects_speed': [0.0, 0.0, 0.0],
    'objects_heading': [0.0, 0.0, 0.0],
    'objects_distance_from_center': [0.266, 0.267, 0.267],
    'objects_distance': [5.78, 11.559, 17.339],
    'is_crashed': False,
    'is_offtrack': True,
    'waypoints': [(0.308, 2.831), (0.324, 2.68), ... , (0.301, 2.982), (0.308, 2.831)]
}
```

> Tip : is_offtrack 가 True이면 네 바퀴가 모두 트랙을 이탈하였음을 의미하며 이 에피소드의 마지막 step임을 의미.


## [3] Head to Head : 트랙 위에 움직이는 장애물(Bot Car)가 존재하는 경우

```python
params = {
    'steps': 32,
    'steering_angle': -15.0,
    'speed': 1.0,
    'x': 0.558,
    'y': 1.352,
    'heading': -88.58,
    'distance_from_center': 0.234,
    'is_left_of_center': False,
    'progress': 6.119,
    'all_wheels_on_track': True,
    'is_reversed': False,
    'track_width': 1.064,
    'track_length': 23.118,
    'closest_waypoints': [9, 10],
    'closest_objects': [1, 0],
    'objects_location': [[2.171, 1.56], [0.042, 2.813]],
    'objects_left_of_center': [True, False],
    'objects_speed': [0.5, 0.5],
    'objects_heading': [0.163, -1.494],
    'objects_distance_from_center': [0.267, 0.267],
    'objects_distance': [2.996, 0.0],
    'is_crashed': False,
    'is_offtrack': False,
    'waypoints': [(0.308, 2.831), (0.324, 2.68), ... , (0.301, 2.982), (0.308, 2.831)]
}
 ```