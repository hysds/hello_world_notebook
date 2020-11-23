FROM hysds/pge-base:latest

ENV HOME=/home/ops \
    CONDA_DIR=/opt/conda

RUN $CONDA_DIR/bin/conda install -y nb_conda_kernels

USER ops

RUN cd $HOME \
    && git clone https://github.com/hysds/notebook_pge_wrapper.git \
    && cd notebook_pge_wrapper \
    && $HOME/verdi/bin/pip install -e .

# copy your repo into the docker container
################################################
COPY . /home/ops/hello_world_notebook
################################################

WORKDIR $HOME

CMD ["/bin/bash", "--login"]
