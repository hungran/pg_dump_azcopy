[![Build action](https://github.com/tuananh/apko-image-template/actions/workflows/release.yaml/badge.svg)](https://github.com/tuananh/apko-image-template/actions/workflows/release.yaml)

# OCI Image included postgres-15-dev and azcopy which built from source by melange and apko

<img width="901" alt="image" src="https://user-images.githubusercontent.com/26101787/226110778-db53f139-64dc-459f-9b00-97a9e735e9e7.png">
<img width="956" alt="image" src="https://user-images.githubusercontent.com/26101787/226110804-0104eea0-c92c-4f3f-bb70-10fb8b3b21df.png">
<img width="636" alt="image" src="https://user-images.githubusercontent.com/26101787/226110842-c52581b0-fcaa-49d2-b291-9bf6ef8f7997.png">


## Usage

```
docker pull ghcr.io/hungran/pg_dump_azcopy:latest
docker run -it ghcr.io/hungran/pg_dump_azcopy:latest /usr/bin/pg_dump --help
docker run -it ghcr.io/hungran/pg_dump_azcopy:latest /usr/local/bin/azure-storage-azcopy --help
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

