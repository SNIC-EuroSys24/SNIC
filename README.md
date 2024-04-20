# SNIC
[EuroSys'24] SmartNIC Security Isolation in the Cloud with S-NIC

## 

First rent cloudlab c6420/c8220 wth ubuntu16 (for using py2.7 in gem5)

Then run the following steps for simulation. It takes around 2 days for each simulation instance; therefore we suggest you run multiple instances. 

```
sudo apt update 
sudo apt install byobu htop build-essential git m4 scons zlib1g zlib1g-dev libprotobuf-dev protobuf-compiler libprotoc-dev libgoogle-perftools-dev  libboost-all-dev pkg-config swig gcc-arm-linux-gnueabi -y

git clone git@github.com:SNIC-EuroSys24/nf_bin.git

cd nf_bin
curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash
sudo apt-get install git-lfs
git lfs install

git lfs pull
make clean && make -j

sudo apt-get install build-essential checkinstall libreadline-gplv2-dev libncursesw5-dev libssl-dev libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev libffi-dev zlib1g-dev -y

cd /opt
sudo wget https://www.python.org/ftp/python/3.8.12/Python-3.8.12.tgz
sudo tar xzf Python-3.8.12.tgz
cd Python-3.8.12
sudo ./configure --enable-optimizations
sudo make altinstall -j 38
cd -

git clone git@github.com:SNIC-EuroSys24/gem5_sim.git && cd gem5_sim
scons build/ARM/gem5.fast -j 38
python3.8 run_sgx_nic_8_16.py
```

Finally, you can find the plot scripts and data for generating figures in the paper at https://github.com/SNIC-EuroSys24/plot


