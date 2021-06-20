FROM python:3.8-buster
RUN apt-get -qq update && apt-get -qq -y install curl bzip2 \
    && curl -sSL https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -o /tmp/miniconda.sh \
    && bash /tmp/miniconda.sh -bfp /usr/local \
    && rm -rf /tmp/miniconda.sh \
    && conda install -y python=3 \
    && conda update conda \
    && apt-get -qq -y remove curl bzip2 \
    && apt-get -qq -y autoremove \
    && apt-get autoclean \
    && rm -rf /var/lib/apt/lists/* /var/log/dpkg.log \
    && conda clean --all --yes
RUN conda create -n myenv
RUN echo "source activate myenv" > ~/.bashrc
ENV PATH /opt/conda/bin:$PATH
RUN apt-get clean && \
    apt-get update && \
    apt-get install -y \
        build-essential \
        make \
        curl \
        git \
        autoconf \
        automake \
        libtool \
        pkg-config
RUN wget https://poppler.freedesktop.org/poppler-data-0.4.10.tar.gz \
    && tar -xf poppler-data-0.4.10.tar.gz \
    && cd poppler-data-0.4.10 \
    && make install \
    && cd .. \
    && wget https://poppler.freedesktop.org/poppler-21.03.0.tar.xz \
    && tar -xf poppler-21.03.0.tar.xz \
    && cd poppler-21.03.0 \
    && mkdir build \
    && cd build \
    && pip install cmake \
    && cmake .. \
    && make \
    && make install \
    && cd ../.. \
    && ldconfig \
    && rm poppler-data-0.4.10.tar.gz \
    && rm -rf poppler-data-0.4.10 \
    && rm poppler-21.03.0.tar.xz \
    && rm -rf poppler-21.03.0
RUN apt-get -y install nginx
RUN apt-get -y install default-jre  libreoffice libreoffice-java-common libreoffice-writer
RUN pip install --src /usr/local/src flask flask_cors flask_script gevent wget boto3
RUN pip install --src /usr/local/src opencv-python pytesseract
RUN pip install --src /usr/local/src numpy scipy spacy
RUN pip install --src /usr/local/src  bidict google-cloud-vision==1.0.0 json-logic-qubit==0.9.1 pdf2image==1.14.0 boto3==1.17.27 reportlab==3.5.65 opencv-python==4.5.1.48 openpyxl==3.0.7 pdfquery==0.4.3 shapely==1.7.1 requests==2.25.1 pdfminer.six==20201018 pdftotext==2.1.5 Pillow==8.1.2 pdfminer==20191125 xlsxwriter datefinder PyPDF2 camelot-py[cv]==0.8.0

CMD ["/bin/bash"]
