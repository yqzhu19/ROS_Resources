- catkin_make: in root of ws, to build any packages in ~/catkin_ws/src.
- 上述等于
```
$ cd ~/catkin_ws
$ cd src
$ catkin_init_workspace
$ cd ..
$ mkdir build
$ cd build
$ cmake ../src -DCMAKE_INSTALL_PREFIX=../install -DCATKIN_DEVEL_PREFIX=../devel
$ make
```

-[http://wiki.ros.org/catkin/commands/catkin_make]
