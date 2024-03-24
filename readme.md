# Framework For Misbehavior Detection (F2MD)🦟

This project aims to recreate within a simulation all the elements that form the chain of misbehavior detection. 

> * Omnet++工作目录
> * sumo1.8+Omnetpp5.6+veins5.2

# install
```

export DEBIAN_FRONTEND=noninteractive 
sudo apt-get update
sudo apt-get install -y git rapidjson-dev net-tools gnuplot python3 python3-dev python3-tk 
#python-is-python3



# set INET variables in .bashrc/.zshrc and source .bashrc/.zshrc
if [ -d "/home/jeremy/dev/f2md_omnet/inet" ] && [[ ":$PATH:" != *":/home/jeremy/dev/f2md_omnet/inet:"* ]]; then
    export INET_ROOT="/home/jeremy/dev/f2md_omnet/inet"
    export INET_NED_PATH="$INET_ROOT/src:$INET_ROOT/tutorials:$INET_ROOT/showcases:$INET_ROOT/examples"
    export INET_OMNETPP_OPTIONS="-n $INET_NED_PATH --image-path=$INET_ROOT/images"
    export INET_GDB_OPTIONS="-quiet -ex run --args"
    export INET_VALGRIND_OPTIONS="-v --tool=memcheck --leak-check=yes --show-reachable=no --leak-resolution=high --num-callers=40 --freelist-vol=4000000"
fi
```
# build

```

cd f2md_omnet/inet
make makefiles && make -j$(nproc) WITH_OSGEARTH=no MODE=debug && make -j$(nproc) MODE=release all

# Build veins
cd f2md_omnet/veins-f2md
./configure && make -j$(nproc) MODE=release all

# Build veins_inet3
cd f2md_omnet/veins-f2md/subprojects/veins_inet3
./configure && make -j$(nproc) MODE=release all

# Build simulte
cd f2md_omnet/simulte-f2md
make makefiles && make -j$(nproc) MODE=release all
```


# run
1. Launch the SUMO TraCI daemon
```
$ ./launchSumoTraciDaemon
```
2. Run a simulation scenario
```
$ ./runScenario
```
3. Visualise the output
```
$ cd f2md-results && ./plotScenario
```

# Make Top Repository
```
git submodule add -b main git@github.com:jeremyHua1931/simulte-f2md.git

git submodule add -b main git@github.com:jeremyHua1931/veins-f2md.git

git submodule add -b inet-v3.6.6 git@github.com:jeremyHua1931/inet.git
```

# tips
```
# sumo and omnet++ environment path in .zshrc

# set SUMO_HOME variable
if [ -d "/home/jeremy/programs/sumo-1.8.0" ] && [[ ":$PATH:" != *":/home/jeremy/programs/sumo-1.8.0/bin:"* ]]; then
    export SUMO_HOME="/home/jeremy/programs/sumo-1.8.0"
    PATH="/home/jeremy/programs/sumo-1.8.0/bin:$PATH"
fi

# set PATH so it includes SUMO
if [ -d "/home/jeremy/programs/sumo-1.8.0/bin" ] && [[ ":$PATH:" != *":/home/jeremy/programs/sumo-1.8.0/bin:"* ]]; then
    PATH="/home/jeremy/programs/sumo-1.8.0/bin:$PATH"
fi


# set PATH so it includes Omnet++
if [ -d "/home/jeremy/programs/omnetpp-5.6.2" ] && [[ ":$PATH:" != *":/home/jeremy/programs/omnetpp-5.6.2/bin:"* ]]; then
    PATH="/home/jeremy/programs/omnetpp-5.6.2/bin:$PATH"
fi

source /etc/profile.d/proxy.sh


# set INET variables
if [ -d "/home/jeremy/dev/f2md_omnet/inet" ] && [[ ":$PATH:" != *":/home/jeremy/dev/f2md_omnet/inet:"* ]]; then
    export INET_ROOT="/home/jeremy/dev/f2md_omnet/inet"
    export INET_NED_PATH="$INET_ROOT/src:$INET_ROOT/tutorials:$INET_ROOT/showcases:$INET_ROOT/examples"
    export INET_OMNETPP_OPTIONS="-n $INET_NED_PATH --image-path=$INET_ROOT/images"
    export INET_GDB_OPTIONS="-quiet -ex run --args"
    export INET_VALGRIND_OPTIONS="-v --tool=memcheck --leak-check=yes --show-reachable=no --leak-resolution=high --num-callers=40 --freelist-vol=4000000"
fi%

# source .zshrc
# same to .bashrc
```