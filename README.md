# Automatic_License_Plate_Recognition
On Pakistani Dataset using Transfer Learning

This ALPR Project has two parts:

# 1. Detecting the License Plate from the entire image:

We manually collected our custom dataset of Pakistani cars, and then annotated them using YOLO format. The configuration of yolo labels is as follows:

<object_class> <x_center> <y_centre> <width> <height>
  
 Since, we are only try to detect the License Plate only 1 label is involved i.e License Plate. An example of annotation file is as follows:
  
  ![image](https://user-images.githubusercontent.com/58310295/134763308-1cce4974-caed-454d-813d-77b3edc489a6.png)

# 2. Recognizing the characters of the License Plate:
  
After the License Plate has been detected, the task is to recognize the characters of that License Plate. There are 36 classes involved in this case. 26 classes for letters A-Z and 10 classes for numbers 0-9.
  
We annotated each of the character separately from the detected License Plate using the yolo format labelling. 
  
For example lets consider the following image
  
![image](https://user-images.githubusercontent.com/58310295/134763887-993e0679-c49e-4b74-8a93-c22351d883ea.png)

Numbers 0-25 are used for the letters A-Z and numbers 26-35 are used to represent the number 0-9 on a license plate. For the above images the annotation file is:
  
![image](https://user-images.githubusercontent.com/58310295/134763965-f4dc8596-261b-496a-8420-bd88f6de5eb2.png)
  
# Training:
  
Since we are training by using YOLO v3 we do that by cloning the darknet github repo of pjreddie using the following link:
  
https://github.com/pjreddie/darknet
  
# Tuning cfg file in darknet:
  
configuration files (or config files) are files used to configure the parameters and initial settings for some computer programs. Parameters and initial settings can be specific values that should be applied in our system when it is running.
  
To train our own dataset we need to tune config file to be compatible with our dataset.

We need to update the yolov3.cfg file as follows to be compatible with our own dataset:
  
# a. Tuning cfg for Detecting License Plate:

batch=16
  
subdivisions=4
 
max_batches=9000
  
steps= 7200, 8100

Similarly, in line# 611, 695 and 779 we set the number of classes to (in YOLO Layer):
  
classes=1
  
Also, in line$ 605, 689 and 773 we set the number of filters to (in convolutional layer):
  
filters=18
  
# b. Tuning cfg file for Recognizing characters of License Plate:
  
batch=16
  
subdivisions=4
 
max_batches=6000
  
steps= 4800, 5400

Similarly, in line# 611, 695 and 779 we set the number of classes to (in YOLO Layer):
  
classes=36
  
Also, in line$ 605, 689 and 773 we set the number of filters to (in convolutional layer):
  
filters=123
  
  
To start training we first download darknet pre_trained weights using the following link:
  
https://pjreddie.com/media/files/darknet53.conv.74
  
To start training, we use the following command:
  
!./darknet detector train data/obj.data cfg/yolov3-voc_mine.cfg darknet53.conv.74
  
# Results:
  
1. Image
  
![image](https://user-images.githubusercontent.com/58310295/134764732-50645544-3dda-49f9-8c81-a377ae252719.png)
  
![image](https://user-images.githubusercontent.com/58310295/134764751-2a517ef4-9151-4048-b3cb-52a94e3efde3.png)

2. Image

![image](https://user-images.githubusercontent.com/58310295/134764767-7f212996-bd4f-4042-b4c9-46dc56e3c797.png)

![image](https://user-images.githubusercontent.com/58310295/134764795-1659e1fa-02a1-48b9-87f6-dd77b5e337d1.png)

  
3. Image:

![image](https://user-images.githubusercontent.com/58310295/134764827-8517e13f-8bb0-4018-905e-69512c9edf85.png)
  
![image](https://user-images.githubusercontent.com/58310295/134764843-630b61a2-8dee-42c2-b964-4988302db258.png)
  
4. Image:
  
![image](https://user-images.githubusercontent.com/58310295/134764861-f28097d2-0749-4700-8394-af2e4a4c5014.png)

![image](https://user-images.githubusercontent.com/58310295/134764876-2fc1de8c-51ea-42f6-ae36-463a31833452.png)

5. Detection on a Video:
  
https://user-images.githubusercontent.com/58310295/134765656-96692c1c-ca53-4b1e-b054-c51f9757cba2.mp4



