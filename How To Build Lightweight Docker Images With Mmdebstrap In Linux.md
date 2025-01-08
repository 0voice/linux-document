原文地址：https://ostechnix.com/build-docker-images-with-mmdebstrap/



# How To Build Lightweight Docker Images With Mmdebstrap In Linux

## A Step-by-Step Guide to Create Minimal Debian-based Container Images for Docker using Mmdebstrap



Building lightweight container images with **`mmdebstrap`** for **[Docker](https://ostechnix.com/getting-started-with-docker/)** is a great way to create minimal and efficient environments for your applications. This process allows you to leverage the power of Debian while keeping your images small and manageable. In this step-by-step tutorial, we will explain how to **build docker images with mmdebstrap** in Linux.

This is useful to create optimized, minimal Docker images, such as microservices, CI/CD pipelines, or serverless applications.



## **Why Use `mmdebstrap`?**

- **Small Base Images:** It produces minimal Debian root filesystems, reducing image size.
- **Flexible Output Formats:** It can generate tarballs, squashfs, or directory outputs, which can be easily imported into Docker.
- **No Dependencies:** It does not require `dpkg` or `apt` inside the container.
- **Reproducibility:** It supports exact package versions for consistent builds.



## Build Docker Images with mmdebstrap

**`mmdebstrap`** is a modern, minimal, and dependency-free alternative to `debootstrap` for creating Debian-based root filesystems. It supports reproducible builds and integrates well with Docker.

### Prerequisites

Before you start, ensure you have the following installed:

Make sure **Docker is installed** and running on your system. if not, use the following links to install Docker on your preferred Linux system.

- **[Install Docker Engine And Docker Compose In RPM-based Systems](https://ostechnix.com/install-docker-almalinux-centos-rocky-linux/)**
- **[How to Install Docker Engine And Docker Compose In Ubuntu](https://ostechnix.com/install-docker-ubuntu/)**

You can also use **[Podman](https://ostechnix.com/what-is-podman-and-how-to-install-podman-in-linux/)** if you prefer to run containers in rootless mode.



Next, **[Install mmdebstrap](https://ostechnix.com/create-chroot-environments-using-mmdebstrap-in-debian-linux/)** if you haven't already. You can do this with the following command:

```
sudo apt update
sudo apt install mmdebstrap
```

### Step 1: Create a Minimal Debian Filesystem

We will first create a basic Debian image using `mmdebstrap`. This image will serve as the foundation for our Docker container.

**1. Choose a Debian Suite**:

Decide which Debian release you want to use (e.g., `bullseye`, `bookworm`).

**2. Create the Image**:

Run the following command to create a basic Debian filesystem:

```
mmdebstrap --variant=minbase --include=ca-certificates,curl stable debian-rootfs.tar
```

This adds required packages like `curl` and `ca-certificates`. You can further customize the container by installing any other additional packages or making configuration changes.

Here,

- **`--variant=minbase`:** Creates a minimal base system without unnecessary packages.
- **`--include=ca-certificates,curl`**: Installs curl and ca-certificates in the debian image.
- **`stable`:** Specifies the Debian release (e.g., `stable`, `bookworm`, or `bullseye`).
- **`debian-rootfs.tar`:** Output tarball for the root filesystem.

You can also clean up package caches and logs inside the tarball before importing:



```
tar --delete -f debian-rootfs.tar ./var/cache/apt ./var/lib/apt/lists
```

### Step 2: Import the Tarball into Docker

Import the Debian image that you created in the earlier step into docker using command:

```
cat debian-rootfs.tar | docker import - debian:custom
```

Here,

- **`debian:custom`:** Assigns a tag to the imported image.

### Step 3: Verify the Docker Images

Verify if the docker image is imported into your docker environment using command:

```
docker images
```

You will see an output like below:

```
REPOSITORY                  TAG         IMAGE ID      CREATED         SIZE
localhost/debian            custom      7762908acf49  21 seconds ago  170 MB
```

### Step 4: Run the Container

Finally, run the container with the new image using command:



```
docker run -it debian:custom /bin/bash
```

This command starts a new container from your image and opens an interactive terminal.

If you want to run the container in detached mode, use `-d` flag.

## Conclusion

Using `mmdebstrap` to build lightweight container images for Docker is a straightforward process. By creating a minimal Debian environment, you can ensure that your images are small and efficient.

This method is especially useful for developers looking to create custom Docker images tailored to their applications. With just a few steps, you can have a fully functional and lightweight Debian container ready for your projects.

**Related Read**:

- **[How To Build Custom Docker Image Using Dockerfile](https://ostechnix.com/a-brief-introduction-to-dockerfile/)**
- **[Troubleshooting Guide For Mmdebstrap: Fixing Common Issues](https://ostechnix.com/troubleshooting-mmdebstrap/)**

