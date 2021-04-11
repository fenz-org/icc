# Adtapted from Intel Dockerfiles
FROM ubuntu:20.04

ARG DEBIAN_FRONTEND=noninteractive
ARG APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE=1

ENV LC_ALL=C.UTF-8 \
    LANG=C.UTF-8 \
    LANGUAGE=C.UTF-8

# install OS tools
RUN apt-get update -y && \
    apt-get install -y --no-install-recommends -o=Dpkg::Use-Pty=0 \
        build-essential \
        pkg-config \
        ca-certificates \
        gnupg \
        libarchive13 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

ARG cmake_url=https://github.com/Kitware/CMake/releases/download/v3.20.0/cmake-3.20.0-linux-x86_64.sh
ADD $cmake_url /
RUN file=$(basename "$cmake_url") && \
    bash $file --prefix=/usr --skip-license && \
    rm $file

# add apt repo public key
ARG url=https://apt.repos.intel.com/intel-gpg-keys/GPG-PUB-KEY-INTEL-SW-PRODUCTS-2023.PUB
ADD $url /
RUN file=$(basename "$url") && \
    apt-key add "$file" && \
    rm "$file"

# configure the repository
ARG repo=https://apt.repos.intel.com/oneapi
RUN echo "deb $repo all main" > /etc/apt/sources.list.d/oneAPI.list

# disable cert check
ARG disable_cert_check=
RUN if [ "$disable_cert_check" ] ; then echo "Acquire::https::Verify-Peer \"false\";\nAcquire::https::Verify-Host \"false\";" > /etc/apt/apt.conf.d/99-disable-cert-check ; fi

RUN apt-get update -y && \
    apt-get install -y --no-install-recommends -o=Dpkg::Use-Pty=0 \
    intel-oneapi-compiler-dpcpp-cpp-and-cpp-classic && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# setvars.sh environment variables
ENV CMAKE_PREFIX_PATH='/opt/intel/oneapi/tbb/2021.2.0/env/..:' \
    CPATH='/opt/intel/oneapi/tbb/2021.2.0/env/../include:/opt/intel/oneapi/dev-utilities/2021.2.0/include:/opt/intel/oneapi/compiler/2021.2.0/linux/include' \
    INFOPATH='/opt/intel/oneapi/debugger/10.1.1/documentation/info/' \
    INTELFPGAOCLSDKROOT='/opt/intel/oneapi/compiler/2021.2.0/linux/lib/oclfpga' \
    INTEL_PYTHONHOME='/opt/intel/oneapi/debugger/10.1.1/dep' \
    LD_LIBRARY_PATH='/opt/intel/oneapi/tbb/2021.2.0/env/../lib/intel64/gcc4.8:/opt/intel/oneapi/debugger/10.1.1/dep/lib:/opt/intel/oneapi/debugger/10.1.1/libipt/intel64/lib:/opt/intel/oneapi/debugger/10.1.1/gdb/intel64/lib:/opt/intel/oneapi/compiler/2021.2.0/linux/lib:/opt/intel/oneapi/compiler/2021.2.0/linux/lib/x64:/opt/intel/oneapi/compiler/2021.2.0/linux/lib/emu:/opt/intel/oneapi/compiler/2021.2.0/linux/lib/oclfpga/host/linux64/lib:/opt/intel/oneapi/compiler/2021.2.0/linux/lib/oclfpga/linux64/lib:/opt/intel/oneapi/compiler/2021.2.0/linux/compiler/lib/intel64_lin:/opt/intel/oneapi/compiler/2021.2.0/linux/compiler/lib' \
    LIBRARY_PATH='/opt/intel/oneapi/tbb/2021.2.0/env/../lib/intel64/gcc4.8:/opt/intel/oneapi/compiler/2021.2.0/linux/compiler/lib/intel64_lin:/opt/intel/oneapi/compiler/2021.2.0/linux/lib' \
    MANPATH='/opt/intel/oneapi/debugger/10.1.1/documentation/man:/opt/intel/oneapi/compiler/2021.2.0/documentation/en/man/common' \
    OCL_ICD_FILENAMES='libintelocl_emu.so:libalteracl.so:/opt/intel/oneapi/compiler/2021.2.0/linux/lib/x64/libintelocl.so' \
    ONEAPI_ROOT='/opt/intel/oneapi' \
    PATH='/opt/intel/oneapi/dev-utilities/2021.2.0/bin:/opt/intel/oneapi/debugger/10.1.1/gdb/intel64/bin:/opt/intel/oneapi/compiler/2021.2.0/linux/lib/oclfpga/llvm/aocl-bin:/opt/intel/oneapi/compiler/2021.2.0/linux/lib/oclfpga/bin:/opt/intel/oneapi/compiler/2021.2.0/linux/bin/intel64:/opt/intel/oneapi/compiler/2021.2.0/linux/bin:/opt/intel/oneapi/compiler/2021.2.0/linux/ioc/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin' \
    SETVARS_COMPLETED='1' \
    SETVARS_VARS_PATH='/opt/intel/oneapi/tbb/latest/env/vars.sh' \
    TBBROOT='/opt/intel/oneapi/tbb/2021.2.0/env/..'
