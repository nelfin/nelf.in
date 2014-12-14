Hello World
===========

:date: 2014-12-14 16:47
:tags: python, blog
:authors: Andrew Haigh
:summary: Blogging with Pelican and GitHub pages

Built in an afternoon with pelican, taking advantage of GitHub pages backing
onto Fastly. Who has the time to set up a CDN?

Running a small pre-push hook courtesy of `Getting Clojure`_, with some minor
additions to ensure sensible messages each time:

.. code-block:: bash

    #!/bin/bash
    lastcommit=`git log origin/master..HEAD --oneline`
    if [ $(echo $lastcommit | wc -l) -gt 1 ];
    then
        message="`git log -1 --oneline`\n\n`git log origin/master..HEAD^ --oneline`"
    else
        message=`git log -1 --oneline`
    fi
    make publish
    cd output && git add -A && git commit -m "$message" && git push origin master
    exit 0

..

_`Getting Clojure`: http://mavant.com/blog/2014/03/10/pelican-git-hooks-github-dot-io/
