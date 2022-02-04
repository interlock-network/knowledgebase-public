# Installing/running a Solana Node via Docker

You can find the official Docker image for Solana
[here](https://hub.docker.com/r/solanalabs/solana).

``` {#pull the docker image .shell}
docker pull solanalabs/solana:v1.9.2
```

Note that in the above command you should specify a version. It is not
enough to attempt `docker pull solanalabs/solana`{.verbatim}, this will
not work because there is no manifest specification.

After pulling the image, you can start it:

``` {#pull the docker image .shell}
docker run solanalabs/solana:v1.9.2
```

Make sure that you use the same version number as in your previous
command you used to fetch the image.
