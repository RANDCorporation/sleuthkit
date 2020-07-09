###Ubuntu 16.04 installation:

This version of The Sleuthkit is modified to work with RAND's DFORC2 digital forensics suite.
#####Install dependencies:
```
sudo apt-get install wget git git-svn build-essential libssl-dev libbz2-dev libz-dev ant automake autoconf libtool vim python-dev uuid-dev libfuse-dev libcppunit-dev libafflib-dev libpq-dev dc3dd
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
export JDK_HOME=/usr
```

The below instructions should be run form a workspace directory, somewhere within your home folder, and not inside this repository.
#####Install libewf:
```
wget https://raw.github.com/libyal/legacy/master/libewf/libewf-20140427.tar.gz
tar xvfz libewf-20140427.tar.gz
cd libewf-20140427
./configure --enable-python --enable-verbose-output --enable-debug-output --prefix=$HOME/tsk
make
sudo make install
export LIBEWF_HOME=$HOME/tsk
```

#####Install TSK:
```
git clone git@gitlab.com:RANDCorporation/sleuthkit.git
cd sleuthkit
./bootstrap
./configure --prefix=$HOME/tsk --with-libewf=$HOME/tsk --enable-java
make
make install

mkdir -p ~/tsk/bindings/java/dist
cp -v ~/tsk/share/java/Tsk_DataModel.jar ~/tsk/share/java/Tsk_DataModel_PostgreSQL.jar
cp -v ~/tsk/share/java/*.jar ~/tsk/bindings/java/dist
mkdir -p ~/tsk/bindings/java/lib
cp -v bindings/java/lib/*.jar ~/tsk/bindings/java/lib/
export TSK_HOME=$HOME/tsk
```