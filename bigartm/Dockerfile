FROM jupyter/datascience-notebook

USER root

# Step 1. Update and install dependencies
RUN apt-get --yes update
RUN apt-get --yes install gcc g++ git make cmake build-essential libboost-all-dev

# Step 2. Insall python packages
RUN apt-get --yes install wget python-numpy python-pandas python-scipy
RUN wget https://bootstrap.pypa.io/get-pip.py \
&& python get-pip.py \
&& pip install protobuf tqdm wheel

# Step 3. Clone repository and build
RUN git clone --branch=stable https://github.com/bigartm/bigartm.git \
&& cd bigartm \
&& mkdir build && cd build \
&& cmake .. \
&& make \

# Step 4. Install BigARTM
&& make install \
&& export ARTM_SHARED_LIBRARY=/usr/local/lib/libartm.so

# Step 5. Install necessary python packages
RUN pip install nltk \
&& pip install html2text

RUN cd / && mkdir notebooks && chown -R jovyan:users notebooks/

WORKDIR "/notebooks"