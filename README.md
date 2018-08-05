repostatus.org
==============

[![Project Status: Active – The project has reached a stable, usable state and is being actively developed.](https://www.repostatus.org/badges/latest/active.svg)](https://www.repostatus.org/#active)

A standard to easily communicate to humans and machines the development/support and usability status of software repositories/projects.

For the majority of documentation and human-readable text, see https://www.repostatus.org/ or the [gh-pages branch](https://github.com/jantman/repostatus.org/tree/gh-pages) from which it is built.

Please feel free to leave comments as Issues, or open pull requests.

Community Involvement
---------------------

This project seems to have gained a lot more interest than I thought it would. As of April, 2017 there are [over 1,200 references on GitHub](https://github.com/search?l=&q=https%3A%2F%2Fwww.repostatus.org%2Fbadges%2F+-user%3A%22jantman%22&ref=advsearch&type=Code&utf8=%E2%9C%93)
to repostatus.org badge URLs. I do *not* want to be the sole person making decisions for this project. I encourage everyone who finds
it useful to watch [the repo on GitHub](https://github.com/jantman/repostatus.org) and provide their feedback in discussions, especially the
issues with the [discussion](https://github.com/jantman/repostatus.org/issues?q=is%3Aopen+is%3Aissue+label%3Adiscussion) or
["needs decision"](https://github.com/jantman/repostatus.org/issues?q=is%3Aopen+is%3Aissue+label%3Adiscussion+label%3A%22needs+decision%22)
labels. I'm handling the code updates, but I very much want this project to be driven based on consensus of those who use it.

Contributing
------------

For changes to the site, text, or anything other than the badges themselves (and their descriptions and sample markup),
simply cut a pull request against the master branch. The content that appears on the website (in the gh-pages branch)
comes from ``gh_pages/`` in master. Note that some of it (described below) is generated programmatically.

The badges (SVG), their descriptions and their sample markup are generated by a [Fabfile](http://www.fabfile.org/). If you're looking
to add a new badge or make changes to an existing one, simply update the ``badge_info`` dictionary at the top of ``fabfile.py`` and
then run ``fab make_badges`` (requires Python and some packages; see the comment at the top of the file for requirements). This will
regenerate all badges, metadata and samples into ``badges/latest``. You can then cut a pull request for this; a version number will
be assigned at merge time. Please remember to also update ``gh_pages/index.md`` for any badge changes.

Release Process
---------------

1. Get everything included in the release merged into master.
2. Assign a version number. In general, patch versions should only be assigned for releases that fix trivial (i.e. spelling)
issues or touch things other than the badges and JSON (i.e. the markup samples). Minor versions should be assigned to
changes that correct grammatical or spelling errors, or graphical elements. Major versions must be assigned to any changes
that add or remove badges, or alter the meaning of existing badges.
3. Re-run ``fab make_badges`` and ensure there are no new changes.
4. Run ``fab version_badges:x.y.z`` (where ``x.y.z`` is the version number).
5. Add a ``CHANGELOG.md`` entry.
6. Run ``fab badges2pages`` to copy the badges under ``gh-pages/``
6. Run ``fab publish`` to push changes to the gh-pages branch.
7. Review the diff of gh-pages against origin.
8. Assuing all is well, push gh-pages to origin. The changes are now live.
9. Tag master with the version number (use GitHub Releases)
