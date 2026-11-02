FROM intel/oneapi:2025.3.1-0-devel-ubuntu24.04

ARG WHISPER_CPP_VERSION

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

RUN \
    apt-get update \
    && apt-get install -y --no-install-recommends \
        netcat-traditional

RUN \
    git clone --depth 1 --branch v${WHISPER_CPP_VERSION} https://github.com/ggerganov/whisper.cpp.git whisper.cpp \
    && cd whisper.cpp \
    && cmake -B build -DGGML_SYCL=ON -DCMAKE_C_COMPILER=icx -DCMAKE_CXX_COMPILER=icpx -DGGML_SYCL_F16=ON \
    && cmake --build build -j --config Release

WORKDIR /whisper.cpp
