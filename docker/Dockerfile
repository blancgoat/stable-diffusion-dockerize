# ARG values are defaults. Override them by creating a .env file or using --build-arg
ARG PYTORCH_IMAGE_TAG=2.4.0-cuda12.1-cudnn9-runtime
FROM pytorch/pytorch:${PYTORCH_IMAGE_TAG}
ENV DEBIAN_FRONTEND=noninteractive PIP_PREFER_BINARY=1
ENV NVIDIA_VISIBLE_DEVICES=all

ARG MIRROR_URL=""
RUN if [ -n "$MIRROR_URL" ]; then \
        sed -i "s@archive.ubuntu.com@$MIRROR_URL@g" /etc/apt/sources.list; \
    fi && \
    apt-get update && \
    apt-get -y install git libgoogle-perftools-dev libgl1 libglib2.0-0 && \
    apt clean && \
    rm -rf /var/lib/apt/lists/

ARG XFORMERS_TAG="0.0.27.post2"
RUN pip install xformers==${XFORMERS_TAG}

ARG WEBUI_VERSION="v1.10.1"
WORKDIR /stable-diffusion-webui
RUN git clone --branch ${WEBUI_VERSION} https://github.com/AUTOMATIC1111/stable-diffusion-webui.git . && \
    pip install -r requirements.txt

ENV COMMANDLINE_ARGS="--listen --xformers --enable-insecure-extension-access --no-download-sd-model"

COPY webui-user.sh .
ENTRYPOINT [ "./webui.sh" , "-f" ]
