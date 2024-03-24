# Welcome to the SCOPED Specufex Container

This repository contains the code necessary to build the SCOPED containers for Specufex. For more information on using Specufex, see the [documentation](https://specufex.github.io/specufex) and the [code](https://github.com/specufex/specufex).

Three containers are built by this repository:

- `ghcr.io/seisscoped/specufex:latest`

- `ghcr.io/seisscoped/specufex:tutorial`

- `ghcr.io/seisscoped/specufex:ubuntu22.04`

The first two images are the same, except that the Jupyterlab instance in the `specufx:tutorial` image opens in the `tutorials` directory. This directory contains a notebook to work on some data from The Geysers geothermal field in California (see [Holtzman, et al., Science Advances (2018)](https://advances.sciencemag.org/content/4/5/eaao2929).) Both of these are currently built for Intel and ARM 64 platforms.

The `specufex:ubuntu22.04` image imcludes MPI support and is only built for AMD64 platforms. Specufex does not currently use MPI however.

The containers are set up to run a Jupyter Lab server with the appropriate environment and dependencies for Specufex. To run the tutorial, first pull it from the registry and then start it up. Using the terminal:

```bash
docker pull ghcr.io/seisscoped/specufex:tutorial
docker run -p 8888:8888 ghcr.io/seisscoped/specufex:tutorial
```

Once the container starts it will print out a bunch of stuff, ending with something like

```bash
    To access the server, open this file in a browser:
        file:///home/scoped/.local/share/jupyter/runtime/jpserver-22-open.html
    Or copy and paste one of these URLs:
        http://e3899a50623c:8888/lab?token=7a35fb512dea5eb10b46c30b71be175f3e55eeefba3aee16
     or http://127.0.0.1:8888/lab?token=7a35fb512dea5eb10b46c30b71be175f3e55eeefba3aee16
```

Following those instructions will open the Jupyter Lab server from your browser.

To use the container with your own data, you have to either pull the data into a notebook from a remote server or mount a local directory contiaining the data to the container. For the latter, start the docker container like so

```bash
docker run -v path/to/your/local/directory:/home/specufex/data \
 -p 8888:8888 \
 ghcr.io/seisscoped/specufex:latest
```

When you open the server in your browser, you will see your directory and its contents in the file pane on the left hand side of the page.
