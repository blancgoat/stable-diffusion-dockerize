FROM pytorch/pytorch:2.3.0-cuda12.1-cudnn8-runtime
ENV DEBIAN_FRONTEND=noninteractive PIP_PREFER_BINARY=1
RUN sed -i 's@archive.ubuntu.com@mirror.kakao.com@g' /etc/apt/sources.list

RUN apt-get update
RUN apt-get -y install git libgoogle-perftools-dev libgl1 libglib2.0-0

WORKDIR /stable-diffusion-webui
RUN git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git .
COPY ./webui-user.sh .
  
ENV NVIDIA_VISIBLE_DEVICES=all
EXPOSE 7860
ENTRYPOINT [ "./webui.sh" , "-f"]
