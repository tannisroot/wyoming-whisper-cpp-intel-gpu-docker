FROM alpine:latest

ARG WHISPER_CPP_VERSION

RUN \
    apk update \
    && apk add \
        bash \
        wget

RUN \
    wget https://raw.githubusercontent.com/ggml-org/whisper.cpp/refs/tags/v${WHISPER_CPP_VERSION}/models/download-ggml-model.sh \
    && chmod +x download-ggml-model.sh

CMD ["/bin/sh", "-c", "./download-ggml-model.sh ${WHISPER_MODEL} /models"]
