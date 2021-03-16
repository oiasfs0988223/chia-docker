#Official Chia Docker Container
Currently latest = head of dev branch, tagged releases to come shortly


## Initialize
```
docker run --name chia (chia-farmer, chia-harvester1 etc.) -d chia:latest (optional -v /path/to/plots:plots)
```

## Config management
```
docker exec -it chia /bin/bash
vim (or nano if you prefer) ~/.chia/testnet/config/config.yaml
```

modify the line
```
self_hostname: &self_hostname "localhost"
```
to match
```
self_hostname: &self_hostname "127.0.0.1"
```

#### optional: remote harvester

```
 harvester:
  # The harvester server (if run) will run on this port
  port: 8448
  farmer_peer:
    host: *self_hostname
    port: 8447
```
include the proper host and port for your remote farmer node or container.

## Starting Chia Blockchain
remain in the container with a bash shell

Activate venv
```
. ./activate
```

If you have your own keys
```
chia keys add (follow prompt)
echo "keys" | chia keys add -
```

To generate keys
```
chia keys generate
```

If added the optional plots earlier

```
chia plots add -d /plots
```

you can start chia as normal or

```
chia start farmer
optional single purpose node
(chia start farmer-only)
(chia start harvester)
```

drop from shell, leave running Container
```
exit
```
