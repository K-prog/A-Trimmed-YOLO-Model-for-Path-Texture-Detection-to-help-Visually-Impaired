
# QYOLO: A Quantized YOLO Model for Path Texture Detection to help the Visually Impaired


Owing to the lack of sufficient standard path texture datasets, its detection is still a topic that has not received much attention. The majority of research has been focused on identifying the textures of objects like stone, wood, paper, and brick, but has disregarded the necessity of identifying different path textures. The partially sighted, must be able to identify the kind and textures of the route for their wellbeing. We have created models that can analyse and identify a variety of path textures, including broken, cemented, concrete, foot, grassy, muddy, paved, and tiled paths. The state of the art Yolov5 model, which runs on DarkNet-53, and its variants (Yolov5l and Yolov5s), are the foundation of the suggested model. To decrease the parameters, as  the model will be deployed on devices with limited resources, model pruning and model quantization have both been tested. For the experiments, a bespoke dataset with 8 classes and a sample collection of 24,000 pictures was used. The research findings and outcomes show that the suggested model is a simple model with good real-time path texture detection and recognition correctness.


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
- [Gaurav Singal](https://github.com/Gauravsingal)
- Swagtham Das
