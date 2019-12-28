Using Git to develop FFmpeg
======================================================================================

Table of Contents
1 Introduction
2 Basics Usage
2.1 Get Git
2.2 Cloning the source tree
2.3 Updating the source tree to the latest revision
2.4 Rebasing your local branches
2.5 Adding/removing files/directories
2.6 Showing modifications
2.7 Inspecting the changelog
2.8 Checking source tree status
2.9 Committing
2.10 Preparing a patchset
2.11 Sending patches for review
2.12 Renaming/moving/copying files or contents of files
3 Git configuration
3.1 Personal Git installation
3.2 Repository configuration
4 FFmpeg specific
4.1 Reverting broken commits
4.2 Pushing changes to remote trees
4.3 Finding a specific svn revision
5 Pre-push checklist
6 Server Issues
1 Introduction
This document aims in giving some quick references on a set of useful Git commands. You should always use the extensive and detailed documentation provided directly by Git:

git --help
man git
shows you the available subcommands,

git <command> --help
man git-<command>
shows information about the subcommand <command>.

Additional information could be found on the Git Reference website.

For more information about the Git project, visit the Git website.

Consult these resources whenever you have problems, they are quite exhaustive.

What follows now is a basic introduction to Git and some FFmpeg-specific guidelines to ease the contribution to the project.

2 Basics Usage
2.1 Get Git
You can get Git from http://git-scm.com/ Most distribution and operating system provide a package for it.

2.2 Cloning the source tree
git clone git://source.ffmpeg.org/ffmpeg <target>
This will put the FFmpeg sources into the directory <target>.

git clone git@source.ffmpeg.org:ffmpeg <target>
This will put the FFmpeg sources into the directory <target> and let you push back your changes to the remote repository.

git clone gil@ffmpeg.org:ffmpeg-web <target>
This will put the source of the FFmpeg website into the directory <target> and let you push back your changes to the remote repository. (Note that gil stands for GItoLite and is not a typo of git.)

If you don’t have write-access to the ffmpeg-web repository, you can create patches after making a read-only ffmpeg-web clone:

git clone git://ffmpeg.org/ffmpeg-web <target>
Make sure that you do not have Windows line endings in your checkouts, otherwise you may experience spurious compilation failures. One way to achieve this is to run

git config --global core.autocrlf false
2.3 Updating the source tree to the latest revision
git pull (--rebase)
pulls in the latest changes from the tracked branch. The tracked branch can be remote. By default the master branch tracks the branch master in the remote origin.

--rebase (see below) is recommended.

2.4 Rebasing your local branches
git pull --rebase
fetches the changes from the main repository and replays your local commits over it. This is required to keep all your local changes at the top of FFmpeg’s master tree. The master tree will reject pushes with merge commits.

2.5 Adding/removing files/directories
git add [-A] <filename/dirname>
git rm [-r] <filename/dirname>
Git needs to get notified of all changes you make to your working directory that makes files appear or disappear. Line moves across files are automatically tracked.

2.6 Showing modifications
git diff <filename(s)>
will show all local modifications in your working directory as unified diff.

2.7 Inspecting the changelog
git log <filename(s)>
You may also use the graphical tools like gitview or gitk or the web interface available at http://source.ffmpeg.org/.

2.8 Checking source tree status
git status
detects all the changes you made and lists what actions will be taken in case of a commit (additions, modifications, deletions, etc.).

2.9 Committing
git diff --check
to double check your changes before committing them to avoid trouble later on. All experienced developers do this on each and every commit, no matter how small.

Every one of them has been saved from looking like a fool by this many times. It’s very easy for stray debug output or cosmetic modifications to slip in, please avoid problems through this extra level of scrutiny.

For cosmetics-only commits you should get (almost) empty output from

git diff -w -b <filename(s)>
Also check the output of

git status
to make sure you don’t have untracked files or deletions.

git add [-i|-p|-A] <filenames/dirnames>
Make sure you have told Git your name and email address

git config --global user.name "My Name"
git config --global user.email my@email.invalid
Use --global to set the global configuration for all your Git checkouts.

Git will select the changes to the files for commit. Optionally you can use the interactive or the patch mode to select hunk by hunk what should be added to the commit.

git commit
Git will commit the selected changes to your current local branch.

You will be prompted for a log message in an editor, which is either set in your personal configuration file through

git config --global core.editor
or set by one of the following environment variables: GIT_EDITOR, VISUAL or EDITOR.

Log messages should be concise but descriptive. Explain why you made a change, what you did will be obvious from the changes themselves most of the time. Saying just "bug fix" or "10l" is bad. Remember that people of varying skill levels look at and educate themselves while reading through your code. Don’t include filenames in log messages, Git provides that information.

Possibly make the commit message have a terse, descriptive first line, an empty line and then a full description. The first line will be used to name the patch by git format-patch.

2.10 Preparing a patchset
git format-patch <commit> [-o directory]
will generate a set of patches for each commit between <commit> and current HEAD. E.g.

git format-patch origin/master
will generate patches for all commits on current branch which are not present in upstream. A useful shortcut is also

git format-patch -n
which will generate patches from last n commits. By default the patches are created in the current directory.

2.11 Sending patches for review
git send-email <commit list|directory>
will send the patches created by git format-patch or directly generates them. All the email fields can be configured in the global/local configuration or overridden by command line. Note that this tool must often be installed separately (e.g. git-email package on Debian-based distros).

2.12 Renaming/moving/copying files or contents of files
Git automatically tracks such changes, making those normal commits.

mv/cp path/file otherpath/otherfile
git add [-A] .
git commit
3 Git configuration
In order to simplify a few workflows, it is advisable to configure both your personal Git installation and your local FFmpeg repository.

3.1 Personal Git installation
Add the following to your ~/.gitconfig to help git send-email and git format-patch detect renames:

[diff]
        renames = copy
3.2 Repository configuration
In order to have git send-email automatically send patches to the ffmpeg-devel mailing list, add the following stanza to /path/to/ffmpeg/repository/.git/config:

[sendemail]
        to = ffmpeg-devel@ffmpeg.org
4 FFmpeg specific
4.1 Reverting broken commits
git reset <commit>
git reset will uncommit the changes till <commit> rewriting the current branch history.

git commit --amend
allows one to amend the last commit details quickly.

git rebase -i origin/master
will replay local commits over the main repository allowing to edit, merge or remove some of them in the process.

git reset, git commit --amend and git rebase rewrite history, so you should use them ONLY on your local or topic branches. The main repository will reject those changes.

git revert <commit>
git revert will generate a revert commit. This will not make the faulty commit disappear from the history.

4.2 Pushing changes to remote trees
git push origin master --dry-run
Will simulate a push of the local master branch to the default remote (origin). And list which branches and ranges or commits would have been pushed. Git will prevent you from pushing changes if the local and remote trees are out of sync. Refer to Updating the source tree to the latest revision.

git remote add <name> <url>
Will add additional remote with a name reference, it is useful if you want to push your local branch for review on a remote host.

git push <remote> <refspec>
Will push the changes to the <remote> repository. Omitting <refspec> makes git push update all the remote branches matching the local ones.

4.3 Finding a specific svn revision
Since version 1.7.1 Git supports ‘:/foo’ syntax for specifying commits based on a regular expression. see man gitrevisions

git show :/'as revision 23456'
will show the svn changeset ‘r23456’. With older Git versions searching in the git log output is the easiest option (especially if a pager with search capabilities is used).

This commit can be checked out with

git checkout -b svn_23456 :/'as revision 23456'
or for Git < 1.7.1 with

git checkout -b svn_23456 $SHA1
where $SHA1 is the commit hash from the git log output.

5 Pre-push checklist
Once you have a set of commits that you feel are ready for pushing, work through the following checklist to doublecheck everything is in proper order. This list tries to be exhaustive. In case you are just pushing a typo in a comment, some of the steps may be unnecessary. Apply your common sense, but if in doubt, err on the side of caution.

First, make sure that the commits and branches you are going to push match what you want pushed and that nothing is missing, extraneous or wrong. You can see what will be pushed by running the git push command with --dry-run first. And then inspecting the commits listed with git log -p 1234567..987654. The git status command may help in finding local changes that have been forgotten to be added.

Next let the code pass through a full run of our test suite.

make distclean
/path/to/ffmpeg/configure
make fate
if fate fails due to missing samples run make fate-rsync and retry
Make sure all your changes have been checked before pushing them, the test suite only checks against regressions and that only to some extend. It does obviously not check newly added features/code to be working unless you have added a test for that (which is recommended).

Also note that every single commit should pass the test suite, not just the result of a series of patches.

Once everything passed, push the changes to your public ffmpeg clone and post a merge request to ffmpeg-devel. You can also push them directly but this is not recommended.

6 Server Issues
Contact the project admins at root@ffmpeg.org if you have technical problems with the Git server.

This document was generated on June 11, 2019 using makeinfo.
