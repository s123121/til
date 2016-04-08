Node is not the default package to install in ec2 centos. So it is a bit harder to install inside ec2 instance. The best way to install lastest update node version is the following
```
sudo yum install openssl openssl-devel
sudo yum groupinstall "Development Tools"

sudo yum install git-core
git clone https://github.com/nodejs/node

cd node
./configure
make

sudo make install
node -v
```
