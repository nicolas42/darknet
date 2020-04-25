files available from https://s3.console.aws.amazon.com/s3/buckets/nschmidt/?region=ap-southeast-2&tab=overview

or from
https://drive.google.com/open?id=0B3NaVR72FYQcWUFSUVhKWE5UMVU
wget https://pjreddie.com/media/files/yolov3.weights


make

(macos)
clang libdarknet.a examples/mydetector.c -Iinclude -o mydarknet
(ubuntu)
clang examples/mydetector.c -Iinclude libdarknet.a -o mydarknet -pthread -lm


./mydarknet detector test cfg/coco.data cfg/yolov3.cfg yolov3.weights teapot.mp4
