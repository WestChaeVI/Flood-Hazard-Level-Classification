# Flood Hazard Level Classification(2023)    

**Chaejun Seo<sup>o, $</sup>**, Seongmin Cho<sup>$</sup>, Seunghyeok Hong<sup>*</sup>. (2023).   
Enhancing the Safety Response Capability of Flood Hazard 
Level Classification Model using DINOv2 Unsupervised Image Learning and Parameter Tuning      
[한국정보과학회 학술발표논문집, pp ??~??]()      

------------------------------------------------------------------------------------------------------------------------       

## Abstract     

Water level hazard monitoring plays a crucial role in environmental disaster management. Flooding is one of the severe disasters that can occur in urban and riverine areas, causing significant damage to lives, property, and infrastructure. Therefore, accurately monitoring flood levels and understanding the risk levels are essential tasks. Unsupervised learning is a machine learning method used for discovering patterns or structures in given data or grouping data without explicit labels. In this paper, we propose a generalized flood level risk classification model using the [Mask2Former](https://arxiv.org/abs/2112.01527) model using the [DINOv2](https://arxiv.org/abs/2304.07193) model as the backbone, an unsupervised learning model, through CCTV footage of rivers. Flood level risk classification is calculated based on the ratio of water area pixel values.      

------------------------------------------------------------------------------------------------------------------------       


## Introduction     

Globally, typhoons and concentrated heavy rainfall events are occurring more frequently, leading to annual flooding and road inundation damages due to the impact of global warming. In response to this, various flood management systems, such as flash flood forecasting systems and flood integrated management systems, have been introduced. However, current river flooding alert systems primarily utilize simple sensor data such as water level and rainfall to trigger alerts, making real-time monitoring of flood situations less effective. Classifying flood risk levels based on water levels is a crucial task for flood management and disaster response in river environments to minimize flood damage. Previous studies on flood datasets have continuously explored methods such as Reflection Attention Units (RAU) and Fully Convolutional Network (FCN) for detecting water puddles and flood areas, as well as applying Region-based CNN (R-CNN) and Scale Invariant Feature Transform (SIFT) for road flood detection in the field of environmental disasters. The contemporary fields of technology and data are exploring innovative approaches, and this paper proposes a new solution using the unsupervised learning-based DINOv2 model for addressing these challenges.    

------------------------------------------------------------------------------------------------------------------------       


## Dataset      

The dataset used in the experiments comprises 1-hour CCTV footage capturing flood events from 17 river regions. Each video was divided into frames at intervals of 15 or 30 frames per second, resulting in a total of 20,400 images. The risk levels are categorized into four stages: attention, caution, warning, and alert, as provided by the Han River Flood Control Office. As the flood progresses, one can observe a gradual rise of water in the river inundating meadows, sidewalks, and eventually roads (Figure 1).      

### Figure 1      
#### Images of Flood Stages in River CCTV Footage   

<p align="center"><img src="https://github.com/WestChaeVI/Flood_Hazard_Level_Classification/assets/104747868/f7504cc6-94d4-4d3c-ba66-9317f1ec1936" height='500'>       

------------------------------------------------------------------------------------------------------------------------       


## DINOv2 Results    

In this study, the areas corresponding to water in each frame were segmented, and the risk level of each frame was evaluated using the risk classification indicators introduced in next section. Representative images corresponding to the five levels: "normal," "attention," "caution," "warning," and "alert" were selected, and region segmentation using the DINOv2 model was performed (Table 1). DINOv2 adopts an unsupervised learning approach, and as the class values corresponding to water are not known in advance, they need to be identified directly. The DINOv2 analysis for "normal" images revealed a class value of 60 for the water, while the remaining four levels showed an observed class value of 21. These results confirm that the DINOv2 model discriminates between clear water in the "normal" stage and turbid water in the other stages. As the main goal of this study is to assess the risk level of flooding, pixels corresponding to class values 21 and 60 in all frames were separated as water, identifying the entire water area (Figure 2).     

### Figure 2      
#### Binary Classification Images of "Clear/Turbid Water" pixels     

<p align="center"><img src="https://github.com/WestChaeVI/Flood_Hazard_Level_Classification/assets/104747868/1bf976df-f4b3-4f92-adce-f3a901075ed3" height='500'>        

------------------------------------------------------------------------------------------------------------------------       


## Risk Level Classification Metric      

The criteria for risk levels are set by the Advanced Water Resources Engineering Research Lab at Korea University. The stages progress in the order of embankment, meadow, bicycle road and sidewalk, and car road, with the starting point being when the river begins to swell after the onset of rainfall (Figure 3).       

### Figure 3      
#### The criteria for flood risk levels in the river     

<p align="center"><img src="https://github.com/WestChaeVI/Flood_Hazard_Level_Classification/assets/104747868/fde23b7c-4be3-4caa-a09e-e9567de4b824" height='500'>      

The scoring method for each risk level was calculated using Equation (1). It involves calculating the ratio between frame-level images and the image taken at the point of the most severe water level within the video. This method is based on the maximum water level for each video, allowing for the classification of risk levels for any CCTV footage capturing a flood. Since the maximum water level in the river, terrain features, and nearby structures vary for each video, these were treated as hyperparameters (Table 1).   

### Equation 1     

$$\text{score} \ = \ \frac{\text{water pixels (frame)}}{\text{water pixels (maximum flood)}} \\ \ \  (1)$$        

To assess how effectively the flood risk levels can be classified when performing flood detection in a new river area, a comparative experiment was conducted between the unsupervised learning-based DINOv2 model and the supervised learning-based ResNet50 model. To evaluate the classification of flood risk levels on new CCTV data, experiments were conducted by inferring on data from the same region used for training and data from different regions. The comparison was made between five classes and two classes (Table 2). The two classes were composed of "normal," "attention," and "caution" in one group, and "warning" and "alert" in the other group among the five classes. This was done to verify the flexibility of the models in classifying flood risk levels in varying scenarios.

### Table 1     
#### Risk Level Score Calculation Method     
 
|     Level    	| normal 	| attention 	|  caution  	|  warning  	| alert 	|
|:------------:	|:------:	|:---------:	|:---------:	|:---------:	|:-----:	|
|   Threshold  	|  ~ 14% 	| 14% ~ 21% 	| 21% ~ 28% 	| 28% ~ 35% 	| 35% ~ 	|
| DINOv2 Image 	| <p align="center"><img src="https://github.com/WestChaeVI/Flood_Hazard_Level_Classification/assets/104747868/65ea7f93-4105-4093-9cf2-9b0439ea5958" width='400'>       	|      <p align="center"><img src="https://github.com/WestChaeVI/Flood_Hazard_Level_Classification/assets/104747868/4bd63f63-c147-4206-81cc-1a4ed713a6cb" width='400'>     	|       <p align="center"><img src="https://github.com/WestChaeVI/Flood_Hazard_Level_Classification/assets/104747868/b98f1c6c-79a8-4c29-938c-280d7f881185" width='400'>     	|       <p align="center"><img src="https://github.com/WestChaeVI/Flood_Hazard_Level_Classification/assets/104747868/7cd53306-ffbb-47dd-a803-6602a407dac6" width='400'>    	|   <p align="center"><img src="https://github.com/WestChaeVI/Flood_Hazard_Level_Classification/assets/104747868/adcbeb31-d783-4524-a4d2-6a15173e32b1" width='400'>     	|         

------------------------------------------------------------------------------------------------------------------------       


## Results and Discussion      

In this study, a notable performance difference was observed between supervised and unsupervised learning when the training and testing datasets differed. The accuracy of supervised learning was 66.67%, while unsupervised learning achieved an impressive 96.67%. Moreover, the ResNet50 model exhibited a training time of 1 minute and 31 seconds, with an inference time of 0.08 seconds per frame. In contrast, the DINOv2 model had an inference time of 1.7 seconds. The supervised learning model showed an exponential increase in processing time as new CCTV data was introduced, whereas the unsupervised learning model, requiring no training, proved to be more efficient in inference only.

Similar research cases utilizing CCTV footage from different regions to discern flood occurrence have been reported. In these cases, VGG16 achieved an accuracy of 90.8%, ResNet50 reached 91.7%, and EfficientNet demonstrated an accuracy of 90.2% based on the test set. This suggests that the proposed DINOv2 model not only outperforms traditional supervised learning models but also exhibits promising efficiency in real-time flood risk assessment. The findings emphasize the potential of unsupervised learning in dynamic and evolving environmental monitoring scenarios.    


### Table 2      
#### Test Accuracy Based on Model and Class-Specific Datasets with the Same CCTV     
 
<table>
  <thead>
    <tr>
      <th></th>
      <th colspan="2">5 class</th>
      <th colspan="2">2 class</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td></td>
      <td style="text-align: center;">Same</td>
      <td style="text-align: center;">W/O Same</td>
      <td style="text-align: center;">Same</td>
      <td style="text-align: center;">W/O Same</td>
    </tr>
    <tr>
      <td style="text-align: center;">ResNet50</td>
      <td style="text-align: center;">100.0%</td>
      <td style="text-align: center;">20.00%</td>
      <td style="text-align: center;">100.0%</td>
      <td style="text-align: center;">66.67%</td>
    </tr>
    <tr>
      <td style="text-align: center;">DINOv2</td>
      <td style="text-align: center;">96.67%</td>
      <td style="text-align: center;">56.67%</td>
      <td style="text-align: center;">100.0%</td>
      <td style="text-align: center;">96.67%</td>
    </tr>
  </tbody>
</table>
   


 


