# Deblur
Despite being somewhat experienced with analog photography, the first role of my new camera (Canon AE-1 Program) came out blurry. I have since replaced the lense and have corrected the issue, but wanted to salvage some pics from the nice day out in the Canadian Rockies. Keen to extend my deep learning knowledge and implementation skills I experimented with a few methods, including DeblurGANv2 (before/after example below) and PULSE. 

                          Before                                                   After 
<p align="center">
  <img src="https://github.com/silkdom/Deblur/blob/master/img/0017_20.jpg?raw=true" alt="Comparison"/>
</p>

## DeblurGANv2

Repo: [https://github.com/TAMU-VITA/DeblurGANv2](https://github.com/TAMU-VITA/DeblurGANv2)  

Testing was undertaken in paperspace by; 
- Cloning the repository to home drive 
- Downloading the pretrained model weights .h5 file (hyperlink broken - copy/paste url instead)
- Specifying the weights path in predict.py  
- Uploading the the pictures to be deblurred
- ```python predict.py IMAGE_NAME.jpg```



This implementation was straightforward minus an annoying error regarding a certificate verification failure. This was caused by an expired secutirity certificate on the website Pytorch hosted the inceptionresnetv2 pretrained model on. The work-around was to fork the repo and subsitute the url for a functioning host. 
Working Repo: [https://github.com/silkdom/Pytorch_pretrained_models](https://github.com/silkdom/Pytorch_pretrained_models)

The architecture is made to handle images of varying demensions, however due to the PatchGAN discriminator using 'patches' of 70x70 deblur success was not uniform accross all sizes attempted. For instance the initial attempt of an image of size 3024x2005 did not provide noticeablke deblur effect. Scaling the images down to 1024x678 proior to DebelurGANv2 provided the best results. Whilst not completely mending my crappy photography the difference is definitely noticeable! 

                          Before                                                   After 
<p align="center">
  <img src="https://github.com/silkdom/Deblur/blob/master/img/0012_25.jpg?raw=true" alt="Comparison"/>
</p>

## PULSE

