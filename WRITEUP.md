# Project Write-Up

You can use this document as a template for providing your project write-up. However, if you
have a different format you prefer, feel free to use it as long as you answer all required
questions.

## Explaining Custom Layers

The process behind converting custom layers involves...

Some of the potential reasons for handling custom layers are...

## Comparing Model Performance

My method(s) to compare models before and after conversion to Intermediate Representations
were...

The difference between model accuracy pre- and post-conversion was...

The size of the model pre- and post-conversion was...

The inference time of the model pre- and post-conversion was...

## Assess Model Use Cases

Some of the potential use cases of the people counter app are...

Each of these use cases would be useful because...

## Assess Effects on End User Needs

Lighting, model accuracy, and camera focal length/image size have different effects on a
deployed edge model. The potential effects of each of these are as follows...

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
  - I tried to improve the model for the app by checking in docmentation and I found that shape attribute is required.So I did that again with shape attribute as well.Still it give errors.
  - Note:So,mentors suggested me to change the model.

- Model 3: [Name]
  - [Model Source]
  - I converted the model to an Intermediate Representation with the following arguments...
  - The model was insufficient for the app because...
  - I tried to improve the model for the app by...
