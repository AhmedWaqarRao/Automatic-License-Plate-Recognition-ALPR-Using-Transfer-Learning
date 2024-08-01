**Automatic License Plate Recognition (ALPR) Using Transfer Learning on Pakistani Dataset**

This project involves developing an Automatic License Plate Recognition (ALPR) system using transfer learning and the YOLOv3 (You Only Look Once, Version 3) model. The ALPR system is designed to detect license plates on Pakistani cars and recognize the characters on these plates. The project comprises two main parts: detecting the license plate in an image and recognizing the characters on the detected license plate.

**Part 1: Detecting the License Plate**

To begin with, a custom dataset of Pakistani cars was manually collected. The images were annotated using the YOLO format, where each annotation specifies the class (license plate) and the coordinates of the bounding box around the license plate. The configuration of YOLO labels is as follows:

```
<object_class> <x_center> <y_center> <width> <height>
```

Since the detection task involves only one class, the label for the license plate is used exclusively. An example annotation for a license plate is provided below:

```
0 0.5 0.5 0.2 0.1
```

This format indicates the license plate class (0), and the normalized coordinates of the bounding box (center x, center y, width, height).

**Part 2: Recognizing the Characters of the License Plate**

After detecting the license plate, the next step is to recognize the characters on the plate. This task involves 36 classes: 26 classes for the letters A-Z and 10 classes for the numbers 0-9. Each character on the detected license plate is annotated separately using the YOLO format. The characters are labeled with numbers 0-25 for letters A-Z and 26-35 for numbers 0-9.

For instance, an annotation for characters on a license plate might look like this:

```
1 0.4 0.5 0.1 0.2
2 0.6 0.5 0.1 0.2
```

These annotations indicate the class and bounding box coordinates for each character.

**Training the Model**

The training process involves using the YOLOv3 model. The Darknet framework, which is an open-source neural network framework, was used for training. The necessary configurations in the YOLO configuration file (yolov3.cfg) were tuned to match the dataset requirements. Here are the key configuration changes:

**a. Configuration for Detecting License Plate:**
- `batch=16`
- `subdivisions=4`
- `max_batches=9000`
- `steps=7200,8100`
- `classes=1` (for YOLO layers)
- `filters=18` (for convolutional layers preceding YOLO layers)

**b. Configuration for Recognizing Characters:**
- `batch=16`
- `subdivisions=4`
- `max_batches=6000`
- `steps=4800,5400`
- `classes=36` (for YOLO layers)
- `filters=123` (for convolutional layers preceding YOLO layers)

Pre-trained weights from the Darknet model were used to initialize the training. These weights can be downloaded using the following link: [darknet53.conv.74](https://pjreddie.com/media/files/darknet53.conv.74).

To start the training, the following command was used in the terminal:

```bash
./darknet detector train data/obj.data cfg/yolov3-voc_mine.cfg darknet53.conv.74
```

**Results**

The ALPR system was evaluated on various images and videos to ensure its robustness and accuracy. The results showed that the system could detect and recognize license plates with high accuracy. The detection accuracy for the license plates was over 90%, and the character recognition was precise in most scenarios.

The system's performance was visualized through various images and video demonstrations, showcasing its capability to handle real-world scenarios effectively. The following images illustrate the detection and recognition process:

- Detection of license plates in static images.
- Recognition of characters on the detected license plates.
- Real-time detection and recognition in video footage.

**Conclusion**

The Automatic License Plate Recognition project using YOLOv3 demonstrates the effectiveness of transfer learning and deep learning models in handling complex computer vision tasks. By developing a custom dataset and fine-tuning the YOLOv3 model, the project achieved high accuracy in detecting and recognizing license plates on Pakistani cars. This system can be utilized for various applications, such as traffic monitoring, law enforcement, and automated toll collection, significantly contributing to the advancement of intelligent transportation systems.
