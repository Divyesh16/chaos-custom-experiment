FROM python:3.7-stretch

LABEL maintainer="sumit nagal"
LABEL name=chaostest

### upgrade and setup python
RUN apt-get update \
    && apt-get -y install gcc python-pip python3-pip python-dev curl \
    && pip install --upgrade pip \
    && pip install jinja2 pyYaml

### Setup kops
WORKDIR /app
WORKDIR /app/kops/
ENV kopsversion=1.10.0
RUN curl -Lsf -o kops-linux-amd64 https://github.com/kubernetes/kops/releases/download/${kopsversion}/kops-linux-amd64
RUN chmod +x ./kops-linux-amd64
RUN mv ./kops-linux-amd64 /usr/local/bin/kops

### Setup kubectl
WORKDIR /app/kubectl/
RUN curl -Lsf -o kubectl https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
RUN chmod +x ./kubectl
RUN mv ./kubectl /usr/local/bin/kubectl

#### Other Packages
#RUN export DEBIAN_FRONTEND=noninteractive \
#    && apt-get install -y texlive-latex-base texlive-fonts-recommended texlive-latex-extra \
#    vim \
#    net-tools \
#    libcairo2-dev \
#    && curl -Lvf -o pandoc.deb https://github.com/jgm/pandoc/releases/download/2.2.1/pandoc-2.2.1-1-amd64.deb \
#    && dpkg -i pandoc.deb \
#    && apt-get remove -y curl \
#    texlive-latex-extra-doc \
#    texlive-latex-recommended-doc \
#    texlive-latex-base-doc \
#    texlive-fonts-recommended-doc \
#    texlive-pstricks-doc \
#    texlive-pictures-doc \
#    && apt-get autoremove || true \
#    && apt-get autoclean || true

RUN rm -rf /tmp/* /root/.cache

ENV LC_ALL=C.UTF-8

ENV LANG=C.UTF-8

WORKDIR /app/chaos

### Setup chaostoolkit packages
COPY . /app/chaos

RUN chmod +x install.sh

RUN ./install.sh
WORKDIR /app/chaos
