FROM tensorflow/tensorflow:1.0.0-gpu

MAINTAINER Akshay Bhat <akshayubhat@gmail.com>
RUN apt-get update && apt-get install -y wget
WORKDIR "/bin/"
RUN wget https://johnvansickle.com/ffmpeg/releases/ffmpeg-release-64bit-static.tar.xz
RUN tar xvfJ ffmpeg-release-64bit-static.tar.xz
RUN mv ffmpeg*/* .
WORKDIR "/root/
RUN apt-get update && apt-get install -y \
		bc \
		build-essential \
		curl \
		git \
		libffi-dev \
		libssl-dev \
		libtiff5-dev \
		libzmq3-dev \
		nano \
		pkg-config \
		python-pip \
		python-dev \
		software-properties-common \
		unzip \
		vim \
		wget \
		zlib1g-dev \
		libboost-all-dev \
		libgflags-dev \
		libgoogle-glog-dev \
		&& \
	apt-get clean && \
	apt-get autoremove && \
	rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y libpq-dev && \
	apt-get clean && \
	apt-get autoremove && \
	rm -rf /var/lib/apt/lists/*
RUN wget https://s3.amazonaws.com/pytorch/whl/cu80/torch-0.1.7.post2-cp27-none-linux_x86_64.whl 
RUN pip install torch-0.1.7.post2-cp27-none-linux_x86_64.whl
RUN pip install scipy
RUN pip install torchvision
RUN pip install --upgrade pip \
                          fabric \
                          django \
                          jinja \
                          jinja2 \
                          djangorestframework \
                          markdown \
                          django-filter \
                          "celery==3.1.23" \
                          "django-celery==3.1.17" \
                          "dj-database-url==0.4.0" \
                          "whitenoise==2.0.6" \
                          raven \
                          psycopg2 \
                          requests \
                          pandas \
                          boto3 \
                          protobuf \
                          humanize
RUN apt-get update && apt-get install -y \
    pkg-config \
    python-dev \
    python-opencv \
    libopencv-dev \
    libav-tools  \
    libjpeg-dev \
    libpng-dev \
    libtiff-dev \
    libjasper-dev \
    python-numpy \
    python-pycurl \
    python-opencv
RUN wget https://yt-dl.org/downloads/latest/youtube-dl -O /bin/youtube-dl
RUN chmod a+rx /bin/youtube-dl
RUN youtube-dl -U
RUN git clone https://github.com/akshayubhat/DeepVideoAnalytics /root/DVA
WORKDIR "/root/DVA/darknet"
RUN mv Makefile.gpu Makefile
RUN make
RUN wget https://www.dropbox.com/s/0zopjpswug5rjqy/yolo9000.weights
VOLUME ["/root/DVA/dva/media"]
RUN dpkg -L python-opencv
RUN apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys B97B0AFCAA1A47F044F244A07FCC7D46ACCC4CF8
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main" > /etc/apt/sources.list.d/pgdg.list
RUN apt-get update && apt-get install -y postgresql-client-9.6 zip
WORKDIR "/root/DVA"
RUN apt-get update && apt-get install -y nginx supervisor
RUN pip install --upgrade uwsgi matplotlib
RUN git pull
RUN cd dvalib/ssd/checkpoints && unzip ssd_300_vgg.ckpt.zip
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
EXPOSE 80
