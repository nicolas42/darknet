files available from https://s3.console.aws.amazon.com/s3/buckets/nschmidt/?region=ap-southeast-2&tab=overview

or from
https://drive.google.com/open?id=0B3NaVR72FYQcWUFSUVhKWE5UMVU
wget https://pjreddie.com/media/files/yolov3.weights


# Make

make

(macos)
clang libdarknet.a examples/mydetector.c -Iinclude -o mydarknet

(ubuntu no gpu)
gcc examples/mydetector.c -Iinclude libdarknet.a -o mydarknet -pthread -lm

(ubuntu with gpu and cuda)
gcc -Iinclude/ -Isrc/ -DGPU -I/usr/local/cuda/include/ -DCUDNN  -Wall -Wno-unused-result -Wno-unknown-pragmas -Wfatal-errors -fPIC -Ofast -DGPU -DCUDNN \
examples/mydetector.c libdarknet.a -o mydarknet -lm -pthread  -L/usr/local/cuda/lib64 -lcuda -lcudart -lcublas -lcurand -lcudnn -lstdc++  libdarknet.a


# Run

./mydarknet detector test cfg/coco.data cfg/yolov3.cfg yolov3.weights teapot.mp4


# Notes

gcc -Iinclude/ -Isrc/ -DGPU -I/usr/local/cuda/include/ -DCUDNN  -Wall -Wno-unused-result -Wno-unknown-pragmas -Wfatal-errors -fPIC -Ofast -DGPU -DCUDNN examples/mydetector.c libdarknet.a -pthread -lm

nvcc  -gencode arch=compute_30,code=sm_30 -gencode arch=compute_35,code=sm_35 -gencode arch=compute_50,code=[sm_50,compute_50] -gencode arch=compute_52,code=[sm_52,compute_52] \
-Iinclude/ -Isrc/ -DGPU -I/usr/local/cuda/include/ -DCUDNN  \
--compiler-options "-Wall -Wno-unused-result -Wno-unknown-pragmas -Wfatal-errors -fPIC -Ofast -DGPU -DCUDNN" -c ./src/convolutional_kernels.cu -o obj/convolutional_kernels.o


