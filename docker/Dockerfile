# Start with BioSim base image.
ARG BASE_IMAGE=latest
FROM ghcr.io/ccpbiosim/jupyterhub-base:$BASE_IMAGE

LABEL maintainer="James Gebbie-Rayet <james.gebbie@stfc.ac.uk>"

# Switch to jovyan user.
USER $NB_USER
WORKDIR $HOME

# Install workshop deps 
RUN conda install -y -c conda-forge \
    conda-forge::ambertools=26.0 \
    conda-forge::ipywidgets=8.1.9 \
    conda-forge::mdtraj=1.11.1 \
    conda-forge::netcdf4=1.7.4 \
    conda-forge::nglview=4.0.1 \
    conda-forge::openmm=8.6.1 \
    conda-forge::parmed= 4.3.1

COPY docker/fix-nglview.sh /tmp/fix-nglview.sh
RUN bash /tmp/fix-nglview.sh

# Get workshop files and move them to jovyan directory.
COPY --chown=1000:100 . .
RUN rm -rf INSTALL.txt LICENSE README.md docker .git .github .gitignore environment.yaml run_notebook.sh

# Copy updated lab workspace
#COPY --chown=1000:100 docker/default-37a8.jupyterlab-workspace /home/jovyan/.jupyter/lab/workspaces/default-37a8.jupyterlab-workspace

# Always finish with non-root user as a precaution.
USER $NB_USER
