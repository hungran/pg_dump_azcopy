[![Build action](https://github.com/tuananh/apko-image-template/actions/workflows/release.yaml/badge.svg)](https://github.com/tuananh/apko-image-template/actions/workflows/release.yaml)


docker run --privileged --rm -v "${PWD}":/work \
  cgr.dev/chainguard/melange build melange.yaml \
  --arch x86,amd64 \
  --signing-key melange.rsa

docker run --rm -v ${PWD}:/work cgr.dev/chainguard/apko \
  build latest.apko.yaml azcopy-postgres:test azcopy-postgres.tar \
  -k melange.rsa.pub