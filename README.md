# ASL-recognition

A classification model using  Resnet18 that was trained on over 20,000 files of images of the different signs. Original Dataset can be accesed here (You do need an account to access it):https://www.kaggle.com/datasets/grassknoted/asl-alphabet and https://www.kaggle.com/datasets/debashishsau/aslamerican-sign-language-aplhabet-dataset?resource=download


Make sure you have installed jetson-interfence and Docker Image from : https://github.com/dusty-nv/jetson-inference  (This will be covered in the command list)

# What is the Jetson Nano:
![16271-NVIDIA_Jetson_Nano_Developer_Kit__V3_-01](https://github.com/ArjunDhavse/ASL-recognition/assets/169238921/32a5c718-5efa-47d7-a72e-068fdbccda4e)


Released in 2019, the Jetson Nano Developer Kit is a powerful and affordable platform designed to democratize AI development for enthusiasts, educators, and researchers. 

**Technical Specifications**

* Available in 2GB and 4GB LPDDR4 memory configurations
* Powered by a NVIDIA Maxwell™ architecture-based SoC
* Features a micro SD card slot for storage and a Gigabit Ethernet port for networking
* Supports multiple high-resolution cameras through MIPI CSI-2 ports

**Headless and Headed Access**

The Jetson Nano can be accessed in two primary configurations:

* **Headless:** Ideal for embedded applications, headless mode provides a command-line interface accessible via SSH. SSH connection requires a wifi adapter or an ethernet cable.(More information can be found in the playlist linked below)
* **Headed:** Enables a graphical desktop environment using Ubuntu for development and visualization tasks (Requires an HDMI cable and has a graphical user interface).

# How to use it: 
The commands below are what will be required to run the model in the repository. This will be in a linux terminal and if you would like a refresher on the basic linux commands you can access it here: https://www.geeksforgeeks.org/basic-linux-commands/.
  1) Clone the jetson-inference project using this command (Downloading the repository from github onto your Jetson-Nano)


    git clone --recursive https://github.com/dusty-nv/jetson-inference


      

      
     
  2)  Move into your new jetson-inference folder


     cd jetson-infrence



  3) Update the modules within the folder
```
  git submodule update --init
```
  4) In order to install the necessary python packages, run this command. You will be prompted to enter your password.
  ```
      sudo apt-get install libpython3-dev python3-numpy
   ```
  5) If you did not see pytorch installation by running the previous command, run this command to install pytorch.
  ```
     ./install-pytorch.sh
   ```
 6) change directory to python/training/classification/models and run the command
    
```
    git clone --recursive https://github.com/ArjunDhavse/ASL-recognition
  ```

 7) You may get an error later while in the docker saying you're out of memory. You can ensure your system overcommits memory which allows it to have more memory for the task by running this now. Run this in your terminal when you're in your jetson-inference directory:(If you want to get back to Jetson infrence dorectory, run the cd ../ command until the terminal only shows the jetson infrence directory)



 ```
 echo 1 | sudo tee /proc/sys/vm/overcommit_memory  
 ```


8) Change the directory to python/training/classification/models and run the command
 'ls models/A.S.L_Resnet18Model_ArjunDhavse_2024_/' to make sure that the model is on the nano. You should see a file called resnet18.onnx.

9) You have two choices now, to run the model to recognise real-time hand movements via a webcam or to use the model to recognise an image

a) For camera(Must be connected to Jeston Nano via one of the USB ports)
     ```
       imagenet.py --model=models/A.S.L_Resnet18Model_ArjunDhavse_2024_/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=models/labels.txt dev/video0 output.mp4
     ```
 If you get an error, try switching 'dev/video0' to 'dev/video1'

b) For image(Must be present in the Jetson-Nano)
      ```
       imagenet.py --model=models/A.S.L_Resnet18Model_ArjunDhavse_2024_/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=models/labels.txt [INSERT PATH OF IMAGE HERE AND REMOVE BRACES] output.jpg
       ```

After all this, you should get an output depending on what you chose in step 9 in the models folder. That is it!
 

# Read More:
You can access the offical videos on how to use the jetson-nano and Resnet18 model here as well as how to install pytorch and run the docker sequence: https://youtu.be/sN6aT9TpltU 
It is a part of a [larger series](https://www.youtube.com/playlist?list=PL5B692fm6--uQRRDTPsJDp4o0xbzkoyf8) that completly explains how to use the Jetson nano and is crucial to watch if you want to create your own model. 

Thank You!


![images](https://github.com/ArjunDhavse/ASL-recognition/assets/169238921/bf93405f-ea8d-4fba-b702-082ed632271a)
