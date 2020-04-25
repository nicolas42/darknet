make
clang libdarknet.a examples/mydetector.c -Iinclude -o mydarknet
./mydarknet detector test cfg/coco.data cfg/yolov3.cfg yolov3.weights teapot.mp4
