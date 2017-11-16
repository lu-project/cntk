# Lableup CNTK(Microsoft Cognitive Toolkit) service
Integrate with Microsoft Deep Learning toolkit [Microsoft Cognitive Toolkit - CNTK](https://www.microsoft.com/en-us/cognitive-toolkit/) into Lablup backend.ai

## Introduction
Integrating with Lablup backend.ai service to support deep learning technology of Microsoft CNTK. 

## Building docker image and pratical CNTK code
In this repository, provide backend.ai docker image and CNTK practical code for working on CNTK docker image

## Docker image for CNTK
Python-CNTK docker image wrapped with backend.ai's jail support was built. The CNTK version is 2.2 in Ubuntu 16.04 environment. Some features of this images are:

* Can execute user's custom code upon requested through backend.ai's manager/agent service. 
* Supports Keras frontend. 
* Jail support: backend.ai's jail layer wraps a container to provides additional security protection. Detaild settings can easily be tweaked by policy.yml file.
  * It limits resource usage for a container, to prevent one container consumes all of the resources of the server.
  * It filters all syscalls to keep a container safe against malcious code running inside the container. Only whitelisted syscalls are allowed to be called, and the list can be adjusted by policy.yml depending on the purpose of images.

This image currently supports rather basic features of CNTK, but we are planning to add commonly-used toolkits. 

The optimization of the docker image will also be needed. To reduce the size of the image (which will improve the container loading time), we are also planning to adopt [minideb](https://github.com/bitnami/minideb) as a base image, which is a minified version of Debian linux. 

## Practical code for CNTK service on backend.ai
This Python-CNTK image was tested to successfully execute the following very short code snippets.

```python3
# Test python3 is working
print("hello world")
```
Output contains: `hello world`

```python3
# Test CNTK is working
import cntk
import numpy as np
x = cntk.input_variable(2)
y = cntk.input_variable(2)
x0 = np.asarray([[2., 1.]], dtype=np.float32)
y0 = np.asarray([[4., 6.]], dtype=np.float32)
print(cntk.squared_error(x, y).eval({x:x0, y:y0}))
```
Output contains: `[ 29.]`

```python3
# Test Keras as a frontend of CNTK is working
import keras
print(keras.__name__)
```
Output contains: `Using CNTK backend`

More advanced, long-running machine-learning codes can be list here as well. As more useful toolkits are introduced, test cases utilizing them can be added.

## Reference
[CNTK repository](https://github.com/Microsoft/CNTK) 
[Setup Linux Python](https://docs.microsoft.com/en-us/cognitive-toolkit/Setup-Linux-Python?tabs=cntkpy22#tabpanel_FweSSiKxOx_cntkpy22) 
[Object detection using Fast R-CNN](https://docs.microsoft.com/en-us/cognitive-toolkit/object-detection-using-fast-r-cnn)  
[Visual Object Tagging Tool](https://github.com/Microsoft/VoTT)  
