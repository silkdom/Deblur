# Deblur
I recently upgraded my Pentax K1000 for a Canon AE-1 Program, but unfortunately the first roll of film came out blurry. I have since replaced the lense and have corrected the issue, but wanted to salvage some pics from the nice day out in the Canadian Rockies. Keen to extend my deep learning knowledge and implementation skills I experimented with a few methods, including DeblurGANv2 (before/after example below) and PULSE. 

                          Before                                                   After 
<p align="center">
  <img src="https://github.com/silkdom/Deblur/blob/master/img/0017_20.jpg?raw=true" alt="Comparison"/>
</p>

## DeblurGANv2

Repo: [https://github.com/TAMU-VITA/DeblurGANv2](https://github.com/TAMU-VITA/DeblurGANv2)  

Testing was undertaken in paperspace by; 
- Cloning the repository to home drive 
- Downloading the neccisary packages outlined in requirements.txt
- Downloading the pretrained model weights .h5 file (hyperlink broken - copy/paste url instead)
- Specifying the weights path in predict.py  
- Uploading the the pictures to be deblurred
- ```python predict.py IMAGE_NAME.jpg```



This implementation was straightforward minus an annoying error regarding a certificate verification failure. This was caused by an expired secutirity certificate on the website Pytorch hosted the inceptionresnetv2 pretrained model on. The work-around was to fork the repo and subsitute the url for a functioning host. This in conjunction with other issues regarding incorrect package versions outlined in the requirements.txt prompted me to create a demo Colab notebook for easy testing of the network: [https://github.com/silkdom/Deblur/blob/master/DeblurGANv2_Demo.ipynb](https://github.com/silkdom/Deblur/blob/master/DeblurGANv2_Demo.ipynb)

[![Run in Google Colab](https://img.shields.io/badge/Colab-Run_in_Google_Colab-blue?logo=Google&logoColor=FDBA18)](https://colab.research.google.com/github/silkdom/Deblur/blob/master/DeblurGANv2_Demo.ipynb#scrollTo=fU0aGtD4Nl4W)

The architecture is made to handle images of varying demensions, however due to the PatchGAN discriminator using 'patches' of 70x70 deblur success was not uniform accross all sizes attempted. For instance the initial attempt of an image of size 3024x2005 did not provide noticeablke deblur effect. Scaling the images down to 1024x678 proior to DebelurGANv2 provided the best results. Whilst not completely mending my crappy photography the difference is definitely noticeable! 

                          Before                                                   After 
<p align="center">
  <img src="https://github.com/silkdom/Deblur/blob/master/img/0012_25.jpg?raw=true" alt="Comparison"/>
</p>

## PULSE

Repo: [https://github.com/adamian98/pulse](https://github.com/adamian98/pulse)  

Testing was undertaken in Colab:

[![Run in Google Colab](https://img.shields.io/badge/Colab-Run_in_Google_Colab-blue?logo=Google&logoColor=FDBA18)](https://colab.research.google.com/github/tg-bomze/Face-Depixelizer/blob/master/Face_Depixelizer_Eng.ipynb#scrollTo=fU0aGtD4Nl4W)

Implementation is simple, however Google Quota limits often throw the following errors: "Google Drive Quota Exceeded" or "No such file or directory: '/content/pulse/runs/face.png'". This can be overcome by either;
- Trying again periodically throughout the day (Quota's reset 24hr after the limit is reached)
- Editing the PULSE.py file in the repo
    - Go to the two google drive links and download the respective files 
    - Host the files on your personal Google Drive
    - Get shareable links for the two files and replace their id's in the code

The examples provided in the paper illustrated promise, however initial results quickly proved otherwise (see below). Unfortunately the bias of the Flickr Faces HQ database was inhereted by the model, and the network did not perform well on portraits containing people not with caucasian descent. Little experimentation was done after the initial results. 

                          Before                                                   After 
<p align="center">
  <img src="https://github.com/silkdom/Deblur/blob/master/img/comb1.jpg?raw=true" alt="Comparison"/>
</p>

