News
============

November 6th, 2018, FFmpeg 4.1 "al-Khwarizmi"
--------------------------------------------------------------------------------------------------------------

FFmpeg 4.1 "al-Khwarizmi", a new major release, is now available! Some of the highlights:

- deblock filter
- tmix filter
- amplify filter
- fftdnoiz filter
- aderivative and aintegral audio filters
- pal75bars and pal100bars video filter sources
- mbedTLS based TLS support
- adeclick and adeclip filters
- libtensorflow backend for DNN based filters like srcnn
- VC1 decoder is now bit-exact
- ATRAC9 decoder
- lensfun wrapper filter
- colorconstancy filter
- AVS2 video decoder via libdavs2
- IMM4 video decoder
- Brooktree ProSumer video decoder
- MatchWare Screen Capture Codec decoder
- WinCam Motion Video decoder
- 1D LUT filter (lut1d)
- RemotelyAnywhere Screen Capture decoder
- cue and acue filters
- Support for AV1 in MP4 and Matroska/WebM
- transpose_npp filter
- AVS2 video encoder via libxavs2
- amultiply filter
- Block-Matching 3d (bm3d) denoising filter
- acrossover filter
- ilbc decoder
- audio denoiser as afftdn filter
- AV1 parser
- sinc audio filter source
- chromahold filter
- setparams filter
- vibrance filter
- S12M timecode decoding in h264
- xstack filter
- (a)graphmonitor filter
- yadif_cuda filter

We strongly recommend users, distributors, and system integrators to upgrade unless they use current git master.

April 20th, 2018, FFmpeg 4.0 "Wu"
--------------------------------------------------------------------------------------------------------------

FFmpeg 4.0 "Wu", a new major release, is now available! Some of the highlights:

- Bitstream filters for editing metadata in H.264, HEVC and MPEG-2 streams
- Experimental MagicYUV encoder
- TiVo ty/ty+ demuxer
- Intel QSV-accelerated MJPEG encoding
- native aptX and aptX HD encoder and decoder
- NVIDIA NVDEC-accelerated H.264, HEVC, MJPEG, MPEG-1/2/4, VC1, VP8/9 hwaccel decoding
- Intel QSV-accelerated overlay filter
- mcompand audio filter
- acontrast audio filter
- OpenCL overlay filter
- video mix filter
- video normalize filter
- audio lv2 wrapper filter
- VAAPI MJPEG and VP8 decoding
- AMD AMF H.264 and HEVC encoders
- video fillborders filter
- video setrange filter
- support LibreSSL (via libtls)
- Dropped support for building for Windows XP. The minimum supported Windows version is Windows Vista.
- deconvolve video filter
- entropy video filter
- hilbert audio filter source
- aiir audio filter
- Removed the ffserver program
- Removed the ffmenc and ffmdec muxer and demuxer
- VideoToolbox HEVC encoder and hwaccel
- VAAPI-accelerated ProcAmp (color balance), denoise and sharpness filters
- Add android_camera indev
- codec2 en/decoding via libcodec2
- native SBC encoder and decoder
- drmeter audio filter
- hapqa_extract bitstream filter
- filter_units bitstream filter
- AV1 Support through libaom
- E-AC-3 dependent frames support
- bitstream filter for extracting E-AC-3 core
- Haivision SRT protocol via libsrt
- vfrdet filter

We strongly recommend users, distributors, and system integrators to upgrade unless they use current git master.

October 15th, 2017, FFmpeg 3.4 "Cantor"
--------------------------------------------------------------------------------------------------------------

FFmpeg 3.4 "Cantor", a new major release, is now available! Some of the highlights:

- deflicker video filter
- doubleweave video filter
- lumakey video filter
- pixscope video filter
- oscilloscope video filter
- update cuvid/nvenc headers to Video Codec SDK 8.0.14
- afir audio filter
- scale_cuda CUDA based video scale filter
- librsvg support for svg rasterization
- crossfeed audio filter
- spec compliant VP9 muxing support in MP4
- surround audio filter
- sofalizer filter switched to libmysofa
- Gremlin Digital Video demuxer and decoder
- headphone audio filter
- superequalizer audio filter
- roberts video filter
- additional frame format support for Interplay MVE movies
- support for decoding through D3D11VA in ffmpeg
- limiter video filter
- libvmaf video filter
- Dolby E decoder and SMPTE 337M demuxer
- unpremultiply video filter
- tlut2 video filter
- floodfill video filter
- pseudocolor video filter
- raw G.726 muxer and demuxer, left- and right-justified
- NewTek NDI input/output device
- FITS demuxer and decoder
- FITS muxer and encoder
- despill video filter
- haas audio filter
- SUP/PGS subtitle muxer
- convolve video filter
- VP9 tile threading support
- KMS screen grabber
- CUDA thumbnail filter
- V4L2 mem2mem HW assisted codecs
- Rockchip MPP hardware decoding
- vmafmotion video filter

We strongly recommend users, distributors, and system integrators to upgrade unless they use current git master.

April 13th, 2017, FFmpeg 3.3 "Hilbert"
--------------------------------------------------------------------------------------------------------------

FFmpeg 3.3 "Hilbert", a new major release, is now available! Some of the highlights:

- Apple Pixlet decoder
- NewTek SpeedHQ decoder
- QDMC audio decoder
- PSD (Photoshop Document) decoder
- FM Screen Capture decoder
- ScreenPressor decoder
- XPM decoder
- DNxHR decoder fixes for HQX and high resolution videos
- ClearVideo decoder (partial)
- 16.8 and 24.0 floating point PCM decoder
- Intel QSV-accelerated VP8 video decoding
- native Opus encoder
- DNxHR 444 and HQX encoding
- Quality improvements for the (M)JPEG encoder
- VAAPI-accelerated MPEG-2 and VP8 encoding
- premultiply video filter
- abitscope multimedia filter
- readeia608 filter
- threshold filter
- midequalizer filter
- MPEG-7 Video Signature filter
- add internal ebur128 library, remove external libebur128 dependency
- Intel QSV video scaling and deinterlacing filters
- Sample Dump eXchange demuxer
- MIDI Sample Dump Standard demuxer
- Scenarist Closed Captions demuxer and muxer
- Support MOV with multiple sample description tables
- Pro-MPEG CoP #3-R2 FEC protocol
- Support for spherical videos
- CrystalHD decoder moved to new decode API
- configure now fails if autodetect-libraries are requested but not found

We strongly recommend users, distributors, and system integrators to upgrade unless they use current git master.

October 30th, 2016, Results: Summer Of Code 2016.
--------------------------------------------------------------------------------------------------------------

This has been a long time coming but we wanted to give a proper closure to our participation in this run of the program and it takes time. Sometimes it's just to get the final report for each project trimmed down, others, is finalizing whatever was still in progress when the program finished: final patches need to be merged, TODO lists stabilized, future plans agreed; you name it.

Without further ado, here's the silver-lining for each one of the projects we sought to complete during this Summer of Code season:

FFv1 (Mentor: Michael Niedermayer)
Stanislav Dolganov designed and implemented experimental support for motion estimation and compensation in the lossless FFV1 codec. The design and implementation is based on the snow video codec, which uses OBMC. Stanislav's work proved that significant compression gains can be achieved with inter frame compression. FFmpeg welcomes Stanislav to continue working beyond this proof of concept and bring its advances into the official FFV1 specification within the IETF.

Self test coverage (Mentor: Michael Niedermayer)
Petru Rares Sincraian added several self-tests to FFmpeg and successfully went through the in-some-cases tedious process of fine tuning tests parameters to avoid known and hard to avoid problems, like checksum mismatches due to rounding errors on the myriad of platforms we support. His work has improved the code coverage of our self tests considerably.

MPEG-4 ALS encoder implementation (Mentor: Thilo Borgmann)
Umair Khan updated and integrated the ALS encoder to fit in the current FFmpeg codebase. He also implemented a missing feature for the ALS decoder that enables floating-point sample decoding. FFmpeg support for MPEG-4 ALS has been improved significantly by Umair's work. We welcome him to keep maintaining his improvements and hope for great contributions to come.

Tee muxer improvements (Mentor: Marton Balint)
Ján Sebechlebský's generic goal was to improve the tee muxer so it tolerated blocking IO and allowed transparent error recovery. During the design phase it turned out that this functionality called for a separate muxer, so Ján spent his summer working on the so-called FIFO muxer, gradually fixing issues all over the codebase. He succeeded in his task, and the FIFO muxer is now part of the main repository, alongside several other improvements he made in the process.

TrueHD encoder (Mentor: Rostislav Pehlivanov)
Jai Luthra's objective was to update the out-of-tree and pretty much abandoned MLP (Meridian Lossless Packing) encoder for libavcodec and improve it to enable encoding to the TrueHD format. For the qualification period the encoder was updated such that it was usable and throughout the summer, successfully improved adding support for multi-channel audio and TrueHD encoding. Jai's code has been merged into the main repository now. While a few problems remain with respect to LFE channel and 32 bit sample handling, these are in the process of being fixed such that effort can be finally put in improving the encoder's speed and efficiency.

Motion interpolation filter (Mentor: Paul B Mahol)
Davinder Singh investigated existing motion estimation and interpolation approaches from the available literature and previous work by our own: Michael Niedermayer, and implemented filters based on this research. These filters allow motion interpolating frame rate conversion to be applied to a video, for example, to create a slow motion effect or change the frame rate while smoothly interpolating the video along the motion vectors. There's still work to be done to call these filters 'finished', which is rather hard all things considered, but we are looking optimistically at their future.

And that's it. We are happy with the results of the program and immensely thankful for the opportunity of working with such an amazing set of students. We can be a tough crowd but our mentors did an amazing job at hand holding our interns through their journey. Thanks also to Google for this wonderful program and to everyone that made room in their busy lives to help making GSoC2016 a success. See you in 2017!

September 24th, 2016, SDL1 support dropped.
Support for the SDL1 library has been dropped, due to it no longer being maintained (as of January, 2012) and it being superseded by the SDL2 library. As a result, the SDL1 output device has also been removed and replaced by an SDL2 implementation. Both the ffplay and opengl output devices have been updated to support SDL2.

August 9th, 2016, FFmpeg 3.1.2 "Laplace"
--------------------------------------------------------------------------------------------------------------

FFmpeg 3.1.2, a new point release from the 3.1 release branch, is now available! It fixes several bugs.

We recommend users, distributors, and system integrators, to upgrade unless they use current git master.

July 10th, 2016, ffserver program being dropped
--------------------------------------------------------------------------------------------------------------

After thorough deliberation, we're announcing that we're about to drop the ffserver program from the project starting with the next release. ffserver has been a problematic program to maintain due to its use of internal APIs, which complicated the recent cleanups to the libavformat library, and block further cleanups and improvements which are desired by API users and will be easier to maintain. Furthermore the program has been hard for users to deploy and run due to reliability issues, lack of knowledgable people to help and confusing configuration file syntax. Current users and members of the community are invited to write a replacement program to fill the same niche that ffserver did using the new APIs and to contact us so we may point users to test and contribute to its development.

July 1st, 2016, FFmpeg 3.1.1 "Laplace"
--------------------------------------------------------------------------------------------------------------

FFmpeg 3.1.1, a new point release from the 3.1 release branch, is now available! It mainly deals with a few ABI issues introduced in the previous release.

We strongly recommend users, distributors, and system integrators, especially those who experienced issues upgrading from 3.0, to upgrade unless they use current git master.

June 27th, 2016, FFmpeg 3.1 "Laplace"
--------------------------------------------------------------------------------------------------------------

FFmpeg 3.1 "Laplace", a new major release, is now available! Some of the highlights:

- DXVA2-accelerated HEVC Main10 decoding
- fieldhint filter
- loop video filter and aloop audio filter
- Bob Weaver deinterlacing filter
- firequalizer filter
- datascope filter
- bench and abench filters
- ciescope filter
- protocol blacklisting API
- MediaCodec H264 decoding
- VC-2 HQ RTP payload format (draft v1) depacketizer and packetizer
- VP9 RTP payload format (draft v2) packetizer
- AudioToolbox audio decoders
- AudioToolbox audio encoders
- coreimage filter (GPU based image filtering on OSX)
- libdcadec removed
- bitstream filter for extracting DTS core
- ADPCM IMA DAT4 decoder
- musx demuxer
- aix demuxer
- remap filter
- hash and framehash muxers
- colorspace filter
- hdcd filter
- readvitc filter
- VAAPI-accelerated format conversion and scaling
- libnpp/CUDA-accelerated format conversion and scaling
- Duck TrueMotion 2.0 Real Time decoder
- Wideband Single-bit Data (WSD) demuxer
- VAAPI-accelerated H.264/HEVC/MJPEG encoding
- DTS Express (LBR) decoder
- Generic OpenMAX IL encoder with support for Raspberry Pi
- IFF ANIM demuxer & decoder
- Direct Stream Transfer (DST) decoder
- loudnorm filter
- MTAF demuxer and decoder
- MagicYUV decoder
- OpenExr improvements (tile data and B44/B44A support)
- BitJazz SheerVideo decoder
- CUDA CUVID H264/HEVC decoder
- 10-bit depth support in native utvideo decoder
- libutvideo wrapper removed
- YUY2 Lossless Codec decoder
- VideoToolbox H.264 encoder

We strongly recommend users, distributors, and system integrators to upgrade unless they use current git master.

March 16th, 2016, Google Summer of Code
--------------------------------------------------------------------------------------------------------------

FFmpeg has been accepted as a Google Summer of Code open source organization. If you wish to participate as a student see our project ideas page. You can already get in contact with mentors and start working on qualification tasks as well as register at google and submit your project proposal draft. Good luck!

February 15th, 2016, FFmpeg 3.0 "Einstein"
--------------------------------------------------------------------------------------------------------------

FFmpeg 3.0 "Einstein", a new major release, is now available! Some of the highlights:

The native FFmpeg AAC encoder has seen extensive improvements and is no longer considered experimental
Removed support for libvo-aacenc and libaacplus
Over 30 new filters have been added
Many ASM optimizations
VP9 Hardware Acceleration (DXVA2 and VA-API)
Cineform HD decoder
New DCA decoder based on libdcadec with full support for DTS-HD extensions
As with all major releases expect major backward incompatible API/ABI changes
See the Changelog for a list of more updates
We strongly recommend users, distributors, and system integrators to upgrade unless they use current git master.

January 30, 2016, Removing support for two external AAC encoders
--------------------------------------------------------------------------------------------------------------

We have just removed support for VisualOn AAC encoder (libvo-aacenc) and libaacplus in FFmpeg master.

Even before marking our internal AAC encoder as stable, it was known that libvo-aacenc was of an inferior quality compared to our native one for most samples. However, the VisualOn encoder was used extensively by the Android Open Source Project, and we would like to have a tested-and-true stable option in our code base.

When first committed in 2011, libaacplus filled in the gap of encoding High Efficiency AAC formats (HE-AAC and HE-AACv2), which was not supported by any of the encoders in FFmpeg at that time.

The circumstances for both have changed. After the work spearheaded by Rostislav Pehlivanov and Claudio Freire, the now-stable FFmpeg native AAC encoder is ready to compete with much more mature encoders. The Fraunhofer FDK AAC Codec Library for Android was added in 2012 as the fourth supported external AAC encoder, and the one with the best quality and the most features supported, including HE-AAC and HE-AACv2.

Therefore, we have decided that it is time to remove libvo-aacenc and libaacplus. If you are currently using libvo-aacenc, prepare to transition to the native encoder (aac) when updating to the next version of FFmpeg. In most cases it is as simple as merely swapping the encoder name. If you are currently using libaacplus, start using FDK AAC (libfdk_aac) with an appropriate profile option to select the exact AAC profile that fits your needs. In both cases, you will enjoy an audible quality improvement and as well as fewer licensing headaches.

Enjoy!

January 16, 2016, FFmpeg 2.8.5, 2.7.5, 2.6.7, 2.5.10
--------------------------------------------------------------------------------------------------------------

We have made several new point releases (2.8.5, 2.7.5, 2.6.7, 2.5.10). They fix various bugs, as well as CVE-2016-1897 and CVE-2016-1898. Please see the changelog for each release for more details.

We recommend users, distributors and system integrators to upgrade unless they use current git master.

December 5th, 2015, The native FFmpeg AAC encoder is now stable!
After seven years the native FFmpeg AAC encoder has had its experimental flag removed and declared as ready for general use. The encoder is transparent at 128kbps for most samples tested with artifacts only appearing in extreme cases. Subjective quality tests put the encoder to be of equal or greater quality than most of the other encoders available to the public.

Licensing has always been an issue with encoding AAC audio as most of the encoders have had a license making FFmpeg unredistributable if compiled with support for them. The fact that there now exists a fully open and truly free AAC encoder integrated directly within the project means a lot to those who wish to use accepted and widespread standards.

The majority of the work done to bring the encoder up to quality was started during this year's GSoC by developer Claudio Freire and Rostislav Pehlivanov. Both continued to work on the encoder with the latter joining as a developer and mainainer, working on other parts of the project as well. Also, thanks to Kamedo2 who does comparisons and tests, the original authors and all past and current contributors to the encoder. Users are suggested and encouraged to use the encoder and provide feedback or breakage reports through our bug tracker.

October 13th, 2015, Telepoint & MediaHub are now supporting our project
--------------------------------------------------------------------------------------------------------------

A big thank you note goes to our newest supporters: MediaHub and Telepoint. Both companies have donated a dedicated server with free of charge internet connectivity. Here is a little bit about them in their own words:

Telepoint is the biggest carrier-neutral data center in Bulgaria. Located in the heart of Sofia on a cross-road of many Bulgarian and International networks, the facility is a fully featured Tier 3 data center that provides flexible customer-oriented colocation solutions (ranging from a server to a private collocation hall) and a high level of security.

MediaHub Ltd. is a Bulgarian IPTV platform and services provider which uses FFmpeg heavily since it started operating a year ago. "Donating to help keep FFmpeg online is our way of giving back to the community" .

Thanks Telepoint and MediaHub for their support!

September 29th, 2015, GSoC 2015 results
--------------------------------------------------------------------------------------------------------------

FFmpeg participated to the latest edition of the Google Summer of Code Project. FFmpeg got a total of 8 assigned projects, and 7 of them were successful.

We want to thank Google, the participating students, and especially the mentors who joined this effort. We're looking forward to participating in the next GSoC edition!

Below you can find a brief description of the final outcome of each single project.

Basic servers for network protocols, mentee: Stephan Holljes, mentor: Nicolas George
Stephan Holljes's project for this session of Google Summer of Code was to implement basic HTTP server features for libavformat, to complement the already present HTTP client and RTMP and RTSP server code.

The first part of the project was to make the HTTP code capable of accepting a single client;
it was completed partly during the qualification period and partly during the first week of the summer.
Thanks to this work, it is now possible to make a simple HTTP stream using the following commands::

    ffmpeg -i /dev/video0 -listen 1 -f matroska \
    -c:v libx264 -preset fast -tune zerolatency http://:8080
    ffplay http://localhost:8080/

The next part of the project was to extend the code to be able to accept several clients,
simultaneously or consecutively. Since libavformat did not have an API for that kind of task,
it was necessary to design one. This part was mostly completed before the midterm and applied shortly afterwards.
Since the ffmpeg command-line tool is not ready to serve several clients,
the test ground for that new API is an example program serving hard-coded content.

The last and most ambitious part of the project was to update ffserver to make use of the new API. It would prove that the API is usable to implement real HTTP servers, and expose the points where more control was needed. By the end of the summer, a first working patch series was undergoing code review.

Browsing content on the server, mentee: Mariusz Szczepańczyk, mentor: Lukasz Marek
Mariusz finished an API prepared by the FFmpeg community and implemented Samba directory listing as qualification task.

During the program he extended the API with the possibility to remove and rename files on remote servers. He completed the implementation of these features for file, Samba, SFTP, and FTP protocols.

At the end of the program, Mariusz provided a sketch of an implementation for HTTP directory listening.

Directshow digital video capture, mentee: Mate Sebok, mentor: Roger Pack
Mate was working on directshow input from digital video sources. He got working input from ATSC input sources, with specifiable tuner.

The code has not been committed, but a patch of it was sent to the ffmpeg-devel mailing list for future use.

The mentor plans on cleaning it up and committing it, at least for the ATSC side of things. Mate and the mentor are still working trying to finally figure out how to get DVB working.

Implementing full support for 3GPP Timed Text Subtitles, mentee: Niklesh Lalwani, mentor: Philip Langdale
Niklesh's project was to expand our support for 3GPP Timed Text subtitles. This is the native subtitle format for mp4 containers, and is interesting because it's usually the only subtitle format supported by the stock playback applications on iOS and Android devices.

ffmpeg already had basic support for these subtitles which ignored all formatting information - it just provided basic plain-text support.

Niklesh did work to add support on both the encode and decode side for text formatting capabilities, such as font size/colour and effects like bold/italics, highlighting, etc.

The main challenge here is that Timed Text handles formatting in a very different way from most common subtitle formats. It uses a binary encoding (based on mp4 boxes, naturally) and stores information separately from the text itself. This requires additional work to track which parts of the text formatting applies to, and explicitly dealing with overlapping formatting (which other formats support but Timed Text does not) so it requires breaking the overlapping sections into separate non-overlapping ones with different formatting.

Finally, Niklesh had to be careful about not trusting any size information in the subtitles - and that's no joke: the now infamous Android stagefright bug was in code for parsing Timed Text subtitles.

All of Niklesh's work is committed and was released in ffmpeg 2.8.

libswscale refactoring, mentee: Pedro Arthur, mentors: Michael Niedermayer, Ramiro Polla
Pedro Arthur has modularized the vertical and horizontal scalers. To do this he designed and implemented a generic filter framework and moved the existing scaler code into it. These changes now allow easily adding removing, splitting or merging processing steps. The implementation was benchmarked and several alternatives were tried to avoid speed loss.

He also added gamma corrected scaling support. An example to use gamma corrected scaling would be::

    ffmpeg -i input -vf scale=512:384:gamma=1 output

Pedro has done impressive work considering the short time available, and he is a FFmpeg committer now.
He continues to contribute to FFmpeg, and has fixed some bugs in libswscale after GSoC has ended.

AAC Encoder Improvements, mentee: Rostislav Pehlivanov, mentor: Claudio Freire
Rostislav Pehlivanov has implemented PNS, TNS, I/S coding and main prediction on the native AAC encoder.
Of all those extensions, only TNS was left in a less-than-usable state,
but the implementation has been pushed (disabled) anyway since it's a good basis for further improvements.

PNS replaces noisy bands with a single scalefactor representing the energy of that band, gaining in coding efficiency considerably, and the quality improvements on low bitrates are impressive for such a simple feature.

TNS still needs some polishing, but has the potential to reduce coding artifacts by applying noise shaping in the temporal domain (something that is a source of annoying, notable distortion on low-entropy bands).

Intensity Stereo coding (I/S) can double coding efficiency by exploiting strong correlation between stereo channels, most effective on pop-style tracks that employ panned mixing. The technique is not as effective on classic X-Y recordings though.

Finally, main prediction improves coding efficiency by exploiting correlation among successive frames. While the gains have not been huge at this point, Rostislav has remained active even after the GSoC, and is polishing both TNS and main prediction, as well as looking for further improvements to make.

In the process, the MIPS port of the encoder was broken a few times, something he's also working to fix.

Animated Portable Network Graphics (APNG), mentee: Donny Yang, mentor: Paul B Mahol
Donny Yang implemented basic keyframe only APNG encoder as the qualification task.
Later he wrote interframe compression via various blend modes. The current implementation tries all blend modes and picks one which takes the smallest amount of memory.

Special care was taken to make sure that the decoder plays correctly all files found in the wild and that the encoder produces files that can be played in browsers that support APNG.

During his work he was tasked to fix any encountered bug in the decoder due to the fact that it doesn't match APNG specifications. Thanks to this work, a long standing bug in the PNG decoder has been fixed.

For latter work he plans to continue working on the encoder, making it possible to select which blend modes will be used in the encoding process. This could speed up encoding of APNG files.

September 9th, 2015, FFmpeg 2.8
--------------------------------------------------------------------------------------------------------------

We published release 2.8 as new major version. It contains all features and bug fixes of the git master branch from September 8th. Please see the changelog for a list of the most important changes.

We recommend users, distributors and system integrators to upgrade unless they use current git master.

August 1st, 2015, A message from the FFmpeg project
--------------------------------------------------------------------------------------------------------------

Dear multimedia community,

The resignation of Michael Niedermayer as leader of FFmpeg yesterday has come by surprise.
He has worked tirelessly on the FFmpeg project for many years and we must thank him for the work that he has done.
We hope that in the future he will continue to contribute to the project. In the coming weeks,
the FFmpeg project will be managed by the active contributors.

The last four years have not been easy for our multimedia community - both contributors and users.
We should now look to the future, try to find solutions to these issues,
and to have reconciliation between the forks, which have split the community for so long.

Unfortunately, much of the disagreement has taken place in inappropriate venues so far,
which has made finding common ground and solutions difficult.
We aim to discuss this in our communities online over the coming weeks,
and in person at the VideoLAN Developer Days in Paris in September: a neutral venue for the entire open source multimedia community.

The FFmpeg project.

July 4th, 2015, FFmpeg needs a new host
--------------------------------------------------------------------------------------------------------------

UPDATE: We have received more than 7 offers for hosting and servers, thanks a lot to everyone!

After graciously hosting our projects (FFmpeg, MPlayer and rtmpdump) for 4 years, Arpi (our hoster) has informed us that we have to secure a new host somewhere else immediately.

If you want to host an open source project, please let us know, either on ffmpeg-devel mailing list or irc.freenode.net #ffmpeg-devel.

We use about 4TB of storage and at least 4TB of bandwidth / month for various mailing lists, trac, samples repo, svn, etc.

March 16, 2015, FFmpeg 2.6.1
--------------------------------------------------------------------------------------------------------------

We have made a new major release (2.6) and now one week afterward 2.6.1. It contains all features and bugfixes of the git master branch from the 6th March. Please see the Release Notes for a list of note-worthy changes.

We recommend users, distributors and system integrators to upgrade unless they use current git master.

March 4, 2015, Google Summer of Code
--------------------------------------------------------------------------------------------------------------

FFmpeg has been accepted as a Google Summer of Code Project. If you wish to participate as a student see our project ideas page. You can already get in contact with mentors and start working on qualification tasks. Registration at Google for students will open March 16th. Good luck!

March 1, 2015, Chemnitzer Linux-Tage
--------------------------------------------------------------------------------------------------------------

We happily announce that FFmpeg will be represented at Chemnitzer Linux-Tage (CLT) in Chemnitz, Germany. The event will take place on 21st and 22nd of March.

More information can be found here

We demonstrate usage of FFmpeg, answer your questions and listen to your problems and wishes. If you have media files that cannot be processed correctly with FFmpeg, be sure to have a sample with you so we can have a look!

For the first time in our CLT history, there will be an FFmpeg workshop! You can read the details here. The workshop is targeted at FFmpeg beginners. First the basics of multimedia will be covered. Thereafter you will learn how to use that knowledge and the FFmpeg CLI tools to analyse and process media files. The workshop is in German language only and prior registration is necessary. The workshop will be on Saturday starting at 10 o'clock.

We are looking forward to meet you (again)!

December 5, 2014, FFmpeg 2.5
--------------------------------------------------------------------------------------------------------------

We have made a new major release (2.5) It contains all features and bugfixes of the git master branch from the 4th December. Please see the Release Notes for a list of note-worthy changes.

We recommend users, distributors and system integrators to upgrade unless they use current git master.

October 10, 2014, FFmpeg is in Debian unstable again
--------------------------------------------------------------------------------------------------------------

We wanted you to know there are FFmpeg packages in Debian unstable again. A big thank-you to Andreas Cadhalpun and all the people that made it possible. It has been anything but simple.

Unfortunately that was already the easy part of this news. The bad news is the packages probably won't migrate to Debian testing to be in the upcoming release codenamed jessie. Read the argumentation over at Debian.

However things will come out in the end, we hope for your continued remarkable support!

October 8, 2014, FFmpeg secured a place in OPW!
--------------------------------------------------------------------------------------------------------------

Thanks to a generous 6K USD donation by Samsung (Open Source Group), FFmpeg will be welcoming at least 1 "Outreach Program for Women" intern to work with our community for an initial period starting December 2014 (through March 2015).

We all know FFmpeg is used by the industry, but even while there are countless products building on our code, it is not at all common for companies to step up and help us out when needed. So a big thank-you to Samsung and the OPW program committee!

If you are thinking on participating in OPW as an intern, please take a look at our OPW wiki page for some initial guidelines. The page is still a work in progress, but there should be enough information there to get you started. If you, on the other hand, are thinking on sponsoring work on FFmpeg through the OPW program, please get in touch with us at opw@ffmpeg.org. With your help, we might be able to secure some extra intern spots for this round!

September 15, 2014, FFmpeg 2.4
--------------------------------------------------------------------------------------------------------------

We have made a new major release (2.4) It contains all features and bugfixes of the git master branch from the 14th September. Please see the Release Notes for a list of note-worthy changes.

We recommend users, distributors and system integrators to upgrade unless they use current git master.

August 20, 2014, FFmpeg 2.3.3, 2.2.7, 1.2.8
--------------------------------------------------------------------------------------------------------------

We have made several new point releases (2.3.3, 2.2.7, 1.2.8). They fix various bugs, as well as CVE-2014-5271 and CVE-2014-5272. Please see the changelog for more details.

We recommend users, distributors and system integrators to upgrade unless they use current git master.

July 29, 2014, Help us out securing our spot in OPW
--------------------------------------------------------------------------------------------------------------

Following our previous post regarding our participation on this year's OPW (Outreach Program for Women), we are now reaching out to our users (both individuals and companies) to help us gather the needed money to secure our spot in the program.
We need to put together 6K USD as a minimum but securing more funds would help us towards getting more than one intern.
You can donate by credit card using Click&Pledge and selecting the "OPW" option. If you would like to donate by money transfer or by check, please get in touch by e-mail and we will get back to you with instructions.
Thanks!

July 20, 2014, New website
--------------------------------------------------------------------------------------------------------------

The FFmpeg project is proud to announce a brand new version of the website made by db0. While this was initially motivated by the need for a larger menu, the whole website ended up being redesigned, and most pages got reworked to ease navigation. We hope you'll enjoy browsing it.

July 17, 2014, FFmpeg 2.3
--------------------------------------------------------------------------------------------------------------

We have made a new major release (2.3) It contains all features and bugfixes of the git master branch from the 16th July. Please see the Release Notes for a list of note-worthy changes.

We recommend users, distributors and system integrators to upgrade unless they use current git master.

July 3, 2014, FFmpeg and the Outreach Program For Women
--------------------------------------------------------------------------------------------------------------

FFmpeg has started the process to become an OPW includer organization for the next round of the program, with internships starting December 9. The OPW aims to "Help women (cis and trans) and genderqueer to get involved in free and open source software". Part of the process requires securing funds to support at least one internship (6K USD), so if you were holding on your donation to FFmpeg, this is a great chance for you to come forward, get in touch and help both the project and a great initiative!

We have set up an email address you can use to contact us about donations and general inquires regarding our participation in the program. Hope to hear from you soon!

June 29, 2014, FFmpeg 2.2.4, 2.1.5, 2.0.5, 1.2.7, 1.1.12, 0.10.14
--------------------------------------------------------------------------------------------------------------

We have made several new point releases (2.2.4, 2.1.5, 2.0.5, 1.2.7, 1.1.12, 0.10.14). They fix a security issue in the LZO implementation, as well as several other bugs. See the git log for details.

We recommend users, distributors and system integrators to upgrade unless they use current git master.

May 1, 2014, LinuxTag
--------------------------------------------------------------------------------------------------------------

Once again FFmpeg will be represented at LinuxTag in Berlin, Germany. The event will take place from 8th to 10th of May. Please note that this year's LinuxTag is at a different location closer to the city center.

We will have a shared booth with XBMC and VideoLAN. If you have media files that cannot be processed correctly with FFmpeg, be sure to have a sample with you so we can have a look!

More information about LinuxTag can be found here

We are looking forward to see you in Berlin!

April 18, 2014, OpenSSL Heartbeat bug
--------------------------------------------------------------------------------------------------------------

Our server hosting the Trac issue tracker was vulnerable to the attack against OpenSSL known as "heartbleed". The OpenSSL software library was updated on 7th of April, shortly after the vulnerability was publicly disclosed. We have changed the private keys (and certificates) for all FFmpeg servers. The details were sent to the mailing lists by Alexander Strasser, who is part of the project server team. Here is a link to the user mailing list archive .

We encourage you to read up on "OpenSSL heartbleed". It is possible that login data for the issue tracker was exposed to people exploiting this security hole. You might want to change your password in the tracker and everywhere else you used that same password.

April 11, 2014, FFmpeg 2.2.1
--------------------------------------------------------------------------------------------------------------

We have made a new point releases (2.2.1). It contains bug fixes for Tickets #2893, #3432, #3469, #3486, #3495 and #3540 as well as several other fixes. See the git log for details.

March 24, 2014, FFmpeg 2.2
--------------------------------------------------------------------------------------------------------------

We have made a new major release (2.2) It contains all features and bugfixes of the git master branch from 1st March. A partial list of new stuff is below:

- HNM version 4 demuxer and video decoder
- Live HDS muxer
- setsar/setdar filters now support variables in ratio expressions
- elbg filter
- string validation in ffprobe
- support for decoding through VDPAU in ffmpeg (the -hwaccel option)
- complete Voxware MetaSound decoder
- remove mp3_header_compress bitstream filter
- Windows resource files for shared libraries
- aeval filter
- stereoscopic 3d metadata handling
- WebP encoding via libwebp
- ATRAC3+ decoder
- VP8 in Ogg demuxing
- side & metadata support in NUT
- framepack filter
- XYZ12 rawvideo support in NUT
- Exif metadata support in WebP decoder
- OpenGL device
- Use metadata_header_padding to control padding in ID3 tags (currently used in MP3, AIFF, and OMA files), FLAC header, and the AVI "junk" block.
- Mirillis FIC video decoder
- Support DNx444
- libx265 encoder
- dejudder filter
- Autodetect VDA like all other hardware accelerations

We recommend users, distributors and system integrators to upgrade unless they use current git master.

February 3, 2014, Chemnitzer Linux-Tage
--------------------------------------------------------------------------------------------------------------

We happily announce that FFmpeg will be represented at `Chemnitzer Linux-Tage` in Chemnitz, Germany. The event will take place on 15th and 16th of March.

More information can be found here

We invite you to visit us at our booth located in the Linux-Live area! There we will demonstrate usage of FFmpeg, answer your questions and listen to your problems and wishes.

If you have media files that cannot be processed correctly with FFmpeg, be sure to have a sample with you so we can have a look!

We are looking forward to meet you (again)!

February 9, 2014, trac.ffmpeg.org / trac.mplayerhq.hu Security Breach
--------------------------------------------------------------------------------------------------------------

The server on which FFmpeg and MPlayer Trac issue trackers were installed was compromised. The affected server was taken offline and has been replaced and all software reinstalled. FFmpeg Git, releases, FATE, web and mailinglists are on other servers and were not affected. We believe that the original compromise happened to a server, unrelated to FFmpeg and MPlayer, several months ago. That server was used as a source to clone the VM that we recently moved Trac to. It is not known if anyone used the backdoor that was found.

We recommend all users to change their passwords. Especially users who use a password on Trac that they also use elsewhere, should change that password at least elsewhere.

November 12, 2013, FFmpeg RFP in Debian
--------------------------------------------------------------------------------------------------------------

Since the splitting of Libav the Debian/Ubuntu maintainers have followed the Libav fork. Many people have requested the packaging of ffmpeg in Debian, as it is more feature-complete and in many cases less buggy.

Rogério Brito, a Debian developer, has proposed a Request For Package (RFP) in the Debian bug tracking system.

Please let the Debian and Ubuntu developers know that you support packaging of the real FFmpeg! See Debian ticket #729203 for more details.

October 28, 2013, FFmpeg 2.1
--------------------------------------------------------------------------------------------------------------

We have made a new major release (2.1) It contains all features and bugfixes of the git master branch from 28th October. A partial list of new stuff is below:

- aecho filter
- perspective filter ported from libmpcodecs
- ffprobe -show_programs option
- compand filter
- RTMP seek support
- when transcoding with ffmpeg (i.e. not streamcopying), -ss is now accurate even when used as an input option. Previous behavior can be restored with the -noaccurate_seek option.
- ffmpeg -t option can now be used for inputs, to limit the duration of data read from an input file
- incomplete Voxware MetaSound decoder
- read EXIF metadata from JPEG
- DVB teletext decoder
- phase filter ported from libmpcodecs
- w3fdif filter
- Opus support in Matroska
- FFV1 version 1.3 is stable and no longer experimental
- FFV1: YUVA(444,422,420) 9, 10 and 16 bit support
- changed DTS stream id in lavf mpeg ps muxer from 0x8a to 0x88, to be more consistent with other muxers.
- adelay filter
- pullup filter ported from libmpcodecs
- ffprobe -read_intervals option
- Lossless and alpha support for WebP decoder
- Error Resilient AAC syntax (ER AAC LC) decoding
- Low Delay AAC (ER AAC LD) decoding
- mux chapters in ASF files
- SFTP protocol (via libssh)
- libx264: add ability to encode in YUVJ422P and YUVJ444P
- Fraps: use BT.709 colorspace by default for yuv, as reference fraps decoder does
- make decoding alpha optional for prores, ffv1 and vp6 by setting the skip_alpha flag.
- ladspa wrapper filter
- native VP9 decoder
- dpx parser
- max_error_rate parameter in ffmpeg
- PulseAudio output device
- ReplayGain scanner
- Enhanced Low Delay AAC (ER AAC ELD) decoding (no LD SBR support)
- Linux framebuffer output device
- HEVC decoder, raw HEVC demuxer, HEVC demuxing in TS, Matroska and MP4
- mergeplanes filter

We recommend users, distributors and system integrators to upgrade unless they use current git master.
