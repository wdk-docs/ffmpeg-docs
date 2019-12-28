.. _libswscale:

Libswscale Documentation
===============================

Table of Contents
1 Description
2 See Also
3 Authors
1 Description
The libswscale library performs highly optimized image scaling and colorspace and pixel format conversion operations.

Specifically, this library performs the following conversions:

Rescaling: is the process of changing the video size. Several rescaling options and algorithms are available. This is usually a lossy process.
Pixel format conversion: is the process of converting the image format and colorspace of the image, for example from planar YUV420P to RGB24 packed. It also handles packing conversion, that is converts from packed layout (all pixels belonging to distinct planes interleaved in the same buffer), to planar layout (all samples belonging to the same plane stored in a dedicated buffer or "plane").
This is usually a lossy process in case the source and destination colorspaces differ.

2 See Also
ffmpeg, ffplay, ffprobe, ffmpeg-scaler, libavutil

3 Authors
The FFmpeg developers.

For details about the authorship, see the Git history of the project (git://source.ffmpeg.org/ffmpeg), e.g. by typing the command git log in the FFmpeg source directory, or browsing the online repository at http://source.ffmpeg.org.

Maintainers for the specific components are listed in the file MAINTAINERS in the source code tree.

This document was generated on June 8, 2019 using makeinfo.
