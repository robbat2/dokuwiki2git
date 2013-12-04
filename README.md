dokuwiki2git
============

dokuwiki2git converts dokuwiki data directory into a git repository containing
the wiki pages, with proper history. Thus, migration to git-backed wiki engines
(eg. gollum) becomes easier.

It contains two modes:

* direct creation
* git fast-import

Usage
-----

    $ dokuwiki2git /path/to/dokuwiki/data

    $ dokuwiki2git-fast-import /path/to/dokuwiki/data >FILE
    $ mkdir repo ; cd repo ; git init
    $ git fast-import <FILE

This will create a git repository in `gitdir/`, containing the whole history of
the dokuwiki pages, one commit per change.

Details
-------

Change files (`*.changes`) under `data/meta` are read for changelog information
of each page. The changelog of all pages is then sorted by date, and a separate
commit is created from each changelog entry, with the content taken from
`data/attic/<pagename>.<timestamp>.txt.gz`. The original *author name*, *IP*,
*date* and *change message* become standard parts of the created git commit.

Media files are imported under `media/`.

Caveats
-------

NOTE: Media file history is not imported yet. Let me know if you need this. In
new DokuWiki:

* `media/<filename>.<ext>` contains the latest version
* `media_meta/<filepath>.<ext>.changes` contains the changelog
* `media_attic/<filepath>.<timestamp>.<ext>` contains the old versions the
   changelog mentions, except for the last one (which is under `media/`).

License
-------

dokuwiki2git is licensed under AGPLv3.

Contacting
----------

Bugs? Feature requests? Mail the author!
