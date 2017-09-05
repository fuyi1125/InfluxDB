### 1.Define the local system with raspi-config for example.
### 2.Install packages needed for compiling
`apt-get install gawk mercurial bzr protobuf-compiler flex bison valgrind g++ make autoconf libtool libz-dev libbz2-dev curl rpm build-essential git wget libgflags-dev`
***
### 3.Install GVM
`bash < <(curl -s -S -L https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer)`
***
### 4.Initialize the GVM environments variablessource /root/.gvm/scripts/gvm
`source /root/.gvm/scripts/gvm`
***
### 5.Install Go 1.3gvm install go1.3
`gvm install go1.3`
***
### 6.Set default version 1.3 GBgvm use go1.3 --default
`gvm install go1.3`
***
### 7.Installer les plugins suivantsgo get code.google.com/p/goprotobuf/{proto,protoc-gen-go}
`go get code.google.com/p/goprotobuf/{proto,protoc-gen-go}`
***
### 8.Installer GCC 4.9:
#### 1.Edit the file/etc/apt/sources.list by adding following content
`deb http://mirrordirector.raspbian.org/raspbian/ wheezy main contrib non-free rpi`
`deb http://archive.raspbian.org/raspbian wheezy main contrib non-free rpi`
`# Source repository to add`
`deb-src http://archive.raspbian.org/raspbian wheezy main contrib non-free rpi`
`deb http://mirrordirector.raspbian.org/raspbian/ jessie main contrib non-free rpi`
`deb http://archive.raspbian.org/raspbian jessie main contrib non-free rpi`
`# Source repository to add`
`deb-src http://archive.raspbian.org/raspbian jessie main contrib non-free rpi`
#### 2.Edit the /etc/apt/preferences file and insert the following contentPackage: 
`Pin: release n=wheezy`
`Pin-Priority: 900`
`Package: *`
`Pin: release n=jessie`
`Pin-Priority: 300`
`Package: *`
`Pin: release o=Raspbian`
`Pin-Priority: -10`
#### 3.Update the packages
`apt-get update`
#### 4.Install gcc and g++
`apt-get install -t jessie gcc g++`
#### Source : http://somewideopenspace.wordpress.com/2014/02/28/gcc-4-8-on-raspberry-pi-wheezy/
***
### 9.Increase the size of the filesystem mounted on /tmp by adding the following line to /etc/fstab
`tmpfs /tmp tmpfs defaults,noatime,nosuid,size=400m 0 0`
***
### 10.Restartreboot
`reboot`
***
### 11.Prepare the structure for the compilation
`mkdir gocodez export GOPATH=$HOME/gocodez mkdir-p $GOPATH/src/github.com/influxdb cd $GOPATH/src/github.com/influxdb`
***
### 12.Download the latest version of the sources
`wget http://S3.amazonaws.com/influxdb/influxdb-latest.src.tar.gz`
***
### 13.Unpack the archive and move the sources
`mkdir influxdb cd influxdb tar zxvf../influxdb-latest.src.tar.gz cp-R src/github.com/* $GOPATH/src/github.com/cd $GOPATH/src/github.com/influxdb/influxdb`
***
### 14.Start the configuration
`./configure`
### 15.Edit the file Makefile to make architecture arm. This is the line 16 file. Replace :
`arch   = amd64`
by
`arch   = arm`
***
### 16.Edit the file Makefile to disable RocksDB on line 112. Replace :
`rocksdb = yes`
by
`rocksdb = no`
***
### 17.Edit the file Makefile to comment the line 233. Replace :
`$(GO) build -o benchmark-storage $(GO_BUILD_OPTIONS) github.com/influxdb/influxdb/tools/benchmark-storage`
by
`#$(GO) build -o benchmark-storage $(GO_BUILD_OPTIONS) github.com/influxdb/influxdb/tools/benchmark-storage`
***
### 18.Start the compilation
`make build`
***
### 19.You can now install InfluxDB
`make install`
