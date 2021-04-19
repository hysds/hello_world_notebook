FROM cae-artifactory.jpl.nasa.gov:16001/gov/nasa/jpl/nisar/sds/pcm/nisar_ade:latest

ENV HOME=/home/jovyan \
    CONDA_DIR=/opt/conda

USER root
RUN $CONDA_DIR/bin/conda install -y nb_conda_kernels

USER jovyan

RUN $HOME/verdi/bin/pip install 'ipykernel<5.0.0'

RUN cd $HOME \
    && git clone https://github.com/hysds/notebook_pge_wrapper.git \
    && cd notebook_pge_wrapper \
    && $HOME/verdi/bin/pip install -e .

# copy your repo into the docker container
################################################
COPY . $HOME/hello_world_notebook
################################################

# testing
RUN conda install -c conda-forge nodejs -y

# installing user defined dependencies
RUN $HOME/verdi/bin/papermill $HOME/hello_world_notebook/docker/requirements.ipynb /tmp/requirements_output.ipynb --log-output

WORKDIR $HOME

CMD ["/bin/bash", "--login"]
