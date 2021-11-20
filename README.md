# Seq_nms_YOLO

#### Membres: Yunyun SUN, Yutong YAN, Sixiang XU, Heng ZHANG

---

## Introduction

![](img/index.jpg) 

This project combines **YOLOv2**([reference](https://arxiv.org/abs/1506.02640)) and **seq-nms**([reference](https://arxiv.org/abs/1602.08465)) to realise **real time video detection**.



## Steps to execute
In order to execute the project, you need to download the code zip and extract it into a folder. Make sure that the `Makefile` has the following changes:
  - The flags `OPENCV` and `CUDDN` must be deactivated.
      `OPENCV=0`
      `CUDDN=0`
  - The `COMMON` and `LDFLAGS` paths must be defined with the correct cuda version:
      `COMMON+= -DGPU -I/usr/local/cuda-10.1/include/`
      `LDFLAGS+= -L/usr/local/cuda-10.1/lib64 -lcuda -lcudart -lcublas –lcurand`

From the `img2video.py` file the `cv2.destroyAllWindows()` function is commented as `libgtk2.0-dev` will not be installed.

Then, you should follow the next steps.

1. Create a conda enviroment:
  `conda create --name yolo python=2.7`
  `source activate yolo`
 
2. Install the necessary libraries with the following commands:
  `conda install -c conda-forge opencv`
  `conda install -c conda-forge matplotlib`
  `conda install -c conda-forge tensorflow`
  `conda install -c anaconda scipy`
  `conda install -c anaconda pillow`
  `pip install tensorflow-object-detection-api`
  
3. Set the correct path:
  `export PATH=/usr/local/cuda-10.1/bin${PATH:+:${PATH}}`
  
4. `make` the project;

5. Download `yolo.weights` and `tiny-yolo.weights` by running `wget https://pjreddie.com/media/files/yolo.weights` and `wget https://pjreddie.com/media/files/tiny-yolo-voc.weights`;

6. Copy a video file to the video folder, for example, `input.mp4`;

7. In the video folder, run `python video2img.py -i input.mp4` and then `python get_pkllist.py`;

8. Return to root floder and run `python yolo_seqnms.py` to generate output images in `video/output`;

9. If you want to reconstruct a video from these output images, you can go to the video folder and run `python img2video.py -i output`

And you will see detection results in `video/output`

## Reference

This project copies lots of code from [darknet](https://github.com/pjreddie/darknet) , [Seq-NMS](https://github.com/lrghust/Seq-NMS) and  [models](https://github.com/tensorflow/models).
