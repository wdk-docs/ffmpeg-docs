Platform Specific Information
=====================================

Table of Contents
1 Unix-like
1.1 Advanced linking configuration
1.2 BSD
1.3 (Open)Solaris
1.4 Darwin (Mac OS X, iPhone)
2 DOS
3 OS/2
4 Windows
4.1 Native Windows compilation using MinGW or MinGW-w64
4.1.1 Native Windows compilation using MSYS2
4.2 Microsoft Visual C++ or Intel C++ Compiler for Windows
4.2.1 Linking to FFmpeg with Microsoft Visual C++
4.3 Cross compilation for Windows with Linux
4.4 Compilation under Cygwin
4.5 Crosscompilation for Windows under Cygwin
1 Unix-like
Some parts of FFmpeg cannot be built with version 2.15 of the GNU assembler which is still provided by a few AMD64 distributions. To make sure your compiler really uses the required version of gas after a binutils upgrade, run:

$(gcc -print-prog-name=as) --version
If not, then you should install a different compiler that has no hard-coded path to gas. In the worst case pass --disable-asm to configure.

1.1 Advanced linking configuration
If you compiled FFmpeg libraries statically and you want to use them to build your own shared library, you may need to force PIC support (with --enable-pic during FFmpeg configure) and add the following option to your project LDFLAGS:

-Wl,-Bsymbolic
If your target platform requires position independent binaries, you should pass the correct linking flag (e.g. -pie) to --extra-ldexeflags.

1.2 BSD
BSD make will not build FFmpeg, you need to install and use GNU Make (gmake).

1.3 (Open)Solaris
GNU Make is required to build FFmpeg, so you have to invoke (gmake), standard Solaris Make will not work. When building with a non-c99 front-end (gcc, generic suncc) add either --extra-libs=/usr/lib/values-xpg6.o or --extra-libs=/usr/lib/64/values-xpg6.o to the configure options since the libc is not c99-compliant by default. The probes performed by configure may raise an exception leading to the death of configure itself due to a bug in the system shell. Simply invoke a different shell such as bash directly to work around this:

bash ./configure
1.4 Darwin (Mac OS X, iPhone)
The toolchain provided with Xcode is sufficient to build the basic unaccelerated code.

Mac OS X on PowerPC or ARM (iPhone) requires a preprocessor from https://github.com/FFmpeg/gas-preprocessor or https://github.com/yuvi/gas-preprocessor(currently outdated) to build the optimized assembly functions. Put the Perl script somewhere in your PATH, FFmpeg’s configure will pick it up automatically.

Mac OS X on amd64 and x86 requires nasm to build most of the optimized assembly functions. Fink, Gentoo Prefix, Homebrew or MacPorts can easily provide it.

2 DOS
Using a cross-compiler is preferred for various reasons. http://www.delorie.com/howto/djgpp/linux-x-djgpp.html

3 OS/2
For information about compiling FFmpeg on OS/2 see http://www.edm2.com/index.php/FFmpeg.

4 Windows
To get help and instructions for building FFmpeg under Windows, check out the FFmpeg Windows Help Forum at http://ffmpeg.zeranoe.com/forum/.

4.1 Native Windows compilation using MinGW or MinGW-w64
FFmpeg can be built to run natively on Windows using the MinGW-w64 toolchain. Install the latest versions of MSYS2 and MinGW-w64 from http://msys2.github.io/ and/or http://mingw-w64.sourceforge.net/. You can find detailed installation instructions in the download section and the FAQ.

Notes:

Building for the MSYS environment is discouraged, MSYS2 provides a full MinGW-w64 environment through mingw64_shell.bat or mingw32_shell.bat that should be used instead of the environment provided by msys2_shell.bat.
Building using MSYS2 can be sped up by disabling implicit rules in the Makefile by calling make -r instead of plain make. This speed up is close to non-existent for normal one-off builds and is only noticeable when running make for a second time (for example during make install).
In order to compile FFplay, you must have the MinGW development library of SDL and pkg-config installed.
By using ./configure --enable-shared when configuring FFmpeg, you can build the FFmpeg libraries (e.g. libavutil, libavcodec, libavformat) as DLLs.
4.1.1 Native Windows compilation using MSYS2
The MSYS2 MinGW-w64 environment provides ready to use toolchains and dependencies through pacman.

Make sure to use mingw64_shell.bat or mingw32_shell.bat to have the correct MinGW-w64 environment. The default install provides shortcuts to them under MinGW-w64 Win64 Shell and MinGW-w64 Win32 Shell.

# normal msys2 packages
pacman -S make pkgconf diffutils

# mingw-w64 packages and toolchains
pacman -S mingw-w64-x86_64-nasm mingw-w64-x86_64-gcc mingw-w64-x86_64-SDL2
To target 32 bits replace x86_64 with i686 in the command above.

4.2 Microsoft Visual C++ or Intel C++ Compiler for Windows
FFmpeg can be built with MSVC 2013 or later.

You will need the following prerequisites:

MSYS2
NASM (Also available via MSYS2’s package manager.)
To set up a proper environment in MSYS2, you need to run msys_shell.bat from the Visual Studio or Intel Compiler command prompt.

Place yasm.exe somewhere in your PATH.

Next, make sure any other headers and libs you want to use, such as zlib, are located in a spot that the compiler can see. Do so by modifying the LIB and INCLUDE environment variables to include the Windows-style paths to these directories. Alternatively, you can try to use the --extra-cflags/--extra-ldflags configure options.

Finally, run:

For MSVC:
./configure --toolchain=msvc

For ICL:
./configure --toolchain=icl

make
make install
If you wish to compile shared libraries, add --enable-shared to your configure options. Note that due to the way MSVC and ICL handle DLL imports and exports, you cannot compile static and shared libraries at the same time, and enabling shared libraries will automatically disable the static ones.

Notes:

If you wish to build with zlib support, you will have to grab a compatible zlib binary from somewhere, with an MSVC import lib, or if you wish to link statically, you can follow the instructions below to build a compatible zlib.lib with MSVC. Regardless of which method you use, you must still follow step 3, or compilation will fail.
Grab the zlib sources.
Edit win32/Makefile.msc so that it uses -MT instead of -MD, since this is how FFmpeg is built as well.
Edit zconf.h and remove its inclusion of unistd.h. This gets erroneously included when building FFmpeg.
Run nmake -f win32/Makefile.msc.
Move zlib.lib, zconf.h, and zlib.h to somewhere MSVC can see.
FFmpeg has been tested with the following on i686 and x86_64:
Visual Studio 2013 Pro and Express
Intel Composer XE 2013
Intel Composer XE 2013 SP1
Anything else is not officially supported.

4.2.1 Linking to FFmpeg with Microsoft Visual C++
If you plan to link with MSVC-built static libraries, you will need to make sure you have Runtime Library set to Multi-threaded (/MT) in your project’s settings.

You will need to define inline to something MSVC understands:

#define inline __inline
Also note, that as stated in Microsoft Visual C++, you will need an MSVC-compatible inttypes.h.

If you plan on using import libraries created by dlltool, you must set References to No (/OPT:NOREF) under the linker optimization settings, otherwise the resulting binaries will fail during runtime. This is not required when using import libraries generated by lib.exe. This issue is reported upstream at http://sourceware.org/bugzilla/show_bug.cgi?id=12633.

To create import libraries that work with the /OPT:REF option (which is enabled by default in Release mode), follow these steps:

Open the Visual Studio Command Prompt.
Alternatively, in a normal command line prompt, call vcvars32.bat which sets up the environment variables for the Visual C++ tools (the standard location for this file is something like C:\Program Files (x86_\Microsoft Visual Studio 10.0\VC\bin\vcvars32.bat).

Enter the bin directory where the created LIB and DLL files are stored.
Generate new import libraries with lib.exe:
lib /machine:i386 /def:..\lib\foo-version.def  /out:foo.lib
Replace foo-version and foo with the respective library names.

4.3 Cross compilation for Windows with Linux
You must use the MinGW cross compilation tools available at http://www.mingw.org/.

Then configure FFmpeg with the following options:

./configure --target-os=mingw32 --cross-prefix=i386-mingw32msvc-
(you can change the cross-prefix according to the prefix chosen for the MinGW tools).

Then you can easily test FFmpeg with Wine.

4.4 Compilation under Cygwin
Please use Cygwin 1.7.x as the obsolete 1.5.x Cygwin versions lack llrint() in its C library.

Install your Cygwin with all the "Base" packages, plus the following "Devel" ones:

binutils, gcc4-core, make, git, mingw-runtime, texinfo
In order to run FATE you will also need the following "Utils" packages:

diffutils
If you want to build FFmpeg with additional libraries, download Cygwin "Devel" packages for Ogg and Vorbis from any Cygwin packages repository:

libogg-devel, libvorbis-devel
These library packages are only available from Cygwin Ports:

yasm, libSDL-devel, libgsm-devel, libmp3lame-devel,
speex-devel, libtheora-devel, libxvidcore-devel
The recommendation for x264 is to build it from source, as it evolves too quickly for Cygwin Ports to be up to date.

4.5 Crosscompilation for Windows under Cygwin
With Cygwin you can create Windows binaries that do not need the cygwin1.dll.

Just install your Cygwin as explained before, plus these additional "Devel" packages:

gcc-mingw-core, mingw-runtime, mingw-zlib
and add some special flags to your configure invocation.

For a static build run

./configure --target-os=mingw32 --extra-cflags=-mno-cygwin --extra-libs=-mno-cygwin
and for a build with shared libraries

./configure --target-os=mingw32 --enable-shared --disable-static --extra-cflags=-mno-cygwin --extra-libs=-mno-cygwin
This document was generated on June 11, 2019 using makeinfo.
