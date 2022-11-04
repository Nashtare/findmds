CXXFLAGS= -Wall -Wextra -I boost_1_64_0 -march=native -std=gnu++0x -O3 -g -fopenmp -gstabs+ -g3
#CXXFLAGS+= -fsanitize=address
CXXFLAGS+= -I tbb-2021.7.0/include -L tbb-2021.7.0/build/linux_release/
LDLIBS=-ltbb
LDFLAGS=-Wl,-rpath=tbb-2021.7.0/build/linux_release/


all: boost_1_64_0 tbb-2021_7_0 find_mds

boost_1_64_0:
	echo -e "\e[31;1mDownloading and unpacking Boost 1.64.\nThis will take a few minutes...\e[0m"
	wget -c https://boostorg.jfrog.io/artifactory/main/release/1.64.0/source/boost_1_64_0.tar.bz2
	tar xf boost_1_64_0.tar.bz2

tbb-2021_7_0:
	echo -e "\e[31;1mDownloading and compiling TBB 2021_U7.\nThis will take a few minutes...\e[0m"
	wget -c https://github.com/oneapi-src/oneTBB/archive/refs/tags/v2021.7.0.tar.gz
	tar xf v2021.7.0.tar.gz
	patch -d oneTBB-2021.7.0 -p1 < TBB_increase_memory.patch
	cd oneTBB-2021.7.0 && mkdir build && cd build && cmake .. && cmake --build . && cmake --install .

clean:
	rm -fr oneTBB-2021.7.0 boost_1_64_0 find_mds

.PHONY: all clean
