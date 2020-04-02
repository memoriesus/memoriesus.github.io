---
post: page
title: Convert multiArray to image in CoreML
subtitle: understand why sometime you can convert multiArray to image
tags: [CoreML,iOS]
comment: true 
---

## What's multiArray?
Multidimensional arrays are commonly used to represent input and output data. Often, each dimension of a multidimensional array has an associated label or meaning. For example, Core ML neural network models use a C x H x W layout for images, where C is the number of channels, H is the height of the image, and W is the width.

But sometimes the input type of CoreML model is multiArray.It's so common. But sometimes we desired the type is image because it's inconvenient -if a model works on images, it should accept images as input.
It's not easy to do

`import coremltools
  import coremltools.proto.FeatureTypes_pb2 as ft

  spec = coremltools.utils.load_spec("")

  input = spec.description.input[0]

  input.type.imageType.colorSpace = ft.ImageFeatureType.RGB

  input.type.imageType.height = 224

  input.type.imageType.width = 224

  coremltools.utils.save_spec(spec,"")`
  
  This script changes the data type of the first input to expect an image.
  >Note: If necessary, change colorSpace to GRAYSCALE OR BGR.You should use BGR if the model was trained with Caffe or if 
  OpenCV was used to load the trainning image. CoreML will automatically convert the pixel order of your input image to whatever
  format the model requires, but you should only do this if you set colorspace correctly.
  Also make sure that the width and height are also right.
