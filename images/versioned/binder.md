---
title: binder
---

## Quick reference

- Source repository: [rocker-org/rocker-versioned2](https://github.com/rocker-org/rocker-versioned2)
- [Dockerfile](https://github.com/rocker-org/rocker-versioned2/blob/master/dockerfiles/binder_devel.Dockerfile)
- tags
  - [DockerHub](https://hub.docker.com/r/rocker/binder/tags)
  - [GitHub Container Registry](https://github.com/rocker-org/rocker-versioned2/pkgs/container/binder/versions)
- Published image details: [rocker-org/rocker-versioned2's wiki](https://github.com/rocker-org/rocker-versioned2/wiki)
- Non-root default user: `rstudio`

## Overview

This image is based on [`rocker/geospatial`](rstudio.md) and
configured to run RStudio Server on [Binder](https://mybinder.org/),
thanks to [`jupyter-rsession-proxy`](https://github.com/jupyterhub/jupyter-rsession-proxy).

For instructions on how to use this image with Binder for your project,
see the [rocker-org/binder](https://github.com/rocker-org/binder), a template repository.

By placing the following badge in `README.md` of your project,
RStudio can be started and used in the browser by simply clicking on the badge.

```md
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/<GITHUB_USER>/<REPO>/<BRANCH>?urlpath=rstudio)
```

You can also make a Binder badge with `usethis::use_binder_badge()` R function.

If you use this image with Docker,
the default command runs Jupyter notebook.
Since the Jupyter notebook port is set to `8888`,
you can open the Jupyter notebook screen on `localhost:8888` from your browser with the following command.

```sh
docker run --rm -ti -p 8888:8888 rocker/binder
```

You can log in by entering the token displayed in the terminal as your password.

:::{.callout-tip}

RStudio Server started from jupyter does not read environment variables set at container startup;
if you want to use environment variables on your RStudio instance, set them on the `.Renviron` file.

:::

:::{.callout-note}

This document is for R 4.0.0 >= images.

:::