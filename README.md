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
#	(Download, Build and Install linux)
#	(Download, Build and Install libc)
#	(Download, Build and Install libasm)
#	(Download, Build and Install coreutils)
#	(Download, Build and Install edt)
make -f src/Makefile
```

### Download, Configure, Build and Install linux

```sh
# Download
make -f src/Makefile src/linux

# Install (kernel-headers) -- Download if directory does not exist
make -f src/Makefile usr/include/linux

# Configure (kernel) -- Download if directory does not exist

make -f src/Makefile src/linux/.config

# Build and Install (kernel) -- Download and Configure if directory does not exist
make -f src/Makefile boot/bzImage
```

### Download, Build and Install libc

```sh
# Download
make -f src/Makefile src/libc

# Build and Install -- Download if directory does not exist
make -f src/Makefile usr/lib/libc.a
```

### Download, Build and Install libasm

```sh
# Download
make -f src/Makefile src/libasm

# Build and Install -- Download if directory does not exist
make -f src/Makefile usr/lib/libasm.a
```

### Download, Build and Install coreutils

```sh
# Download
make -f src/Makefile src/coreutils

# Build and Install -- Download if directory does not exist
make -f src/Makefile usr/bin/coreutils
```

### Download, Build and Install edt

```sh
# Download
make -f src/Makefile src/edt

# Build and Install -- Download if directory does not exist
make -f src/Makefile usr/bin/edt
```
