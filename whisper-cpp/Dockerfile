FROM intel/oneapi:2026.2.0-devel-ubuntu26.04

ARG WHISPER_CPP_VERSION
ARG BUILD_PARALLEL_JOBS=4

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

WORKDIR /whisper.cpp

RUN \
    git clone --depth 1 --branch v${WHISPER_CPP_VERSION} https://github.com/ggml-org/whisper.cpp.git . \
    && cmake -S . -B build \
        -DCMAKE_BUILD_TYPE=Release \
        -DCMAKE_C_COMPILER=icx \
        -DCMAKE_CXX_COMPILER=icpx \
        -DGGML_CCACHE=OFF \
        -DWHISPER_OPENVINO=OFF \
        -DGGML_SYCL=ON \
        -DGGML_SYCL_F16=ON \
        # Examples required for the whisper-server target
        -DWHISPER_BUILD_EXAMPLES=ON \
        -DWHISPER_BUILD_TESTS=OFF \
        -DWHISPER_BUILD_SERVER=OFF \
    && cmake --build build --parallel ${BUILD_PARALLEL_JOBS} --target whisper-server
