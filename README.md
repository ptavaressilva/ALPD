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

A prediction was made with YOLOv5s out of the box (see [03 Yolo v5 prediction](03\ Yolo\ v5\ prediction.ipynb')). This model was pretrained with COCO and recognizes the vehicle classes in that dataset, but not the license plates.

The COCO vehicle clases are:

![COCO vehicle clases](img/COCO_vehicles.png)

The dataset created for this project is annotated with a new class called `license_plate`, as well as the COCO clases considered relevant for our purposes (car, truck and bus).

## Neptune setup

In order to track experiments and save artifacts with Neptune, first create an account at Neptune.ai and then a project. Once the project is created, get the correspoding values for `neptune_project`and `neptune_api_token`.

We will use [IPython Secrets](https://ipython-secrets.readthedocs.io/en/latest/) to keep the secrets secure and make it possible to use them safely in Jupyter notebooks.

When you run the [05 Train YOLOv5s](05\ Train\ YOLOv5s.ipynb) notebook for the first time it will ask you to input the two values. IPython Secrets will store then in your computer's keyring and you can use them in the notebook after that without having to type them in again.

## Next steps

This project is ongoing. The next steps are:

1. Complete the setup of Neptune.ai for experiment logging and artifact registry.
2. Convert the CVAT output from Yolo v1.1 format to the format required by YOLOv5.
3. Train YOLOv5s with a smaller set of 200 training images, in order to test the training setup.
