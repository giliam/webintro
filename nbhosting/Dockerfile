# to redo from scratch:
#FROM jupyter/minimal-notebook:latest
#USER root

# as of today this is python-3.7.1
FROM nbhosting/minimal-notebook

RUN pip install jupytext


# prerequisites with apt-get
# we do install python(2) here because
# some npm build part named gyp still requires it
RUN apt-get update && apt-get install -y gcc g++ make python


# !!! dirty trick!!!
# original PATH is
# /opt/conda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
# move conda's path **at the end**
# so that python resolves in /usr/bin/python(2)
# but node is still found in conda
ENV PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/opt/conda/bin"
USER jovyan
RUN npm install -g ijavascript
RUN ijsinstall


# !!! clean up!!!
USER root
RUN apt-get autoremove -y python
ENV PATH="/opt/conda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"


# somehow node won't find stuff installed by npm, this band-aid will help
ENV NODE_PATH="/opt/conda/lib/node_modules/"
USER jovyan


# for displaying html fragments
RUN npm install -g jsdom d3 ijavascript-plotly plotly-notebook-js