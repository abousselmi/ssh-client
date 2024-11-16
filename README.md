# Tiny SSH client (openssh-client)

## Alpine image

[![Docker Repository on Quay](https://quay.io/repository/abousselmi/ssh-client-alpine/status "Docker Repository on Quay")](https://quay.io/repository/abousselmi/ssh-client-alpine)

## Bitnami Minideb image

[![Docker Repository on Quay](https://quay.io/repository/abousselmi/ssh-client-minideb/status "Docker Repository on Quay")](https://quay.io/repository/abousselmi/ssh-client-minideb)

## Gitlab-CI sample

```yaml
ssh-to-server:
  stage: ssh
  image:
    quay.io/abousselmi/ssh-client-alpine
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

## Run it

```console
# Alpine
docker run -it --rm quay.io/abousselmi/ssh-client-alpine sh

# Minideb
docker run -it --rm quay.io/abousselmi/ssh-client-minideb sh
```

## Credits

This repo is inspired by [kroniak](https://github.com/kroniak/alpine-ssh-client)