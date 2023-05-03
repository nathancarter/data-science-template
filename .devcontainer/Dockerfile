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

# If you want any Python packages installed by default as part of the image, do:
# (I avoid doing this because it significantly increases container build times.)
# RUN pip3 --disable-pip-version-check --no-cache-dir \
#     install PUT PACKAGE NAMES HERE \
#  && rm -rf /tmp/pip-tmp

# If you want any Julia packages installed by default as part of the image, do:
# (I avoid doing this because it significantly increases container build times.)
# RUN julia -e 'using Pkg; Pkg.add("PUT")'
# RUN julia -e 'using Pkg; Pkg.add("PACKAGE")'
# RUN julia -e 'using Pkg; Pkg.add("NAMES")'
# RUN julia -e 'using Pkg; Pkg.add("HERE")'

# If you want any R packages installed by default as part of the image, do:
# (I avoid doing this because it significantly increases container build times.)
# RUN R -e 'install.packages("PUT",    repos="http://cran.us.r-project.org")'
# RUN R -e 'install.packages("PACKAGE",repos="http://cran.us.r-project.org")'
# RUN R -e 'install.packages("NAMES",  repos="http://cran.us.r-project.org")'
# RUN R -e 'install.packages("HERE",   repos="http://cran.us.r-project.org")'
