FROM jupyter/datascience-notebook:8a1b90cbcba5

# pin jupyterhub to match the Hub version
# set via `docker build --build-arg ...`
ARG JUPYTERHUB_VERSION=0.9.1
RUN pip install --no-cache jupyterhub==$JUPYTERHUB_VERSION


# Infrastructure extensions and tools
RUN pip install --no-cache git+https://github.com/OpenHumans/jhoauth-refresh@3ce0b6f7d42f0416cf056dcb887cfefb62b8b513
RUN jupyter serverextension enable --py jhoauthrefresh --sys-prefix

RUN pip install --no-cache git+https://github.com/data-8/nbgitpuller@28fe9b1af2ba64b346d59bd13c99581346bf349f
RUN jupyter serverextension enable --py nbgitpuller --sys-prefix

RUN pip install --no-cache git+https://github.com/gedankenstuecke/jupyter-notebook-importer.git@v0.0.2
RUN jupyter serverextension enable --py oh_notebook_importer --sys-prefix

ENV JH_BUNDLE_REDIRECT http://juno-exploratory.herokuapp.com/shared

RUN pip install --no-cache git+https://github.com/gedankenstuecke/jupyter-bundler-openhumans.git@v0.0.3
RUN jupyter bundlerextension enable --py oh_bundler --sys-prefix
RUN jupyter nbextension install --py oh_bundler --sys-prefix
RUN jupyter nbextension enable --py oh_bundler --sys-prefix

# R packages users like to use
RUN R -e "install.packages(c('stringr', 'tidytext', 'purrr', 'widyr'), repos = 'http://cran.us.r-project.org')"

# Python packages users like to use
RUN pip install --no-cache \
       textblob==0.15.1 \
       emoji==0.5.0 \
       open-humans-api==0.2.2
RUN python -m textblob.download_corpora
