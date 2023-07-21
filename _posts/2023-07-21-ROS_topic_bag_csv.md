---
title: "[ROS] Rosbag record & Rostopic to csv"
date: 2023-07-21 14:00:00 +0900
categories: [ROS, Rosbag]
tags: [ROS, record]     # TAG names should always be lowercase
---

## Rosbag record
```shell
$ rosbag record -O /bagfile/저장/경로/파일이름.bag 녹화할 토픽1 녹화할 토픽2 녹화할 토픽3 ...
```
> **Example**
```shell
$ rosbag record -O /home/ubuntu/data/test.bag /ublox_gps/fix /ublox_gps/fix_velocity /ublox_gps/rtcm
```

## Rostopic to csv

```shell
$ rostopic echo -b NAME.bag -p TOPIC_NAME > CSVNAME.csv
```

한번에 한 개의 토픽에 대해 변환됨

> **Example**
```shell
$ rostopic echo -b test.bag -p /ublox_gps/fix > fix_data_RTK.csv
```