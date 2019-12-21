```
graph TD
A[Camera, Real Time]-->|USB or CAN| B[Hardware/Software Interface e.g. opendlv_driver_camera_zed]
B-->C[yuv]
B-->D[RGB]
C-->E[video h264 encoder]
D-->F[YOLO Machine Learning]
D-->G[Cone Tracker]
F-->G
F-->H[Path planning algorithm]
G-->H
H-->I[CAN]
E-->|Image Reading| J[Recording]
```
### yuv和RGB的区别
RGB的bit占用计算是w\*h\*3, 而yuv是灰度,只需要1.5来表示一个像素. Camera在高速移动的情况下会blurry,但是问题不大

### Time Stamp
time stamp最好是设在camera里,但有可能占用can bus的线程那样就不好了,所以可以在软件里面设置时间.接收到信号的一瞬间计时,到下一圈的用时.可以估算出来camera到软件的时间,但是不精确啊.咋办呢?

### Kalmen Filter
更新的频率不一样,cone tracker的更新频率明显是要比yolo做机器学习快不少的.yolo相当于measurement,cone tracker相当于estimate.直观的感受就是猜的比测的快.

### 各个部分之间的通信方式
#### UDP multicast
mulicast和broadcast区别就是multicast可以发给所有.UDP multicast可以实现局域网内部电脑之间的数据传递,问题是数据大小有限制
#### Shared Memory
通过一个进程在使用memory就把这个shared memory lock起来的方式避免内存之间的冲突但同时会带来一些问题.
对于大的文件使用shared memory,对于APU与host直接使用UDP multicast.


```
graph TD
A[Opendlv]-->B[Docker engine]
B-->C[OS]
C-->D[HW]
E[Car HW]-->A
E-->B
E-->C
E-->D
F[APU]-->E
```
