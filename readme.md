
# Week1: etcd Installation and Single-Node Cluster Setup Guide

This guide provides a comprehensive overview of installing etcd, configuring your system to run it, and setting up a single-node etcd cluster on a Linux system.

## Downloading etcd

To download a specific version of etcd from the official GitHub repository:

1. Identify the version you want to download from [etcd releases](https://github.com/etcd-io/etcd/releases/).
2. Use the following commands to download and extract etcd to a temporary location:

```sh
ETCD_VER=<version> # Example: v3.4.31
DOWNLOAD_URL=https://github.com/etcd-io/etcd/releases/download
curl -L ${DOWNLOAD_URL}/${ETCD_VER}/etcd-${ETCD_VER}-linux-amd64.tar.gz -o /tmp/etcd-${ETCD_VER}-linux-amd64.tar.gz
tar xzvf /tmp/etcd-${ETCD_VER}-linux-amd64.tar.gz -C /tmp/etcd-download-test --strip-components=1
```

## Making etcd Accessible System-wide

After downloading and extracting etcd, you may encounter a message indicating `etcd` command is not found. This is because the binary is not in your system's `PATH`. To resolve this:

### Moving etcd Binaries

1. Move `etcd` and `etcdctl` to a more permanent location, `/usr/local/bin`:

```sh
sudo mv /tmp/etcd-download-test/etcd /usr/local/bin/
sudo mv /tmp/etcd-download-test/etcdctl /usr/local/bin/
```

### Updating the PATH Variable

For bash users, add `/usr/local/bin` to your `PATH` by editing `~/.bashrc`:

```sh
echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

For zsh users, modify `~/.zshrc` instead:

```sh
echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

## Setting Up a Single-Node Cluster

Follow the steps outlined in the etcd documentation for setting up a single-node cluster:

1. Start the etcd server:

```sh
etcd
```

2. Interact with etcd using `etcdctl`:

```sh
etcdctl put mykey myvalue
etcdctl get mykey
```

For detailed instructions, refer to the [etcd Quickstart Guide](https://etcd.io/docs/v3.5/quickstart/).

## Note

- This guide focuses on development and testing environments. For production setups, consult the official etcd documentation for security, clustering, and configuration best practices.
