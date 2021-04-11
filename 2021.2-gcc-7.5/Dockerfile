# Adtapted from Intel Dockerfiles
FROM intel/oneapi:os-tools-ubuntu18.04

ARG DEBIAN_FRONTEND=noninteractive
ENV LC_ALL=C.UTF-8 \
    LANG=C.UTF-8 \
    LANGUAGE=C.UTF-8

RUN apt-get update -y && \
    apt-get install -y --no-install-recommends -o=Dpkg::Use-Pty=0 \
    intel-oneapi-compiler-dpcpp-cpp-and-cpp-classic

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
