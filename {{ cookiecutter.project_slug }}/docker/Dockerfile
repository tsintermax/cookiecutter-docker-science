{%- if cookiecutter.use_nvidia_docker == 'yes' -%}
FROM nvidia/cuda:8.0-cudnn5-devel-ubuntu16.04
{%- else -%}
FROM jupyter/datascience-notebook
{%- endif %}

COPY ./requirements.txt /requirements.txt
COPY config/jupyter_notebook_config.py ./.jupyter/
RUN pip install -r /requirements.txt

RUN curl -L  "https://oscdl.ipa.go.jp/IPAexfont/ipaexg00301.zip" > font.zip
RUN unzip font.zip
RUN cp ipaexg00301/ipaexg.ttf /opt/conda/lib/python3.7/site-packages/matplotlib/mpl-data/fonts/ttf/ipaexg.ttf
RUN echo "font.family : IPAexGothic" >>  /opt/conda/lib/python3.7/site-packages/matplotlib/mpl-data/matplotlibrc
RUN rm -r ./.cache && rm -r font.zip && rm -r ipaexg00301/

ENV TZ='Asia/Tokyo'
#nvidiaのイメージをもし使う場合は要修正
WORKDIR /home/jovyan/work 
ENTRYPOINT ["/bin/bash"]
