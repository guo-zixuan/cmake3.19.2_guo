# mqtt_install
#!/bin/bash

# 记得这个脚本要sudo运行

sudo apt-get install mosquitto mosquitto-clients python3-pip -y

pip3 install paho-mqtt

sudo apt-get install build-essential gcc make cmake cmake-gui cmake-curses-gui -y

sudo apt-get install libssl-dev -y

sudo apt-get install doxygen graphviz -y

git clone https://github.com/eclipse/paho.mqtt.c.git /src/mqtt/paho.mqtt.c


cd /src/mqtt/paho.mqtt.c
git checkout v1.3.8

cmake -Bbuild -H. -DPAHO_ENABLE_TESTING=OFF -DPAHO_BUILD_STATIC=ON \
    -DPAHO_WITH_SSL=ON -DPAHO_HIGH_PERFORMANCE=ON

sudo cmake --build build/ --target install

sudo ldconfig

cd /src

git clone https://github.com/eclipse/paho.mqtt.cpp /src/mqtt/paho.mqtt.cpp

cd /src/mqtt/paho.mqtt.cpp

cmake -Bbuild -H. -DPAHO_BUILD_STATIC=ON \
    -DPAHO_BUILD_DOCUMENTATION=TRUE -DPAHO_BUILD_SAMPLES=TRUE

sudo cmake --build build/ --target install

sudo ldconfig
升级Cmake 和G++ GCC
sudo apt-get install -y build-essential libssl-dev

cd /src/mqtt/cmake
git clone https://github.com/guo-zixuan/cmake3.19.2_guo.git /src/mqtt/cmake

tar -zxvf cmake-3.19.2.tar.gz

cd cmake-3.19.2/

./bootstrap  # change /usr/local to /usr/local/cmake/cmake-3.19.2
make
sudo make install
hash -r
export PATH=/usr/local/cmake/cmake-3.19.2/bin:$PATH


sudo add-apt-repository ppa:ubuntu-toolchain-r/test -y
sudo apt update
sudo apt install gcc-9 -y
sudo apt install g++-9 -y

sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 100
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-9 100

sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 50
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-7 50

sudo update-alternatives --config gcc
sudo update-alternatives --config g++


cd /src

git clone https://github.com/guo-zixuan/mqtt_client.git -b onboard_version /src/mqtt_ws/src/mqtt_client

cd /src/mqtt_ws

catkin_make

sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 50   
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-9 50

sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 100
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-7 100

sudo update-alternatives --config gcc
sudo update-alternatives --config g++

