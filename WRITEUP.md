# Project Write-Up

You can use this document as a template for providing your project write-up. However, if you
have a different format you prefer, feel free to use it as long as you answer all required
questions.

## Explaining Custom Layers

* The process behind converting custom layers depends on frameowrks we use either it is tensorflow,caffee or kaldi.We can find it [<==>](https://docs.openvinotoolkit.org/2019_R3/_docs_MO_DG_prepare_model_customize_model_optimizer_Customize_Model_Optimizer.html) here.

* Some of the potential reasons for handling custom layers is to optimize our pre-trained models and convert them to a intermediate representation without a lot of loss of accuracy and of course shrink and speed up the Performance.

## Difference in Cloud and Edge
* My method(s) to compare models before and after conversion to Intermediate Representations
were...

* The difference between model accuracy pre- and post-conversion was that it decreased because model was shrinked and help make it faster, although this will not give the model higher inference accuracy. In fact, there will be some loss of accuracy as a result of potential changes like lower precision. However, these losses in accuracy are minimized.

* The size of the model pre- and post-conversion was gradully reduced like when i downloaded it was approxiamtely of 140 MBs and after conversion into IR it reduced to KBs.

* If we compare edge with cloud.We can found the cloud is very costly as they have very high computational costs but edge is relatively cheaper as well as faster becuase we are not calling the servers again and again for the requests.Whether I compare it with Google Cloud,Azure or AWS it will always cost lesser than these.Cloud also have more network needs than this.

## Assess Model Use Cases

Some of the potential use cases of the people counter app are:
 *  It helps to improve in-store operations.
 *  Every business with a physical space should count customer traffic to see the bigger picture of what is going on in their business.
 *  It provides valuable visitor analytics.

* Each of these use cases would be useful because every business whether you are a shopping center, retail chain, museum, library, sporting venue, bank, restaurant or other.People Counting data will help you make well-informed decisions about your business.
* It can help to optimize sales and conversions.

## Assess Effects on End User Needs

Lighting, model accuracy, and camera focal length/image size have different effects on a
deployed edge model. The potential effects of each of these are as follows:
 * Better be the model accuracy more are the chances to obtain the desired results through an app deployed at edge.
 * Lighting here refers to lighter the model more faster it will get execute and more adequate results in faster time as compared to a heavier model.
 * Focal length/image also have a effect as better be the pixel quality of image or better the camera focal length,more clear results ww will obtain.



## Model Research

[This heading is only required if a suitable model was not found after trying out at least three
different models. However, you may also use this heading to detail how you converted 
a successful model.]

In investigating potential people counter models, I tried each of the following three models:

## Model 1: [ssd_mobilenet_v2_coco]
 
 - [http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v2_coco_2018_03_29.tar.gz]
- I converted the model to an Intermediate Representation with the following arguments... 
  * wget http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v2_coco_2018_03_29.tar.gz
 - Unpack the file
   * tar -xvf   ssd_mobilenet_v2_coco_2018_03_29.tar.gz
- To go in the directory
   * cd ssd_mobilenet_v2_coco_2018_03_29
   * export MOD_OPT=/opt/intel/openvino/deployment_tools/model_optimizer
- Command to run 
  * python $MOD_OPT/mo.py --input_model frozen_inference_graph.pb --tensorflow_object_detection_api_pipeline_config pipeline.config --   reverse_input_channels --tensorflow_use_custom_operations_config/opt/intel/openvino/deployment_tools/model_optimizer/extensions/front/tf/ssd_v2_support.json
  * .xml and .bin files were obtained in 57.86 seconds
 
 - The model was insufficient for the app because when i tested it failed on intervals like from 24 to 42 seconds it did not worked as it didn't found the bounding boxes around the person and for next person it didn't detected from 52-53 and also on 1:02 to 1:03 didnt't worked.Again from 1:05 to 1:06,1:35 to 1:36,1:52 to 1:53 it didn't worked.
so it is not suitable to choose this model.
 
  
## Model 2: [faster_rcnn_inception_v2_coco_2018_01_28]
  
  - [http://download.tensorflow.org/models/object_detection/faster_rcnn_inception_v2_coco_2018_01_28.tar.gz]
 - I converted the model to an Intermediate Representation with the following arguments...
    * wget http://download.tensorflow.org/models/object_detection/faster_rcnn_inception_v2_coco_2018_01_28.tar.gz
  - Unpack the file
    * tar -xvf   faster_rcnn_inception_v2_coco_2018_01_28.tar.gz
- To go in the directory
   * cd faster_rcnn_inception_v2_coco_2018_01_28
- Command to run 
  * python $MOD_OPT/mo.py --input_model frozen_inference_graph.pb --tensorflow_object_detection_api_pipeline_config pipeline.config --   reverse_input_channels --tensorflow_use_custom_operations_config/opt/intel/openvino/deployment_tools/model_optimizer/extensions/front/tf/faster_rcnn_support.json
  
  * it was obtained in 139 seconds
    
 - The model was insufficient for the app because when i tried to use it gave errors as well as core dumped. 
  - I tried to improve the model for the app by checking in documentation and I found that shape attribute is required.So I did that again with shape attribute as well.Still it give errors.
  - Note: So,mentors suggested me to change the model.

## Model 3: [ssd_inception_v2_coco_2018_01_28]
 
 - [http://download.tensorflow.org/models/object_detection/ssd_inception_v2_coco_2018_01_28.tar.gz]
 - I converted the model to an Intermediate Representation with the following arguments...
    * wget http://download.tensorflow.org/models/object_detection/ssd_inception_v2_coco_2018_01_28.tar.gz
  -Unpack the file
    * tar -xvf ssd_inception_v2_coco_2018_01_28.tar.gz
  -To go in directory 
    * cd ssd_inception_v2_coco_2018_01_28
  -Command to run
   * python $MOD_OPT/mo.py --input_model frozen_inference_graph.pb --tensorflow_object_detection_api_pipeline_config pipeline.config --  reverse_input_channels 
--tensorflow_use_custom_operations_config /opt/intel/openvino/deployment_tools/model_optimizer/extensions/front/tf/ssd_v2_support.json

- The model was insufficient for the app because It also has issues like first model where it failed to detect person in specific specific seconds like :It failed in respective seconds 0:07,0:17 and when second person came it didn't worked for 17 seconds from 0:25 to 0:42. Similarly for 3rd person it didn't worked in 51st second,53rd and 1:05  again it failed for 20 seconds from 1:35 to 1:50.thus average duration may not be optained exactly so we cann't use this model as well.


## Model 4: [ssd_mobilenet_v1_coco ]
 
 - [http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v1_coco_2018_01_28.tar.gz]
 - I converted the model to an Intermediate Representation with the following arguments...
    * wget http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v1_coco_2018_01_28.tar.gz
 - Unpack the file
    * tar -xvf ssd_mobilenet_v1_coco_2018_01_28.tar.gz
 - To go in directory 
    * cd ssd_mobilenet_v1_coco_2018_01_28
 -Command to run
   * python $MOD_OPT/mo.py --input_model frozen_inference_graph.pb --tensorflow_object_detection_api_pipeline_config pipeline.config --  reverse_input_channels 
--tensorflow_use_custom_operations_config /opt/intel/openvino/deployment_tools/model_optimizer/extensions/front/tf/ssd_v1_support.json

- These errors lead to failure of conversion of model into IR   
Or because the node inputs have incorrect values/shapes.
[ ERROR ]  Or because input shapes are incorrect (embedded to the model or passed via --input_shape).
[ ERROR ]  Run Model Optimizer with --log_level=DEBUG for more information.
[ ERROR ]  Not all output shapes were inferred or fully defined for node "image_tensor". 


