# Scaleway CoreOS builder

Build a CoreOS image from scratch on Scaleway (https://www.scaleway.com/) using
packer.

ScalewayCLI must be configured before building an image.

After its creation, the instance is rebooted in _rescue mode_ using scaleway
CLI.

While in rescue mode, the root filesystem is not mounted, therefore allowing
CoreOS installation to run on /dev/vda.

## Usage

```
cp secrets.example.json secrets.json
vim secrets.json
docker build -t scaleway-coreos .
docker run -it \
  -v $(pwd)/secrets.json:/srv/secrets.json \
  -v $HOME/.scwrc:/root/.scwrc \
  scaleway-coreos
```

A default CoreOS Ignition configuration is burned into the image.  You can
change this configuration by mounting your config.yaml at
`/usr/local/src/app/config.yaml`, at run.

It will be transpiled into JSON using
https://github.com/coreos/container-linux-config-transpiler.

