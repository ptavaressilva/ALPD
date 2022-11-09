# Automatic License Plate Detection (ALPD)

The objective of this (ongoing) project is to practice computer vision object detection by detecting motor vehicle license plates in motorway videos.

## Creating the dataset

For this project I shot 39 videos (1 to 2 minutes long) in a spanish motorway. 80% of these videos are destined to train YOLOv5 to recognize license plates, cars buses and trucks. The remaining videos are used for validation.

Frames were extracted at every second of the video, which resulted in 955 images for training and 191 for validation (17% of the total).

As the ulterior objetive of this project is to embed the detection code in a Raspberry Pi 4 B with a Picam, for real time detection, YOLOv5s will be used and trained with 640x640 images (rather than the larger alternative).

From each frame, three 640x640 images were created, further augmenting the dataset, reaching a a grand total of 3.434 images.

These images were then annotated with bounding boxes using [CVAT](https://github.com/opencv/cvat) installed on a local machine with Docker.

![Image annotation](img/CVAT_annotation.gif)

**Data availability notice**: in Spain license plates are considered Personal Data. Therefore the dataset created for this exercise is not provided along with the code.

## Prediction with pretained model

A prediction was made with YOLOv5s out of the box (see noteblook 03). As YOLOv5 was pretrained with COCO, it recognizes the vehicle classes in that dataset, but not the license plates.

The COCO vehicle clases are:

![COCO vehicle clases](img/COCO_vehicles.png)

The dataset created for this project has a new class called `license_plate`, as well as the COCO clases considered relevant for our purposes (car, truck and bus).

## Next steps

This project is ongoing. The next steps are:

1. Setup Neptune.ai for experiment logging and artifact registry.
2. Convert the CVAT output from Yolo v1.1 format to the format required by YOLOv5.
3. Train YOLOv5s with a smaller set of 200 training images, in order to test the training setup.
