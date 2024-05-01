# Yolo5/8 in Indoor and outdoor usage

Contributors: Ziqi Liao, Xinmiao Xiong, Pin chun Lu, Yi Wen Chen

### Instructions
a pip or conda requirements file

### How to set up the environment
- [OpenMMLab](https://github.com/open-mmlab): Our detection code uses [MMEngine](https://github.com/open-mmlab/mmengine) and our model is built upon [MMYOLO](https://github.com/open-mmlab/mmyolo).
- [SmokeyNet](https://arxiv.org/pdf/2112.08598): Our classification model is built upon [SmokeyNet] framework. Please refer to their work of managing the environment.
- [Indoor usage with YOLO] Code is avalible here with Colab [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/19zZqunRLepQalh7REmbcu7dlfxJ4yVL0?usp=sharing) 

### run a few demos of approaches

 a project on recognition would at least need to include a couple of images, a trained model, and the code to apply the model to the images.

### Instructions on how to download and pre-process dataset

# Indoor: Electronic Device Detection 
## Background
This section serves as our base case for comparing with the outdoor Wildfires project. To understand how YOLO usage differs between indoor and outdoor scenarios, we have tested indoor scenarios with fixed-angle cameras and first-person views. We have used YOLOv5 and YOLOv8 for this purpose.  

## Findings
(1) YOLOv5 provides higher accuracy but does not detect everything in the frame.  
(2) YOLOv8 provides lower accuracy but detects everything in the frame.  
(3) Both YOLOv5 and YOLOv8 perform well in indoor detection when the object is at a certain distance and has the right angle with the camera.  
(4) In first-person view detection, the performance is not as good due to two main reasons:  
    a. The distance is different from the COCO dataset used for YOLO pre-training.  
    b. The person wearing the recording glasses is moving, and the movement and changing angles might blur the frame.  

## Setup and Demo

[Indoor usage with YOLO] Code is available here with Colab: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/19zZqunRLepQalh7REmbcu7dlfxJ4yVL0?usp=sharing)

# Outdoor Detection: Wildfires project 
## Background
Wildfires are increasing around the globe in frequency, severity, and duration, heightening the need to understand the health effects of wildfire exposure. The risk of wildfires grows in extremely dry conditions, such as drought, heat waves and during high winds.
With climate change leading to warmer temperatures and drier conditions and the increasing urbanization of rural areas, the fire season is starting earlier and ending later. Wildfire events are getting more extreme in terms of acres burned, duration and intensity, and they can disrupt transportation, communications, water supply, and power and gas services. 


## Motivation
- A comprehensive sensing framework is needed to assess wildfire risks more accurately and enable strategic decisions
   - Commonly used sensors enable (temperature, humidity, particle, etc.) short-range detection.
   - Long-range detection (~1km-10km) can be enabled using cameras.
- Challenges in edge-devices:
   - Resource-constraint devices.
   - Communication is costly.

## methodology (method, data, evaluation metrics)
If applicable, highlight how it differs from prior work (new experiments, new methods, etc)
Dataset: www.hpwren.ucsd.edu/HPWREN-FIgLib
Reference paper: FIgLib & SmokeyNet: Dataset and Deep Learning Model for Real-Time Wildland Fire Smoke Detection (arxiv.org)
Method: Object Detection + TileToImage binary classification
Difference: We make the inference model on Jetson and to estimate the energy consumption.
Visual: the gif in presentation slide
Demos: on Github

## Models Evaluated

- **ResNet34**: This is a 34-layer Residual Network model, commonly used in image recognition tasks for its efficiency and accuracy.
- **YOLOv8**: The latest version of the You Only Look Once model, YOLOv8 is designed for enhanced real-time object detection.
- **ResNet+ViT**: A hybrid architecture that combines the Residual Network (ResNet) and Vision Transformer (ViT) to capitalize on both their strengths in processing image data.


## Performance Metrics

- **Paras (Parameters)**: Represents the total number of trainable parameters within the model. This metric indicates the model's complexity and memory requirements.
- **Time**: Measures the time required for one iteration during training, impacting the overall training speed.
- **Acc (Accuracy)**: Denotes the percentage of correct predictions made by the model on the test dataset.
- **F1 Score**: A metric that considers both precision and recall to provide a balance between the two by calculating their harmonic mean.
- **Precision**: The ratio of correctly predicted positive observations to the total predicted positives. High precision relates to a low rate of false positives.


## Detailed Performance Table

| Model        | Parameters | Time per Iteration | Accuracy (%) | F1 Score | Precision (%) |
|--------------|------------|--------------------|--------------|----------|---------------|
| ResNet34     | 22.3M      | 50.4 ms/iter       | 75.5         | 73.2     | 82.0          |
| YOLOv8       | 43.6M      | 80.3 ms/iter       | 68.0         | 45.3     | 87            |
| ResNet+ViT   | 60.2M      | 65.2 ms/iter       | 81           | 76       | 89            |

## Summary

This table highlights the trade-offs between model complexity, performance, and training efficiency. It provides insights into which model might be most appropriate based on the specific requirements and constraints of the task at hand.

## Discuss:
The detection model is based on YOLOV8. It can produce good false positive rate but missing too many real signals. And it requires more time to compute the possible boxes. --
ResNet+ViT enable the model to learn the spatial information and can produce better acc at a higher inference speed.
## Reference of Dataset:
The main dataset is [HPWREN](https://www.hpwren.ucsd.edu/FIgLib).

The mini set is [AI-Humankind](https://public.roboflow.com/object-detection/wildfire-smoke).
## License:

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/80x15.png" /></a>
<br />
This work is under the <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>
