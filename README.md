# Tiny SSH client (openssh-client + expect)

![ci status](https://github.com/abousselmi/ssh-client/actions/workflows/main.yml/badge.svg)

## Alpine image

```console
docker run -it --rm ghcr.io/abousselmi/alpine-ssh-client sh
```

## Bitnami Minideb image

```console
docker run -it --rm ghcr.io/abousselmi/minideb-ssh-client sh
```

## Gitlab-CI sample

```yaml
ssh-to-server:
  stage: ssh
  image:
    ghcr.io/abousselmi/alpine-ssh-client:latest
  before_script:
    - mkdir -p ~/.ssh
    - chmod 700 ~/.ssh
    - echo -e "Host *\n\tStrictHostKeyChecking no\n\n" > ~/.ssh/config
    - echo "Revert [cat id_rsa | base64 -w0] and update ssh private key"
    - echo "${SSH_PRIVATE_KEY}" | base64 -d > ~/.ssh/id_rsa
    - chmod 600 ~/.ssh/id_rsa
  script:
    - ssh "${TARGET_USER}"@"${TARGET_IP}" echo "Hello World !"
```

## Credits

This repo is inspired by [kroniak](https://github.com/kroniak/alpine-ssh-client)
