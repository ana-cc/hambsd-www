---
title: "Code"
date: 2021-06-03T14:12:43+01:00
draft: false
---

HamBSD's source code is maintained in a [git repository][]. The HamBSD
changes are regularly rebased on top of the OpenBSD GitHub mirror.

### Getting Source Code

You will need to install devel/git and devel/got from [ports][] in order
to obtain and work with the source code.

Start by checking out the latest source code from GitHub. It is
recommended to do this somewhere under /home as, at the time of writing,
the clone is roughly 2.1GB:

    $ cd /home/user
    $ git clone --bare https://github.com/HamBSD/src.git

If you do not require the entire history, you can perform a shallow
clone instead to only retreive the latest commit:

    $ cd /home/user
    $ git clone --depth 1 --bare https://github.com/HamBSD/src.git

Then checkout a work tree using [got(1)][]:

    $ cd /usr
    $ got checkout /home/user/src.git /usr/src

To update the tree later:

    TODO

### Source History

As the src.git repository is regularly rebased, there is no history kept
of changes to the HamBSD-specific changes over time. In order to provide
this, [git-format-patch(1)][] is used to serialise the HamBSD commits as
patches which are then version controlled in the [patches repository][].

[git repository]: https://github.com/HamBSD/src.git
[ports]: https://www.openbsd.org/faq/faq15.html
[got(1)]: https://gameoftrees.org/got.1.html
[git-format-patch(1)]: https://git-scm.com/docs/git-format-patch
[patches repository]: https://github.com/irl/hambsd.git