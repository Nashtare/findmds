CXXFLAGS= -Wall -Wextra -I boost_1_64_0 -march=native -std=gnu++0x -O3 -g -fopenmp -gstabs+ -g3
#CXXFLAGS+= -fsanitize=address
CXXFLAGS+= -I oneTBB-2021.7.0/include -L oneTBB-2021.7.0/build/gnu_9.4_cxx11_64_relwithdebinfo/
LDLIBS=-ltbb
LDFLAGS=-Wl,-rpath=oneTBB-2021.7.0/build/gnu_9.4_cxx11_64_relwithdebinfo/


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
	cd oneTBB-2021.7.0 && mkdir -p build && cd build && cmake .. && cmake --build . -j && cmake --install .

clean:
	rm -fr oneTBB-2021.7.0 boost_1_64_0 find_mds

.PHONY: all clean
