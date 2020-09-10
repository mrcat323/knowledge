## Creating swap memory

For instance you do live in such server as **2x2200** with **1gb ram** and you must create a swap memory, I mean, it's for example impossible to use [composer](https://getcomposer.org/) because of this error:

```prolog
Failed to allocate memory
```

or something like that, I'll update this note a bit later. So there is only one solution for that:

> Dude, do create a swap

Let's go:

First let's make sure we got swap memory, to do that, just say:

```bash
free -m | grep Swap
```

If there is no swap mem there, which means we need to create it:

```bash
dd if=/dev/zero of=/var/swap.1 bs=1M count=1024
mkswap /var/swap.1
swapon /var/swap.1
```

here, with `dd` command which is incredibly powerful command, we're grabbing with 1024 times giving 1M to *swap.1* file (like, from nowhere), another job is we need to make it as swap, `mkswap` does its job, and `swapon`makes sure where the swapping to take place.

If this solution does not work, then try to create a swap file:

```bash
fallocate -l 1G /swapfile
chmod 600 /swapfile
mkswap /swapfile
swapon /swapfile
```

`fallocate` emits a memory for certain things, `swap`is a memory which locates in harddrive, so the `-l` which `--length`tells `fallocate`how much we do want.

`chmod 600 /swapfile` - makes our */swapfile* **read-only**. 

The other two commands you do know.
