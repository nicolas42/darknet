Run yolov3 on videos without opencv

This is a fork of http://github.com/pjreddie/darknet

# Install

## Make with CPU
make
gcc darknet_ffmpeg.c -Iinclude libdarknet.a -o darknet_ffmpeg -pthread -lm

## get video
aws s3 cp s3://bitwise-nick/videos/test.mp4 .

## Run Yolov3 tiny
aws s3 cp s3://bitwise-nick/weights/yolov3-tiny.weights .
aws s3 cp s3://bitwise-nick/weights/yolov3-tiny.cfg .
./darknet_ffmpeg detector test cfg/coco.data yolov3-tiny.cfg yolov3-tiny.weights test.mp4


## Make with GPU
make
gcc -Iinclude/ -Isrc/ -DGPU -I/usr/local/cuda/include/ -DCUDNN  -Wall -Wno-unused-result -Wno-unknown-pragmas -Wfatal-errors -fPIC -Ofast -DGPU -DCUDNN \
darknet_ffmpeg.c libdarknet.a -o darknet_ffmpeg -lm -pthread  -L/usr/local/cuda/lib64 -lcuda -lcudart -lcublas -lcurand -lcudnn -lstdc++  libdarknet.a


## Run Yolov3
aws s3 cp s3://bitwise-nick/weights/yolov3.weights .
aws s3 cp s3://bitwise-nick/weights/yolov3.cfg .
./darknet_ffmpeg detector test cfg/coco.data yolov3.cfg yolov3.weights test.mp4
