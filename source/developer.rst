Developer Documentation
============================

1 Notes for external developers
-------------------------------------------

This document is mostly useful for internal FFmpeg developers. External developers who need to use the API in their application should refer to the API doxygen documentation in the public headers, and check the examples in doc/examples and in the source code to see how the public API is employed.

You can use the FFmpeg libraries in your commercial program, but you are encouraged to publish any patch you make. In this case the best way to proceed is to send your patches to the ffmpeg-devel mailing list following the guidelines illustrated in the remainder of this document.

For more detailed legal information about the use of FFmpeg in external programs read the LICENSE file in the source tree and consult https://ffmpeg.org/legal.html.

2 Contributing
-------------------------------------------

There are 2 ways by which code gets into FFmpeg:

Submitting patches to the ffmpeg-devel mailing list. See Submitting patches for details.
Directly committing changes to the main tree.
Whichever way, changes should be reviewed by the maintainer of the code before they are committed. And they should follow the Coding Rules. The developer making the commit and the author are responsible for their changes and should try to fix issues their commit causes.

3 Coding Rules
-------------------------------------------

3.1 Code formatting conventions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

There are the following guidelines regarding the indentation in files:

Indent size is 4.
The TAB character is forbidden outside of Makefiles as is any form of trailing whitespace. Commits containing either will be rejected by the git repository.
You should try to limit your code lines to 80 characters; however, do so if and only if this improves readability.
K&R coding style is used.
The presentation is one inspired by ’indent -i4 -kr -nut’.

The main priority in FFmpeg is simplicity and small code size in order to minimize the bug count.

3.2 Comments
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Use the JavaDoc/Doxygen format (see examples below) so that code documentation can be generated automatically. All nontrivial functions should have a comment above them explaining what the function does, even if it is just one sentence. All structures and their member variables should be documented, too.

Avoid Qt-style and similar Doxygen syntax with ! in it, i.e. replace //! with /// and similar. Also @ syntax should be employed for markup commands, i.e. use @param and not \param.

.. code-block:: c

    /**
    * @file
    * MPEG codec.
    * @author ...
    */

    /**
    * Summary sentence.
    * more text ...
    * ...
    */
    typedef struct Foobar {
        int var1; /**< var1 description */
        int var2; ///< var2 description
        /** var3 description */
        int var3;
    } Foobar;

    /**
    * Summary sentence.
    * more text ...
    * ...
    * @param my_parameter description of my_parameter
    * @return return value description
    */
    int myfunc(int my_parameter)
    ...

3.3 C language features
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

FFmpeg is programmed in the ISO C90 language with a few additional features from ISO C99, namely:


.. code-block:: c

    the ‘inline’ keyword;
    ‘//’ comments;
    designated struct initializers (‘struct s x = { .i = 17 };’);
    compound literals (‘x = (struct s) { 17, 23 };’).
    for loops with variable definition (‘for (int i = 0; i < 8; i++)’);

Implementation defined behavior for signed integers is assumed to match the expected behavior for two’s complement. Non representable values in integer casts are binary truncated. Shift right of signed values uses sign extension.
These features are supported by all compilers we care about, so we will not accept patches to remove their use unless they absolutely do not impair clarity and performance.

All code must compile with recent versions of GCC and a number of other currently supported compilers. To ensure compatibility, please do not use additional C99 features or GCC extensions. Especially watch out for:


.. code-block:: c

  mixing statements and declarations;
  ‘long long’ (use ‘int64_t’ instead);
  ‘__attribute__’ not protected by ‘#ifdef __GNUC__’ or similar;
  GCC statement expressions (‘(x = ({ int y = 4; y; })’).

3.4 Naming conventions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

All names should be composed with underscores (_), not CamelCase. For example, ‘avfilter_get_video_buffer’ is an acceptable function name and ‘AVFilterGetVideo’ is not. The exception from this are type names, like for example structs and enums; they should always be in CamelCase.

There are the following conventions for naming variables and functions:

For local variables no prefix is required.
For file-scope variables and functions declared as static, no prefix is required.
For variables and functions visible outside of file scope, but only used internally by a library, an ff_ prefix should be used, e.g. ‘ff_w64_demuxer’.
For variables and functions visible outside of file scope, used internally across multiple libraries, use avpriv_ as prefix, for example, ‘avpriv_report_missing_feature’.
Each library has its own prefix for public symbols, in addition to the commonly used av_ (avformat_ for libavformat, avcodec_ for libavcodec, swr_ for libswresample, etc). Check the existing code and choose names accordingly. Note that some symbols without these prefixes are also exported for retro-compatibility reasons. These exceptions are declared in the lib<name>/lib<name>.v files.
Furthermore, name space reserved for the system should not be invaded. Identifiers ending in _t are reserved by POSIX. Also avoid names starting with __ or _ followed by an uppercase letter as they are reserved by the C standard. Names starting with _ are reserved at the file level and may not be used for externally visible symbols. If in doubt, just avoid names starting with _ altogether.

3.5 Miscellaneous conventions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

fprintf and printf are forbidden in libavformat and libavcodec, please use av_log() instead.
Casts should be used only when necessary. Unneeded parentheses should also be avoided if they don’t make the code easier to understand.
3.6 Editor configuration
In order to configure Vim to follow FFmpeg formatting conventions, paste the following snippet into your .vimrc:


.. code-block:: c

  " indentation rules for FFmpeg: 4 spaces, no tabs
  set expandtab
  set shiftwidth=4
  set softtabstop=4
  set cindent
  set cinoptions=(0
  " Allow tabs in Makefiles.

autocmd FileType make,automake set noexpandtab shiftwidth=8 softtabstop=8
" Trailing whitespace and tabs are forbidden, so highlight them.
highlight ForbiddenWhitespace ctermbg=red guibg=red
match ForbiddenWhitespace /\s\+$\|\t/
" Do not highlight spaces at the end of line while typing on that line.
autocmd InsertEnter * match ForbiddenWhitespace /\t\|\s\+\%#\@<!$/
For Emacs, add these roughly equivalent lines to your .emacs.d/init.el:


.. code-block:: c

  (c-add-style "ffmpeg"
              '("k&r"
                (c-basic-offset . 4)
                (indent-tabs-mode . nil)
                (show-trailing-whitespace . t)
                (c-offsets-alist
                  (statement-cont . (c-lineup-assignments +)))
                )
              )
  (setq c-default-style "ffmpeg")

4 Development Policy
-------------------------------------------

4.1 Patches/Committing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Licenses for patches must be compatible with FFmpeg.
Contributions should be licensed under the LGPL 2.1, including an "or any later version" clause, or, if you prefer a gift-style license, the ISC or MIT license. GPL 2 including an "or any later version" clause is also acceptable, but LGPL is preferred. If you add a new file, give it a proper license header. Do not copy and paste it from a random place, use an existing file as template.

You must not commit code which breaks FFmpeg!
This means unfinished code which is enabled and breaks compilation, or compiles but does not work/breaks the regression tests. Code which is unfinished but disabled may be permitted under-circumstances, like missing samples or an implementation with a small subset of features. Always check the mailing list for any reviewers with issues and test FATE before you push.

Keep the main commit message short with an extended description below.
The commit message should have a short first line in the form of a ‘topic: short description’ as a header, separated by a newline from the body consisting of an explanation of why the change is necessary. If the commit fixes a known bug on the bug tracker, the commit message should include its bug ID. Referring to the issue on the bug tracker does not exempt you from writing an excerpt of the bug in the commit message.

Testing must be adequate but not excessive.
If it works for you, others, and passes FATE then it should be OK to commit it, provided it fits the other committing criteria. You should not worry about over-testing things. If your code has problems (portability, triggers compiler bugs, unusual environment etc) they will be reported and eventually fixed.

Do not commit unrelated changes together.
They should be split them into self-contained pieces. Also do not forget that if part B depends on part A, but A does not depend on B, then A can and should be committed first and separate from B. Keeping changes well split into self-contained parts makes reviewing and understanding them on the commit log mailing list easier. This also helps in case of debugging later on. Also if you have doubts about splitting or not splitting, do not hesitate to ask/discuss it on the developer mailing list.

Ask before you change the build system (configure, etc).
Do not commit changes to the build system (Makefiles, configure script) which change behavior, defaults etc, without asking first. The same applies to compiler warning fixes, trivial looking fixes and to code maintained by other developers. We usually have a reason for doing things the way we do. Send your changes as patches to the ffmpeg-devel mailing list, and if the code maintainers say OK, you may commit. This does not apply to files you wrote and/or maintain.

Cosmetic changes should be kept in separate patches.
We refuse source indentation and other cosmetic changes if they are mixed with functional changes, such commits will be rejected and removed. Every developer has his own indentation style, you should not change it. Of course if you (re)write something, you can use your own style, even though we would prefer if the indentation throughout FFmpeg was consistent (Many projects force a given indentation style - we do not.). If you really need to make indentation changes (try to avoid this), separate them strictly from real changes.

NOTE: If you had to put if(){ .. } over a large (> 5 lines) chunk of code, then either do NOT change the indentation of the inner part within (do not move it to the right)! or do so in a separate commit

Commit messages should always be filled out properly.
Always fill out the commit log message. Describe in a few lines what you changed and why. You can refer to mailing list postings if you fix a particular bug. Comments such as "fixed!" or "Changed it." are unacceptable. Recommended format:

area changed: Short 1 line description

details describing what and why and giving references.
Credit the author of the patch.
Make sure the author of the commit is set correctly. (see git commit –author) If you apply a patch, send an answer to ffmpeg-devel (or wherever you got the patch from) saying that you applied the patch.

Complex patches should refer to discussion surrounding them.
When applying patches that have been discussed (at length) on the mailing list, reference the thread in the log message.

Always wait long enough before pushing changes
Do NOT commit to code actively maintained by others without permission. Send a patch to ffmpeg-devel. If no one answers within a reasonable time-frame (12h for build failures and security fixes, 3 days small changes, 1 week for big patches) then commit your patch if you think it is OK. Also note, the maintainer can simply ask for more time to review!

4.2 Code
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

API/ABI changes should be discussed before they are made.
Do not change behavior of the programs (renaming options etc) or public API or ABI without first discussing it on the ffmpeg-devel mailing list. Do not remove widely used functionality or features (redundant code can be removed).

Remember to check if you need to bump versions for libav*.
Depending on the change, you may need to change the version integer. Incrementing the first component means no backward compatibility to previous versions (e.g. removal of a function from the public API). Incrementing the second component means backward compatible change (e.g. addition of a function to the public API or extension of an existing data structure). Incrementing the third component means a noteworthy binary compatible change (e.g. encoder bug fix that matters for the decoder). The third component always starts at 100 to distinguish FFmpeg from Libav.

Warnings for correct code may be disabled if there is no other option.
Compiler warnings indicate potential bugs or code with bad style. If a type of warning always points to correct and clean code, that warning should be disabled, not the code changed. Thus the remaining warnings can either be bugs or correct code. If it is a bug, the bug has to be fixed. If it is not, the code should be changed to not generate a warning unless that causes a slowdown or obfuscates the code.

Check untrusted input properly.
Never write to unallocated memory, never write over the end of arrays, always check values read from some untrusted source before using them as array index or other risky things.

4.3 Documentation/Other
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Subscribe to the ffmpeg-devel mailing list.
It is important to be subscribed to the ffmpeg-devel mailing list. Almost any non-trivial patch is to be sent there for review. Other developers may have comments about your contribution. We expect you see those comments, and to improve it if requested. (N.B. Experienced committers have other channels, and may sometimes skip review for trivial fixes.) Also, discussion here about bug fixes and FFmpeg improvements by other developers may be helpful information for you. Finally, by being a list subscriber, your contribution will be posted immediately to the list, without the moderation hold which messages from non-subscribers experience.

However, it is more important to the project that we receive your patch than that you be subscribed to the ffmpeg-devel list. If you have a patch, and don’t want to subscribe and discuss the patch, then please do send it to the list anyway.

Subscribe to the ffmpeg-cvslog mailing list.
Diffs of all commits are sent to the ffmpeg-cvslog mailing list. Some developers read this list to review all code base changes from all sources. Subscribing to this list is not mandatory.

Keep the documentation up to date.
Update the documentation if you change behavior or add features. If you are unsure how best to do this, send a patch to ffmpeg-devel, the documentation maintainer(s) will review and commit your stuff.

Important discussions should be accessible to all.
Try to keep important discussions and requests (also) on the public developer mailing list, so that all developers can benefit from them.

Check your entries in MAINTAINERS.
Make sure that no parts of the codebase that you maintain are missing from the MAINTAINERS file. If something that you want to maintain is missing add it with your name after it. If at some point you no longer want to maintain some code, then please help in finding a new maintainer and also don’t forget to update the MAINTAINERS file.

We think our rules are not too hard. If you have comments, contact us.

5 Code of conduct
-------------------------------------------

Be friendly and respectful towards others and third parties. Treat others the way you yourself want to be treated.

Be considerate. Not everyone shares the same viewpoint and priorities as you do. Different opinions and interpretations help the project. Looking at issues from a different perspective assists development.

Do not assume malice for things that can be attributed to incompetence. Even if it is malice, it’s rarely good to start with that as initial assumption.

Stay friendly even if someone acts contrarily. Everyone has a bad day once in a while. If you yourself have a bad day or are angry then try to take a break and reply once you are calm and without anger if you have to.

Try to help other team members and cooperate if you can.

The goal of software development is to create technical excellence, not for any individual to be better and "win" against the others. Large software projects are only possible and successful through teamwork.

If someone struggles do not put them down. Give them a helping hand instead and point them in the right direction.

Finally, keep in mind the immortal words of Bill and Ted, "Be excellent to each other."

6 Submitting patches
-------------------------------------------

First, read the Coding Rules above if you did not yet, in particular the rules regarding patch submission.

When you submit your patch, please use git format-patch or git send-email. We cannot read other diffs :-).

Also please do not submit a patch which contains several unrelated changes. Split it into separate, self-contained pieces. This does not mean splitting file by file. Instead, make the patch as small as possible while still keeping it as a logical unit that contains an individual change, even if it spans multiple files. This makes reviewing your patches much easier for us and greatly increases your chances of getting your patch applied.

Use the patcheck tool of FFmpeg to check your patch. The tool is located in the tools directory.

Run the Regression tests before submitting a patch in order to verify it does not cause unexpected problems.

It also helps quite a bit if you tell us what the patch does (for example ’replaces lrint by lrintf’), and why (for example ’*BSD isn’t C99 compliant and has no lrint()’)

Also please if you send several patches, send each patch as a separate mail, do not attach several unrelated patches to the same mail.

Patches should be posted to the ffmpeg-devel mailing list. Use git send-email when possible since it will properly send patches without requiring extra care. If you cannot, then send patches as base64-encoded attachments, so your patch is not trashed during transmission. Also ensure the correct mime type is used (text/x-diff or text/x-patch or at least text/plain) and that only one patch is inline or attached per mail. You can check https://patchwork.ffmpeg.org, if your patch does not show up, its mime type likely was wrong.

Your patch will be reviewed on the mailing list. You will likely be asked to make some changes and are expected to send in an improved version that incorporates the requests from the review. This process may go through several iterations. Once your patch is deemed good enough, some developer will pick it up and commit it to the official FFmpeg tree.

Give us a few days to react. But if some time passes without reaction, send a reminder by email. Your patch should eventually be dealt with.

7 New codecs or formats checklist
-------------------------------------------

Did you use av_cold for codec initialization and close functions?
Did you add a long_name under NULL_IF_CONFIG_SMALL to the AVCodec or AVInputFormat/AVOutputFormat struct?
Did you bump the minor version number (and reset the micro version number) in libavcodec/version.h or libavformat/version.h?
Did you register it in allcodecs.c or allformats.c?
Did you add the AVCodecID to avcodec.h? When adding new codec IDs, also add an entry to the codec descriptor list in libavcodec/codec_desc.c.
If it has a FourCC, did you add it to libavformat/riff.c, even if it is only a decoder?
Did you add a rule to compile the appropriate files in the Makefile? Remember to do this even if you’re just adding a format to a file that is already being compiled by some other rule, like a raw demuxer.
Did you add an entry to the table of supported formats or codecs in doc/general.texi?
Did you add an entry in the Changelog?
If it depends on a parser or a library, did you add that dependency in configure?
Did you git add the appropriate files before committing?
Did you make sure it compiles standalone, i.e. with configure --disable-everything --enable-decoder=foo (or --enable-demuxer or whatever your component is)?

8 Patch submission checklist
-------------------------------------------

Does make fate pass with the patch applied?
Was the patch generated with git format-patch or send-email?
Did you sign-off your patch? (git commit -s) See Sign your work for the meaning of sign-off.
Did you provide a clear git commit log message?
Is the patch against latest FFmpeg git master branch?
Are you subscribed to ffmpeg-devel? (the list is subscribers only due to spam)
Have you checked that the changes are minimal, so that the same cannot be achieved with a smaller patch and/or simpler final code?
If the change is to speed critical code, did you benchmark it?
If you did any benchmarks, did you provide them in the mail?
Have you checked that the patch does not introduce buffer overflows or other security issues?
Did you test your decoder or demuxer against damaged data? If no, see tools/trasher, the noise bitstream filter, and zzuf. Your decoder or demuxer should not crash, end in a (near) infinite loop, or allocate ridiculous amounts of memory when fed damaged data.
Did you test your decoder or demuxer against sample files? Samples may be obtained at https://samples.ffmpeg.org.
Does the patch not mix functional and cosmetic changes?
Did you add tabs or trailing whitespace to the code? Both are forbidden.
Is the patch attached to the email you send?
Is the mime type of the patch correct? It should be text/x-diff or text/x-patch or at least text/plain and not application/octet-stream.
If the patch fixes a bug, did you provide a verbose analysis of the bug?
If the patch fixes a bug, did you provide enough information, including a sample, so the bug can be reproduced and the fix can be verified? Note please do not attach samples >100k to mails but rather provide a URL, you can upload to ftp://upload.ffmpeg.org.
Did you provide a verbose summary about what the patch does change?
Did you provide a verbose explanation why it changes things like it does?
Did you provide a verbose summary of the user visible advantages and disadvantages if the patch is applied?
Did you provide an example so we can verify the new feature added by the patch easily?
If you added a new file, did you insert a license header? It should be taken from FFmpeg, not randomly copied and pasted from somewhere else.
You should maintain alphabetical order in alphabetically ordered lists as long as doing so does not break API/ABI compatibility.
Lines with similar content should be aligned vertically when doing so improves readability.
Consider adding a regression test for your code.
If you added YASM code please check that things still work with –disable-yasm.
Make sure you check the return values of function and return appropriate error codes. Especially memory allocation functions like av_malloc() are notoriously left unchecked, which is a serious problem.
Test your code with valgrind and or Address Sanitizer to ensure it’s free of leaks, out of array accesses, etc.

9 Patch review process
-------------------------------------------

All patches posted to ffmpeg-devel will be reviewed, unless they contain a clear note that the patch is not for the git master branch. Reviews and comments will be posted as replies to the patch on the mailing list. The patch submitter then has to take care of every comment, that can be by resubmitting a changed patch or by discussion. Resubmitted patches will themselves be reviewed like any other patch. If at some point a patch passes review with no comments then it is approved, that can for simple and small patches happen immediately while large patches will generally have to be changed and reviewed many times before they are approved. After a patch is approved it will be committed to the repository.

We will review all submitted patches, but sometimes we are quite busy so especially for large patches this can take several weeks.

If you feel that the review process is too slow and you are willing to try to take over maintainership of the area of code you change then just clone git master and maintain the area of code there. We will merge each area from where its best maintained.

When resubmitting patches, please do not make any significant changes not related to the comments received during review. Such patches will be rejected. Instead, submit significant changes or new features as separate patches.

Everyone is welcome to review patches. Also if you are waiting for your patch to be reviewed, please consider helping to review other patches, that is a great way to get everyone’s patches reviewed sooner.

10 Regression tests
-------------------------------------------

Before submitting a patch (or committing to the repository), you should at least test that you did not break anything.

Running ’make fate’ accomplishes this, please see fate.html for details.

[Of course, some patches may change the results of the regression tests. In this case, the reference results of the regression tests shall be modified accordingly].

10.1 Adding files to the fate-suite dataset
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When there is no muxer or encoder available to generate test media for a specific test then the media has to be included in the fate-suite. First please make sure that the sample file is as small as possible to test the respective decoder or demuxer sufficiently. Large files increase network bandwidth and disk space requirements. Once you have a working fate test and fate sample, provide in the commit message or introductory message for the patch series that you post to the ffmpeg-devel mailing list, a direct link to download the sample media.

10.2 Visualizing Test Coverage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The FFmpeg build system allows visualizing the test coverage in an easy manner with the coverage tools gcov/lcov. This involves the following steps:

Configure to compile with instrumentation enabled: configure --toolchain=gcov.
Run your test case, either manually or via FATE. This can be either the full FATE regression suite, or any arbitrary invocation of any front-end tool provided by FFmpeg, in any combination.
Run make lcov to generate coverage data in HTML format.
View lcov/index.html in your preferred HTML viewer.
You can use the command make lcov-reset to reset the coverage measurements. You will need to rerun make lcov after running a new test.

10.3 Using Valgrind
The configure script provides a shortcut for using valgrind to spot bugs related to memory handling. Just add the option --toolchain=valgrind-memcheck or --toolchain=valgrind-massif to your configure line, and reasonable defaults will be set for running FATE under the supervision of either the memcheck or the massif tool of the valgrind suite.

In case you need finer control over how valgrind is invoked, use the --target-exec='valgrind <your_custom_valgrind_options> option in your configure line instead.

11 Release process
-------------------------------------------

FFmpeg maintains a set of release branches, which are the recommended deliverable for system integrators and distributors (such as Linux distributions, etc.). At regular times, a release manager prepares, tests and publishes tarballs on the https://ffmpeg.org website.

There are two kinds of releases:

Major releases always include the latest and greatest features and functionality.
Point releases are cut from release branches, which are named release/X, with X being the release version number.
Note that we promise to our users that shared libraries from any FFmpeg release never break programs that have been compiled against previous versions of the same release series in any case!

However, from time to time, we do make API changes that require adaptations in applications. Such changes are only allowed in (new) major releases and require further steps such as bumping library version numbers and/or adjustments to the symbol versioning file. Please discuss such changes on the ffmpeg-devel mailing list in time to allow forward planning.

11.1 Criteria for Point Releases
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Changes that match the following criteria are valid candidates for inclusion into a point release:

Fixes a security issue, preferably identified by a CVE number issued by http://cve.mitre.org/.
Fixes a documented bug in https://trac.ffmpeg.org.
Improves the included documentation.
Retains both source code and binary compatibility with previous point releases of the same release branch.
The order for checking the rules is (1 OR 2 OR 3) AND 4.

11.2 Release Checklist
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The release process involves the following steps:

Ensure that the RELEASE file contains the version number for the upcoming release.
Add the release at https://trac.ffmpeg.org/admin/ticket/versions.
Announce the intent to do a release to the mailing list.
Make sure all relevant security fixes have been backported. See https://ffmpeg.org/security.html.
Ensure that the FATE regression suite still passes in the release branch on at least i386 and amd64 (cf. Regression tests).
Prepare the release tarballs in bz2 and gz formats, and supplementing files that contain gpg signatures
Publish the tarballs at https://ffmpeg.org/releases. Create and push an annotated tag in the form nX, with X containing the version number.
Propose and send a patch to the ffmpeg-devel mailing list with a news entry for the website.
Publish the news entry.
Send an announcement to the mailing list.
This document was generated on June 8, 2019 using makeinfo.
