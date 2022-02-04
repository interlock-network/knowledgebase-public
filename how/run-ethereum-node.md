# Installing/running an Ethereum Node via Docker

In this context, a node is an instance of an Ethereum client running on
the Ethereum network. The easiest way to run a client of your own is via
Docker. You can use the following command to create an instance of a
container running the client software `geth`{.verbatim}:

``` {#install ethereum .shell}
docker pull ethereum/client-go
docker run -it -p 30303:30303 ethereum/client-go
```

Note however, the above command will run a \"full\" Ethereum node. This
could take a tremendous amount of disk space (at the time of writing,
Terabtyes). For this reason, it is recommended to run a \"light\" node
on your developer machine.

## Running a Full Node

-   Stores full blockchain data.
-   Participates in block validation, verifies all blocks and states.
-   All states can be derived from a full node.
-   Serves the network and provides data on request.

## Running a Light Node

-   Stores the header chain and requests everything else.
-   Can verify the validity of the data against the state roots in the
    block headers.
-   Useful for low capacity devices, such as embedded devices or mobile
    phones, which can\'t afford to store gigabytes of blockchain data.

``` {#run light ethereum .shell}
sudo docker run -it -p 30303:30303 ethereum/client-go --syncmode light
```

## Miscellaneous

-   you can pass arguments to Geth via Docker to the image being created
    for example, `--syncmode light`{.verbatim} is a `geth`{.verbatim}
    argument, but Docker passes it on.
-   `geth`{.verbatim} is the name of the \"default/official\" Ethereum
    client implementation. It is written in \"Go\".

[restrict to local
machine](https://stackoverflow.com/questions/51111955/using-ethereum-in-docker-how-to-allow-request-from-host-machine-and-deny-from-o)
