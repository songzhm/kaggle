# Build from kaggle python image
FROM kaggle/python

# install sudo
RUN apt-get update && \
      apt-get -y install sudo

# Make kaggler user, wd, data for joblib, input folder
RUN useradd -m -s /bin/bash -N -u 1000 kaggler && echo "kaggler:kaggler" | chpasswd && adduser kaggler sudo &&\
  mkdir -p /wd && chown kaggler /wd && \
  mkdir -p /data && chown kaggler /data && \
  mkdir -p /input && chown kaggler /input

USER kaggler

# Set up joblib temp
ENV JOBLIB_TEMP_FOLDER=/data/joblib

# Include the gym code in home/gym
ADD ./gym/kagglegym.py /home/kaggler/gym/kagglegym.py
ADD /gym/__init__.py /home/kaggler/gym/__init__.py

# Include the training data in input
ADD  ./gym/input/train.h5 /input/train.h5

# Add the location of kagglegym to the pythonpath
ENV PYTHONPATH="${PYTHONPATH}:/home/kaggler/gym"

WORKDIR /wd

# Port for jupyter notebook
EXPOSE 8888
