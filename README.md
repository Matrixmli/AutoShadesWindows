# Project Name
Automated Windows and Window Shades

My project uses machine learning to determine whether it is day or night outside. It also asks you if you want your shades or windows to be opened and closed. With this information, it will automatically make the correct choices based on your needs.

Original Image:
![image](https://github.com/Matrixmli/AutoShadesWindows/assets/78279532/0adf8b5f-52c0-413e-9e41-9b224d46470f)

Result from AI:
![image](https://github.com/Matrixmli/AutoShadesWindows/assets/78279532/9d951e30-6b16-499f-8ce1-006b678805b7)

## The Algorithm
My algorithm detects if it is night or day. I gave it many different images to train. The AI would find patterns and learn if a picture was taken at night or during the day. If the AI determines that it is night time, it will close windows and pull down shades. If the AI determines that it is day time, it will open the windows and pull down shades. Below, there are a few images that show how confindent my program is with machine learning.


## Warning

**This code only works with Jetson Nano**

You can buy one from amazon using [this](https://www.amazon.com/NVIDIA-Jetson-Nano-Developer-945-13450-0000-100/dp/B084DSDDLT/ref=asc_df_B084DSDDLT/?tag=hyprod-20&linkCode=df0&hvadid=416652333997&hvpos=&hvnetw=g&hvrand=2605406615134929580&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=1018145&hvtargid=pla-893453703291&psc=1&tag=&ref=&adgrpid=100759324064&hvpone=&hvptwo=&hvadid=416652333997&hvpos=&hvnetw=g&hvrand=2605406615134929580&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=1018145&hvtargid=pla-893453703291) link

## Running this project

**downloading files**

1) download the jetson_inference file [here](https://github.com/dusty-nv/jetson-inference.git)
2) Run this command in the terminal to acquire the dataset `wget https://www.dropbox.com/scl/fi/29l5hwfxe8rlrwy4kkc66/night_day.zip?rlkey=dhamsibh48gzyjcfz5702390k`
3) sudo apt-get install unzip
4) unzip [file name]
5) unzip the downloaded file and place the file in /home/nvidia/jetson-inference/python/training/classification/data
6) download train.py and models
7) place both in /home/nvidia/jetson-inference/python/training/classification

**running AI**

1) open putty and enter your jetson nano's IP
2) run `cd jetson-inference` in the terminal (this goes into the jetson inference directory)
4) run `./docker/run.sh` in the terminal (this opens the docker which provides many useful containers)
5) run `cd python/training/classification` (this changes the directories)
6) run `python3 train.py --model-dir=models/night_day data/night_day` (this command will take time to finish)
7) run `python3 onnx_export.py --model-dir=models/night_day` (this makes it possible to test images)
8) hit Ctl + D (this exits out of the docker)
9) run `NET=models/night_day` (this sets variables)
10) run `DATASET=data/night_day` (this sets variables)
11) run `cd python/training/classification` (this changes the directories)
12) run `imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/day/400.jpg day.jpg` (this runs an image through the AI)


