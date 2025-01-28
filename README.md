# Fedora 41 Ansible Test Image with non-root user

Fedora 41 Docker container for Ansible playbook and role testing and non-root user _ansible_.

The image contains a user _ansible_ (with the same password) that can be used to test ansible rules with limited access rights. This verifies that all rights escalations are correct.

Follow [the molecule documentation](https://molecule.readthedocs.io/en/latest/examples.html#docker-with-non-privileged-user) for usage with non-privileged users when using molecule.

## Tags

* `latest`: Latest stable version of Ansible.

The latest tag is a lightweight image for basic validation of Ansible playbooks.

## How to Build

This image is not built on Docker Hub automatically.

If you want to build it locally, do the following:

### Docker

1. [Install Docker](https://docs.docker.com/engine/installation/).
1. `cd` into this directory.
1. Run `docker build -t fedora41-ansible-nonroot .`

### Podman

1. [Install Podman]().
1. `cd` into this directory.
1. Run `podman build -t fedora41-ansible-nonroot .`.

## How to Use

1. Install Docker or Podman.
1. Build the image.
1. Run a container from the image `podman run --detach --privileged  --volume=/sys/fs/cgroup:/sys/fs/cgroup:rw --cgroupns=host localhost/fedora41-ansible-nonroot`. For testing of Ansible roles I integrate this into molecule, but you can mount the current directory into the container with ``---volume=`pwd`:/etc/ansible/roles/testing:ro``).
1. Use Ansible inside the container:

    a. `docker -exec --tty [container_id] env TeRM=xterm ansible --version`
    b. `docker -exec --tty [container_id] env TERM=xterm ansible-playbook /path/to/playbook.yml --syntax-check`

## Author

Based on [docker-fedora39-ansible](https://github.com/geerlingguy/docker-fedora39-ansible) by [Jeff Geerling](https://www.jeffgeerling.com/).
