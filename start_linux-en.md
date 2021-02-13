# Linux Platform Development Environment

Note: Linux platform compilation tools only support 64-bit Linux operating
systems.

# Get Compiler Tool Chain for Linux

    wget http://shyboy.oss-cn-shenzhen.aliyuncs.com/readonly/tc32_gcc_v2.0.tar.bz2

Unpack to `/opt`.  It will create its own subdirectory, `tc32`.  (You can also
choose any other parent directory.)

    sudo tar -xvjf tc32_gcc_v2.0.tar.bz2 -C /opt/

Add the toolchain to environment variables (assuming you've unpacked it to
`/opt` as above):

    export PATH=$PATH:/opt/tc32/bin

The above command only takes effect in the current shell.  The best way to make
sure it's set in all future invocations of the shell is to add it to the end of
the `~/.bashrc` file.

Test whether the build is successful

    tc32-elf-gcc -v

If the build is successful, the following information will be printed:

    Using built-in specs.
    COLLECT_GCC=tc32-elf-gcc
    COLLECT_LTO_WRAPPER=/opt/tc32/lib/gcc/tc32-elf/4.5.1.tc32-elf-1.5/lto-wrapper
    Target: tc32-elf
    Configured with: ../../gcc-4.5.1/configure --program-prefix=tc32-elf- --target=tc32-elf --prefix=/opt/tc32 --enable-languages=c - libexecdir=/opt/tc32/lib --with-gnu-as --with-gnu-ld --without-headers --disable-decimal-float --disable-nls --disable-mathvec --with-pkgversion= 'Telink TC32 version 2.0 build' --without-docdir --without-fp --without-tls --disable-shared --disable-threads --disable-libffi --disable-libquadmath --disable-libstdcxx-pch- -disable-libmudflap --disable-libgomp --disable-libssp -v --without-docdir --enable-soft-float --with-newlib --with-gcc --with-gnu- --with-gmp= /opt/tc32/addontools --with-mpc=/opt/tc32/addontools --with-mpfr=/opt/tc32/addontools
    Thread model: single
    gcc version 4.5.1.tc32-elf-1.5 (Telink TC32 version 2.0 build) 

# Install Python and pyserial

The programming tool is written in Python, so make sure your computer has
Python and the required dependency package `pyserial`

Check if your computer has Python installed:

    python -v

If Python has been installed correctly, you also need to install `pyserial`.
One method is:

    pip install pyserial
