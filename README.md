# JD297/Linux

Linux distribution with own implementation of libc and coreutils.

## Install

Instead of distribute an iso file this distribution is build from scratch with the Makefile and the utility make.

### make

The src/Makefile has the following targets:

### Clean

```sh
make -f src/Makefile clean
```

### All

```sh
# SEE
#	(Download and Install (headers) linux)
#	(Download, Build and Install libc)
make -f src/Makefile
```

### Download and Install (headers) linux

```sh
# Download
make -f src/Makefile src/linux

# Install (headers)
make -f src/Makefile usr/include/linux
```

### Download, Build and Install libc

```sh
# Download
make -f src/Makefile src/libc

# Build and Install -- Download if directory does not exist
make -f src/Makefile usr/lib/libc.so
```

# Download and Install coreutils

```sh
# Download
make -f src/Makefile src/coreutils

# Install
make -f src/Makefile usr/bin/sh
```
