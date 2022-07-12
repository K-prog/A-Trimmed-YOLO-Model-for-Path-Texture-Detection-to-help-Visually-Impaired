
# A Trimmed YOLO Model for Path Texture Detection to help Visually Impaired

Path texture detection is still a less explored area due
to the lack of sufficient standard path texture datasets. Most of
the works have been done to recognize the texture of materials
such as stone, wood, paper, brick etc and overlooked the need for
detection and recognition of various path textures. Apart from the
sighted persons, the visually impaired need to recognize the
type and textures of the path for their safety. We have developed models to detect and recognize various
path textures such as Broken Path, Cemented Path, Concrete
Path, Foot Path, Grassy Path, Muddy Path, Pavement, and Tiled
Path. The proposed model relies on the Yolov5 model that works
on DarkNet-53, and its different variations such as Yolov5l and
Yolov5s. The model pruning, as well as model quantization, have
been experimented with to reduce the dimensions
of the model for deployment on resource-constrained devices. A
custom-built dataset of 8 classes having a sample set of 24,000
images has been used for the experimentations. The findings and
results indicate that the proposed model is a lightweight model
with good accuracy in detecting and recognizing path textures
in real-time.


## Sample Images

![App Screenshot](https://cdn.discordapp.com/attachments/829041911028776960/996164838319456277/0_1.jpg
)

![App Screenshot](https://cdn.discordapp.com/attachments/829041911028776960/996165468396204162/4_1.jpg
)
## Algorithm

![App Screenshot](https://cdn.discordapp.com/attachments/829041911028776960/996165851969486878/unknown.png
)

## Updates in model

- Image Pre-processing and dataset preparation
        
    The dataset consists of 40000 images divided into 8 classes(referencing the 8 classes). The train and validation split is in the ratio of 80:20 i.e., 32000 for training and 8000 for validation.   All the images are resized to 416*416 for efficient training as the yolov5 architecture accepts the size of images in multiples of 32. 
- Post-training pruning

    After the model's training, soft pruning(making the weight value of neurons zero) is performed to improve the model’s performance by using PyTorch functions.
- Quantization of weights in INT8 and FP16  

    The PyTorch weights are quantized to tflite format by casting all the floating point 32 weight values to integer and floating-point 16, reducing time in calculations and increasing inference speed and significant difference in model size.



## Results

### YOLOR VS YOLOV5S

Model | mAP .5 | mAP .5:.95 | Size (mb) | Precision | Recall | Inference Time (torch 1.9.0+cu102 CPU)
------------ | ------------- | ------------- | -------------| ------------- | ------------- | -------------
Yolov5s | 0.939 |0.744 | 14.1|0.895 |0.877 | 57.8 ms|
YoloR | 0.932 | 0.746|291 | 0.955|0.688 | 523.9 ms|

### Yolov5s vs Yolov5s FP16 tflite quantized vs Yolov5s INT8 tflite quantized

Model | mAP .5 | mAP .5:.95 | Size (mb) | Precision | Recall | Inference Time (torch 1.9.0+cu102 CPU)
------------ | ------------- | ------------- | -------------| ------------- | ------------- | -------------
Yolov5s | 0.939 |0.744 | 14.1|0.895 |0.877 | 57.8 ms|
Yolos FP16 tflite | 0.941 | 0.744|13.9 | 0.888|0.878 | 168.9 ms|
Yolos INT8 tflite | 0.882 | 0.55|7.3 | 0.8|0.836 | 15999.6 ms|

### Yolov5l vs Yolov5l FP16 tflite quantized vs Yolov5l INT8 tflite quantized

Model | mAP .5 | mAP .5:.95 | Size (mb) | Precision | Recall | Inference Time (torch 1.9.0+cu102 CPU)
------------ | ------------- | ------------- | -------------| ------------- | ------------- | -------------
Yolov5l | 0.928 |0.729 | 91.6|0.882 |0.866 | 200.4 ms|
Yolol FP16 tflite | 0.928 | 0.729|91.3 | 0.883|0.866 | 632.4 ms|
Yolol INT8 tflite | 0.915 | 0.617|46.7 | 0.875|0.841 | 523.9 ms|

### Yolov5s vs Pruned Yolov5s

Model | mAP .5 | mAP .5:.95  | Precision | Recall | Inference Time (torch 1.9.0+cu102 CPU) | Inference Time (Tesla V100-SXM2-16GB)
------------ | ------------- | ------------- | -------------| ------------- | ------------- | -------------
Yolov5s | 0.939 |0.744 |0.895 |0.877 | 144 ms| 3.3 ms|
Yolos 30% Pruned | 0.936 | 0.729 | 0.882|0.878 | 125.3 ms|2.7 ms |


## Authors
- [Kanak Manjari](https://github.com/kmanjari)
- [Karan Singh](https://github.com/K-prog)
- [Madhushi Verma](https://github.com/vermam1234)
- [Gaurav Singal](www.gauravsingal.in)
- Swagtham Das
