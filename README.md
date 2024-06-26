# helm registry mirrors

This helm chart deploys multiple registry mirrors for major registries.

By default:
- `docker.io` => https://mirror-docker-io.{ingress.suffix}
- `quay.io`=> https://mirror-quay-io.{ingress.suffix}
- `grc.io` =>  https://mirror-grc-io.{ingress.suffix}
- `ghcr.io` =>  https://mirror-ghcr-io.{ingress.suffix}
- `public.ecr.aws` =>  https://mirror-public-ecr-aws.{ingress.suffix}


## Parameters

| Name                     | Description                                   | Value                                                                       |
| ------------------------ | --------------------------------------------- | --------------------------------------------------------------------------- |
| `mirrors`                | Array of mirrors (see bellow mirrors.0.[...]) | `[{dockerDef}, {quayDef}, {gcrDef}, {ghcrDef}, {publicEcrAwsDef}]`          |
| `mirrors.0.name`         | name of the mirror                            | `docker.io`                                                                 |
| `mirrors.0.remoteUrl`    | URL of the mirror                             | `https://registry-1.docker.io`                                              |
| `mirrors.0.storage.size` | Size of the volume to allocate                | inherited from `default.storage.size`                                       |
| `mirrors.0.resources`    | Resource limits and requests                  | inherited from `default.resources`                                          |
| `default.storage.size`   | Default size of the volume to allocate        | `20G`                                                                       |
| `default.resources`      | Default resource limits and requests          | `{limits: {memory: 500Mi, cpu: "1"}, requests: {memory: 50Mi, cpu: "10m"}}` |
| `ingress.suffix`         | suffix to add to `mirrors.0.name`             | `example.org`                                                               |
| `ingress.className`      | Ingress class name                            | `""`                                                                        |
| `ingress.annotations`    | annotations to add to Ingress manifests       | `{}`                                                                        |


## Notes

In my case, `traefik` is used as ingress and `cert-manager` is used to handle a wildcard certificate.
Some tweaks might be added go generalize this chart.

