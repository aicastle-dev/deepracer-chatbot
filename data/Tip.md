# 보상함수 작성시 Tip

1. 모델은 훈련할 때 여러번의 에피소드를 시행합니다. 각 에피소드마다 출발지점이 다르며, 트랙을 일정 간격으로 (예를 들면 5%씩) 이동하면서 에피소드의 시작점을 바꿉니다. 

2. 에피소드가 종료되는 기준은 네 바퀴가 모두 이탈했거나 물체와 충돌했을 때 입니다. 또는 한바퀴를 돌아 출발지점까지 오면 (즉, 100% 완주) 종료합니다.

3. 각 에피소드의 params의 `steps`는 2부터 시작합니다. (이유는 잘 모르겠음) 즉, 보상함수에서 첫 보상을 주는 시작점을 캐치하려면 `if params['steps'] == 2:`와 같이 써야합니다.

4. 각 `steps`는 이론상 15분의 1초를 의미 (15 fps) 하지만 이론적인 값이며, 실제로는 약간의 오차가 존재합니다.

5. 각 에피소드에서 첫 `progress`값은 (즉, `steps`는 2 일 때) 0보다 조금 큰 값입니다. 시작점보다 약간 앞에서 출발하는건지 그 이유는 정확히 모르겠습니다. 참고로 `progress`의 최댓값은 100입니다. 첫 시작값은 약 0.5 ~ 1 사이에 존재합니다.

6. params의 `waypoints`의 첫값과 끝 값은 같습니다. 따라서 `waypoints`에는 트랙에 실제로 존재하는 waypoints 개수보다 하나 더 많이 담겨있습니다. 이것은 순환트랙임을 의미하며, 사실 대부분의 딥레이서에서 제공되는 시뮬레이션 트랙은 순환트랙입니다. `real_waypoints_len = len(waypoints) -1` 이런식으로도 작성 가능합니다.

7. params의 `is_crashed` 또는 `is_offtrack` 중 어느 하나가 `True`가 나오면 해당 에피소드는 마지막 step임을 의미합니다.

8. 좌측 및 우측 라인 좌표와 좌측 차선 및 우측 차선의 중앙 라인 좌표 추출하는 예시

```python
waypoints = params['waypionts']
track_width = params['track_width']
half_width = track_width / 2

# Lists to store left and right waypoints
left_waypoints = []
right_waypoints = []
left_center_waypoints = []
right_center_waypoints = []

for i in range(len(waypoints)):
    center_point = waypoints[i]
    next_point = waypoints[(i+1)%len(waypoints)]
    prev_point = waypoints[(i-1)%len(waypoints)]
    dx = next_point[0] - prev_point[0]
    dy = next_point[1] - prev_point[1]

    # Normalize direction vector
    length = (dx**2 + dy**2) ** 0.5
    dx /= length
    dy /= length

    # Rotate 90 degrees to calculate left and right vectors
    left_dx = -dy * half_width
    left_dy = dx * half_width
    right_dx = dy * half_width
    right_dy = -dx * half_width

    # Calculate left and right waypoints
    left_x = center_point[0] + left_dx
    left_y = center_point[1] + left_dy
    right_x = center_point[0] + right_dx
    right_y = center_point[1] + right_dy
    left_center_x = (center_point[0] + left_x) / 2
    left_center_y = (center_point[1] + left_y) / 2
    right_center_x = (center_point[0] + right_x) / 2
    right_center_y = (center_point[1] + right_y) / 2

    left_waypoints.append((left_x, left_y))
    right_waypoints.append((right_x, right_y))
    left_center_waypoints.append((left_center_x, left_center_y))
    right_center_waypoints.append((right_center_x, right_center_y))
```