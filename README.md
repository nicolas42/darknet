This is a fork of Joseph Redmon's excellent yolov3 software for object detection.

It uses ffmpeg to pipe mp4 video in and out so it doesn't need opencv3.

The demo uses example/mydetector.c

files for demo available here for me
https://s3.console.aws.amazon.com/s3/buckets/nschmidt/?region=ap-southeast-2&tab=overview

or here for everyone else
https://drive.google.com/open?id=0B3NaVR72FYQcWUFSUVhKWE5UMVU
wget https://pjreddie.com/media/files/yolov3.weights


make

gcc examples/mydetector.c -Iinclude libdarknet.a -o mydarknet -pthread -lm  ; \
./mydarknet detector test cfg/coco.data cfg/yolov3.cfg yolov3.weights teapot.mp4

gcc -Iinclude/ -Isrc/ -DGPU -I/usr/local/cuda/include/ -DCUDNN  -Wall -Wno-unused-result -Wno-unknown-pragmas -Wfatal-errors -fPIC -Ofast -DGPU -DCUDNN \
examples/mydetector.c libdarknet.a -o mydarknet -lm -pthread  -L/usr/local/cuda/lib64 -lcuda -lcudart -lcublas -lcurand -lcudnn -lstdc++  libdarknet.a ; \
./mydarknet detector test cfg/coco.data cfg/yolov3.cfg yolov3.weights teapot.mp4


