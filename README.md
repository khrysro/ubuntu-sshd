# ubuntu-sshd

Dockerized SSH service, built on top of [official Ubuntu](https://registry.hub.docker.com/_/ubuntu/) images.

## Image tags

- khrysro/ubuntu-sshd:12.04 (precise)
- khrysro/ubuntu-sshd:14.04 (trusty)
- khrysro/ubuntu-sshd:16.04 (xenial)
- khrysro/ubuntu-sshd:18.04 (bionic)

## Installed packages

Base:

- [Precise (12.04) minimal](http://packages.ubuntu.com/precise/ubuntu-minimal)
- [Trusty (14.04) minimal](http://packages.ubuntu.com/trusty/ubuntu-minimal)
- [Xenial (16.04) minimal](http://packages.ubuntu.com/xenial/ubuntu-minimal)
- [Bionic (18.04) minimal](http://packages.ubuntu.com/bionic/ubuntu-minimal)

Image specific:
- [openssh-server](https://help.ubuntu.com/community/SSH/OpenSSH/Configuring)

Config:

  - `PermitRootLogin yes`
  - `UsePAM no`
  - exposed port 22
  - default command: `/usr/sbin/sshd -D`
  - root password: `root`

## Run example

```bash
$ sudo docker run -d -P --name test_sshd khrysro/ubuntu-sshd:14.04
$ sudo docker port test_sshd 22
  0.0.0.0:49154

$ ssh root@localhost -p 49154
# The password is `root`
root@test_sshd $
```

## Security

If you are making the container accessible from the internet you'll probably want to secure it bit.
You can do one of the following two things after launching the container:

- Change the root password: `docker exec -ti test_sshd passwd`
- Don't allow passwords at all, use keys instead:

```bash
$ docker exec test_sshd passwd -d root
$ docker cp file_on_host_with_allowed_public_keys test_sshd:/root/.ssh/authorized_keys
$ docker exec test_sshd chown root:root /root/.ssh/authorized_keys
```

## Issues

If you run into any problems with this image, please check (and potentially file new) issues on the [khrysro/ubuntu-sshd](https://github.com/khrysro/ubuntu-sshd/issues) repo, which is the source for this image.
