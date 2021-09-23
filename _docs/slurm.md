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
## Interactive
You can use `salloc` to get an interactive terminal, but if you need to connect 
to an `srun` command use the `--pty` flag like so:

`srun -A <account> -p voodoo -w a6k5-01 --pty bash`

