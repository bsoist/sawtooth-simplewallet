# Copyright 2018 Intel Corporation
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
# -----------------------------------------------------------------------------

FROM ubuntu:bionic

# ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
 && apt-get install gnupg -y

RUN apt-get install -y -q --no-install-recommends \
    apt-utils \
 && apt-get install -y -q \
    ca-certificates \
    build-essential \
   #  python3-sawtooth-cli \
    curl \
    vim \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

RUN apt-get update \
   && apt-get --allow-unauthenticated upgrade -y

RUN apt-get install -y -q \
   python3.7 \
   python3.7-distutils

RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py \
 && python3.7 get-pip.py

RUN pip3.7 install sawtooth

RUN curl -sL https://deb.nodesource.com/setup_8.x >setup_8.x
RUN sed 's/sleep 60//' setup_8.x >setup_node.sh 
RUN sh setup_node.sh 
RUN apt-get install -y nodejs

WORKDIR /project/simplewallet/jsclient

ENV PATH "$PATH:/project/simplewallet/jsclient"

EXPOSE 3000

CMD npm install && npm start

ENTRYPOINT ["tail", "-f", "/dev/null"]