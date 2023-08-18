## How to launch

1. 모라이 시뮬 키기
2. roslaunch rosbridge_server rosbridge_websocket
3. roslaunch pointcloud2 + tab
4. roslaunch wego tf2 + tab
5. roslaunch wego gmap + tab
6. rosrun map_server map_saver
7. roslaunch wego navi + tab


# Demonstration Video

[Mapping](https://drive.google.com/file/d/1l-ZT98mDnqRU7xDT34kRlDjsKk6TW3Nr/view?usp=drive_link)
---
[Navigating](https://drive.google.com/file/d/1txlhUMaUrxzmGoWG7h5oqlxCImq2Mic9/view?usp=drive_link)
---


# GPS Path Maker and Planing

[Map Maker](https://drive.google.com/file/d/1-PPzuspkoQL8jNinol6OvLZa_LZsD2mp/view?usp=drive_link)
---

# 맵이 완료되었으면 map_saver 끄고 Ws 확인하면 Map.yaml, Map.ppm 있음

[Map_Planner](https://drive.google.com/file/d/1kgRYsdh2dWlNnzoh8QPpCpUZ4P43G_nB/view?usp=drive_link)
---


## 설명
1. tf2_setting -> 로봇의 현재위치(Odometry)를 구하기 위한 odom.py를 실행
2. Pointcloud2toLaserscan - Morai이 에서 쓰이는 Lidar는 3D Lidar이기에, Mapping 및 Navigating에 사용하기위해서 3D의 데이터를 2D로 변환해준다.
    - parameter (sample_node.launch)
        1. min_height = -0.1(m) 최소 변환 높이
        2. max_height = 1.0(m) 최대 변환 높이
        3. angle_min, angle_max = -2PI ~ 2PI
        4. angle_increment = PI/360
        5. range_min : Point Cloud의 최소 감지 거리(m)
        6. range_max : Point Cloud의 최대 감지 거리(m)
        **remap from을 잘 수정해야한다.**
        ```(xml)
        <remap from="cloud_in" to="lidar3D"/>
        <remap from="scan" to="scan"/>
3. wego gmapping -> Laserscan 데이터를 이용해서 Mapping
4. wego map_server map_saver -> 맵을 yaml과 pgm 파일로 저장
5. wego navigator launch -> 경로 생성 및 rviz로 맵 및 경로를 보여줌
