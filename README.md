# Fast Face Detector (FFD)
The fast face detector is based on the work [Aggregate channel features for multi-view face detection](https://arxiv.org/abs/1407.4023) proposed by Bin Yang, Junjie Yan, Zhen Lei and Stan Z. Li. My version extends the aforementioned one by adding a new channel: the integral image. This innovation makes the detector very robust with respect to the Viola Jones (VJ) detector. 
We tested FFD and VJ on 3547 images by obtaining the following results:

| **Detector** | **True Positive** | **False Positive** | **No Detection** | **Precision** |
|--------------|:-------------------:|:--------------------:|:------------------:|:---------------:|
| FFD | 3059 | 488 | 0 | 86.24% |
| VJ | 2417 | 896 | 344 | 68.14% |


## REQUIREMENTS
* OpenCV
* OpenMP
* SSE
* Boost

## How to build

FPD works under Linux and Mac Os environments. I recommend a so-called out of source build which can be achieved by the following command sequence:

* mkdir build
* cd build
* cmake ../
* make -j<number-of-cores+1>

## How to use

###MATLAB - Training

1) Compile the cpp files by launching:
```matlab
compile_mex_files.m;
```

2) Create a folder _train_ and three subfolders, namely:
* posGt: containing one txt file for each positive image. Each file contains the coordinates of each face in the image in the following format: #x #y #w #h
* pos_jpg: containing the positive samples
* neg_jpg: containing the negative 


3) Launch the training file:
```matlab
train;
```

###C++ - Detection
Go to the bin diretory and launch the program with the following command:
```bash
./ffd ../detector/detector.xml /path/to/the/image.jpg
```

The detector is already trained with the complete [AFW dataset](https://www.ics.uci.edu/~xzhu/face/). So, you can directly use the xml file inside the _detector_ folder.
