# scuffEM-tutorial
Experiments to make running scuff-em solver what is BEM solver to analyze electromagnetic structures

Xubuntu Virtual Machine - scuff-em installation
-----------------------------------------------
- installation url: 

  - install dependencies:
      - since it's 10 year old repository python-dev is now python3-dev, this takes 400MB
          > sudo apt-get install libopenblas-dev libhdf5-openmpi-dev python3-dev python3-scipy gmsh

- these dependencies were tested on my ubuntu virtual machine but they are needed to be installed
    > sudo apt install -y autoconf automake libtool make g++ gfortran libhdf5-dev liblapack-dev libblas-dev libopenmpi-dev python3-dev pkg-config
 
    > sudo apt install -y libhdf5-dev liblapack-dev libblas-dev libopenmpi-dev python3-dev pkg-config
 
	> sudo apt install swig

- build steps made in ~/Documents/:
	> git clone https://github.com/HomerReid/scuff-em.git

	> cd scuff-em
	
	- this is from webpage installation instructions, but wasn't running as it cannot find hdf5:
		> sh autogen.sh --prefix=${HOME}/Documents/scuff-em-installation
	- or try this:
		> sh autogen.sh --prefix=${HOME}/Documents/scuff-em-installation --without-hdf5
		
	- after autogen.sh fail run this:
	```	
          ./configure \
		  --prefix=${HOME}/Documents/scuff-em-installation \
		  --enable-maintainer-mode \
		  CPPFLAGS="$(pkg-config --cflags hdf5-serial)" \
		  LDFLAGS="$(pkg-config --libs hdf5-serial)" \
		  CFLAGS="-g -O2 -Wno-implicit-function-declaration"
 	```

	- claudeai, because there are some errors:
		> sed -i '/#include <stdio.h>/a #include <stdlib.h>' /home/johndoe/Documents/scuff-em/libs/libSpherical/machcon.c

		> make -j 6 install
	
	- add to PATH:
		> export PATH=${PATH}:~/Documents/scuff-em-installation/bin

    - permanently set PATH for user:
        > echo 'export PATH=${PATH}:~/Documents/scuff-em-installation/bin' >> ~/.bashrc && source ~/.bashrc
