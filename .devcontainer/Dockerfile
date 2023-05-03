# See here for image contents: https://hub.docker.com/r/jupyter/datascience-notebook/
FROM jupyter/datascience-notebook

# Package installation steps for the OS need to be done as root
USER root

# Install additional OS packages (some of which are needed for R/Python packages below)
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
 && apt-get -y install --no-install-recommends \
    build-essential zlib1g-dev zip texlive-fonts-recommended lmodern cmake

# Do all other steps using the account the VS Code user will use
USER jovyan

# Note: Steps below are sequenced primarily to ensure that A precedes B iff A is
# needed for B to work, but secondarily sequenced to put frequently edited things
# later in the list, to minimize container rebuild times.

# Install the following Python packages that aren't part of the Jupyter
# datascience-notebook image
RUN pip3 --disable-pip-version-check --no-cache-dir \
    install rdatasets jupytext \
 && rm -rf /tmp/pip-tmp

# Install the following Julia packages that aren't part of the Jupyter
# datascience-notebook image
RUN julia -e 'using Pkg; Pkg.add("DataFrames")'
RUN julia -e 'using Pkg; Pkg.add("Plots")'
RUN julia -e 'using Pkg; Pkg.add("Statistics")'
RUN julia -e 'using Pkg; Pkg.add("RDatasets")'
RUN julia -e 'using Pkg; Pkg.add("Distributions")'
RUN julia -e 'using Pkg; Pkg.add("HypothesisTests")'
RUN julia -e 'using Pkg; Pkg.add("GLM")'

# Install the following R packages that aren't part of the Jupyter
# datascience-notebook image
RUN R -e 'install.packages("lattice",repos="http://cran.us.r-project.org")'
RUN R -e 'install.packages("gplots",repos="http://cran.us.r-project.org")'
RUN R -e 'install.packages("gmodels",repos="http://cran.us.r-project.org")'
