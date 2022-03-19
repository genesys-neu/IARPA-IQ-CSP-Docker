# IARPA-IQ-CSP-Docker

This Docker container (6.1 GB) was built to run the "IARPA-IQ-API" and "IARPA-IQ-CSP-Fusion" repositories for anomaly detection in LTE signals without the need to manually install specific package versions. For more instructions on how to run the "IARPA-IQ-API" Docker container or interface, visit [here.](https://github.com/genesys-neu/IARPA-IQ-Docker)

Please send all questions to either gu.je or d.roy {@northeastern.edu}, thanks!

# Contents
* [Pre-requisites](#pre-requisites)
* [Instructions for Users](#instructions-for-users)
  * [Running the CSP API](#running-the-csp-api)
  * [Acceptable Input File Format](#acceptable-input-file-format)
* [Appendix](#appendix)

## Pre-requisites
Install Docker engine/app for your specific operating system [here.](https://docs.docker.com/engine/install/)  
Install the IARPA-IQ-CSP-Fusion Docker container [here.](https://drive.google.com/file/d/1aB3Prg46CvBYRVnVaSVpbc0bgE1hVda9/view?usp=sharing)

## Instructions for Users

To load the Docker container, go to the directory where the container is and use the following command:
~~~
sudo cat iarpa-iq-csp-api.tar | sudo docker import - iarpa-iq-csp-api
~~~
To verify that the container was loaded successfully, do:
~~~
sudo docker images
~~~
which should display something like the following, with the ```iarpa-iq-csp-api``` image:
~~~
REPOSITORY         TAG       IMAGE ID       CREATED        SIZE
iarpa-iq-csp-api   latest    d71ed07d1bc6   36 hours ago   4.2GB
~~~

### Running the CSP API  
This image comes with folders and folder paths hard-coded for convenience. To run the image with the desired dataset, run
~~~
sudo docker run -v \
<dataset_absolute_local_path>:\
/home/IARPA-CSP-main/test/CSP iarpa-iq-csp-api \
/home/IARPA-CSP-main/./run_ML_code.sh
~~~
where ```/home/IARPA-CSP-main/test/CSP``` is the ```<dataset_absolute_image_path>```. An example of this command is  
```sudo docker run -v /home/jgu1/Downloads/CSP:/home/IARPA-CSP-main/test/CSP iarpa-iq-csp-api /home/IARPA-CSP-main/./run_ML_code.sh```.

### Acceptable Input File Format
The code predicts anomalies from the non-conjugate cycle frequency features. The model is trained on the 4th column of the non-conjugate CSP features; it skips the conjugate features; hence, the input files must have '.NC' extension. Any file with other extension, e.g., '.C' will be skipped. The folder 'CSP_samples', containing a variety of .NC and .C files for combined LTE+DSSS and only LTE signals has been provided for your testing convenience.

For the input dimensions of each .NC file:
* The number of rows can be variable (an empty file with zero rows is accepted as well, but the prediction could be wrong).
* The number of columns must be 4 following the sequence of F, A, C, S.

### Example Output:
~~~
The prediction from CSP features in OnlyLTE_frame_120_131072_3.NC is: OnlyLTE
Total time of execution for OnlyLTE_frame_120_131072_3.NC is : 0.002008676528930664 seconds.

The prediction from CSP features in Combined_LTE_DSSS_frame_127_262144_4.NC is: Combined_LTE_DSSS
Total time of execution for Combined_LTE_DSSS_frame_127_262144_4.NC is : 0.002009153366088867 seconds.
~~~

[Back to Contents](#contents)

## Appendix
The packages and their respective versions in this container are:
~~~
Python 3.8.10
pip3 20.0.3
TensorFlow/Keras 2.8
torch 1.11.0
torchvision 0.12.0
torchaudio 0.11.0
Opencv-python (cv2) 4.4.5
Pillow (PIL) 9.0.1
tqdm 4.62.3
glob2 0.7
Setuptools 60.9.3
pandas 1.4.1
~~~
 
[Back to Contents](#contents)
