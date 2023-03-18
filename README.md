[![Build action](https://github.com/tuananh/apko-image-template/actions/workflows/release.yaml/badge.svg)](https://github.com/tuananh/apko-image-template/actions/workflows/release.yaml)

# OCI Image included postgres-15-dev and azcopy which built from source by melange and apko

## Usage

```
docker pull ghcr.io/hungran/pg_dump_azcopy:latest
docker run -it ghcr.io/hungran/pg_dump_azcopy:latest /usr/bin/pg_dump ...
docker run -it ghcr.io/hungran/pg_dump_azcopy:latest /usr/local/bin/azure-storage-azcopy ...
docker run -it azcopy-postgres:test sh
```
## DIY
### Build apk
```sh
docker run --privileged --rm -v "${PWD}":/work \
  cgr.dev/chainguard/melange build azcopy.melange.yaml \
  --arch x86_64, aarch64 \
  --signing-key melange.rsa
```
### Build OCI Image
```sh
docker run --rm -v ${PWD}:/work cgr.dev/chainguard/apko \
  build latest.apko.yaml azcopy-postgres:test azcopy-postgres.tar \
  -k melange.rsa.pub
```  
### Load Image
```sh
docker load < azcopy-postgres.tar
```

