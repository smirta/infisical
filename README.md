# infisical
Test run [infisical](https://infisical.com) in podman. Some modifications to let it run on unprivleged ports and some selinux relabelling are required.

```bash
diff docker-compose.yml podman-compose.yml 
```
```bash
9,10c9,10
<       - 80:80
<       - 443:443
---
>       - 8080:80
>       - 8443:443
12c12
<       - ./nginx/default.conf:/etc/nginx/conf.d/default.conf:ro
---
>       - ./nginx/default.conf:/etc/nginx/conf.d/default.conf:ro,Z
```

## Install from scratch for running in podman

1. Fetch docker-compose.yml, default.conf and .env according to
https://infisical.com/docs/self-hosting/deployment-options/docker-compose#download-the-required-files

1. Apply patch
    ```bash
    echo "
    9,10c9,10
    <       - 80:80
    <       - 443:443
    ---
    >       - 8080:80
    >       - 8443:443
    12c12
    <       - ./nginx/default.conf:/etc/nginx/conf.d/default.conf:ro
    ---
    >       - ./nginx/default.conf:/etc/nginx/conf.d/default.conf:ro,Z
    " | patch docker-compose.yml - 
    ```

1. run it
    ```bash
    podman-compose -f docker-compose.yml up -d
    ```

## Current status
This is just a playground to find out more about [infisical](https://infisical.com). Only modified files are submitted to this repository.
