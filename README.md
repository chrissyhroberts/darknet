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


* Annotate images in CVAT
* Export to YOLO format
* Put files in data/whill (Each is a JPG and a YOLO text file)
* Edit divide.py to modify the target folders - things to change on lines 8,9,15 and 16
* Run divide.py inside the python folder
	* Creates whill-test.txt and whill-train.txt in the top level directory
* Make config files for the training
	* Copy yolo3.cfg to whill-frozen.cfg
* Edit whill-frozen.cfg
	* line 6 | batch = 16
	* line 7 | subdivisions = 4
	
	Determine max_batches
	number of classes (i.e. things being detected) * 2000 (but can be more if you want)
	
	* line 610 | classes=1
	* line 696 | classes=1
	* line 783 | classes=1
	
	Calculate filters=(classes + 5)*number of mask
	
	* line 603 | filters=18
	* line 689 | filters=18
	* line 776 | filters=18
	
	Determine steps 
	80% and 90% of max batches

	* line 20 | max_batches = 2000
	* line 22 | steps=1600,1800

	
	* add to [shortcut] section | stopbackward=1 # freeze weights above
		
* Copy whill-frozen.cfg to whill.cfg
* Remove comment out on line 3  and 4 | batch=1 / subdivisions=1
* Comment out lines 6 & 7 | #batch=16 / #subdivisions=4

* Edit data/whill.names and add names on lines relating to yolo classes 0,1,2 etc
* Edit cfg/whill.data, ensure classes is correct and paths defined properly
* Edit makefile and ensure line 1 | GPU=1


# In Colab

* Start a GPU session 
* Open darknet.ipynb
	* A100 GPU with High RAM
	