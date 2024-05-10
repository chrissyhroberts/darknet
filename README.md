https://eng-memo.info/blog/yolo-original-dataset-en/

![Darknet Logo](http://pjreddie.com/media/files/darknet-black-small.png)

# Darknet #
Darknet is an open source neural network framework written in C and CUDA. It is fast, easy to install, and supports CPU and GPU computation.

For more information see the [Darknet project website](http://pjreddie.com/darknet).

For questions or issues please use the [Google Group](https://groups.google.com/forum/#!forum/darknet).

Good example of how to train a model here - https://eng-memo.info/blog/yolo-original-dataset-en/

on makefile line 7 remove deprecated runtimes for GPU

this line only needed for T4 GPUs. 

ARCH= -gencode arch=compute_75,code=[sm_75,compute_75]
