---
title: Slurm
---

# Slurm!
## Containers
Thanks to [pyxis](https://github.com/NVIDIA/pyxis/) you can use 
[NVIDIA NGC](https://ngc.nvidia.com/catalog) containers with `srun` 
commands with the `--container-image` flag, for example 
`--container-image="nvcr.io#nvidia/pytorch:21.08-py3"`. By specifying 
`--container-name` and `--container-writable` you get a persistent, writeable
container you can setup and reuse. For example:

`srun --container-image="nvcr.io#nvidia/pytorch:21.08-py3" --container-name=test 
--container-writable pip install something`

On the next invocation only the container name is needed to invoke your persistent 
container:
```
srun --container-name=test --container-writable python script.py
```

### Permission error
You might get an error like `mkdir: cannot create directory ‘/run/user/11183’: Permission denied` 
when using enroot or pyxis.  Try 
```
unset XDG_RUNTIME_DIR
``` 
or setting it to something
you can access, if you have problems with that.

## Working directory

For an `srun` command set the working directory with the `--container-workdir=DIR`
option.

## Interactive
You can use `salloc` to get an interactive terminal, but if you need to connect 
to an `srun` command use the `--pty` flag like so:

`srun -A <account> -p voodoo -w a6k5-01 --pty bash`

