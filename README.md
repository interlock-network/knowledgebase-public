# Interlock Knowledge Base
## Intro
This is the knowledge-base of the interlock-team. It is vaguely
Wikipedia-like in structure, except instead of wiki-markup we use
plain-old markdown, which basically everyone who has ever used Slack,
Discourse, Discord, and GitHub is familiar with.

We need a place where our team can *easily* access, store, and update
our knowledge in a way that preserves history and is easily searchable.
Git handles the history part, and the searchability can be achieved in
numerous ways thanks for the simplicity of plain-text format. We also
want a place where we can do both linear and non-linear exploration. The
articles themselves are linear, but the knowledge-base is non-linear
since articles are connected via cross-links. Furthermore, one can
achieve a pseudo-linear presentation by having a linear list of article
links (as a kind of recommended reading order).

## Structure
The most successful knowledge-base on the planet is Wikipedia, which has
a flat structure of articles, and uses the web's hyperlinks to create
connections between them. We are *almost* like that except we do have a
top-level structure that people can use to find the *kind* of content
they are looking for.

We structure the articles in the knowledge-base, via
interrogative-correlatives such as [ who ]( who/README.md),
[ what ](what/README.md), [ where ]( where/README.md), 
[ when ]( when/README.md),[ why ]( why/README.md), 
[ which ]( which/README.md), [ whither ](whither/README.md), 
[ whose ]( whose/README.md),[ how ](how/README.md), 
[ how-many ]( how-many/README.md), and
[ what-kind-of ](what-kind-of/README.md). This lets people easily search for descriptions
of something (i.e. like our extension) in the  ` what `  directory, for
tutorials about things (i.e. like how to install or test or merge our
extension) in the  ` how `  directory, and so on. Each correlative has
its own directory with its own README file.

## Contribution
To contribute, you just create and edit markdown-files. You can do this
in your favorite text editor, or in a markdown-supporting
knowledge-base-editor like *Obsidian* &mdash; which we are testing out.

Most contributions take on life as *discussions* on GitHub, and
eventually graduate into the knowledge base as one of more articles.
Alternatively, an article can be derived from a GitHub issue. In general
contributions and changes should be discussed before they are made.

Also, if you want to use a different markup format supported by GitHub,
you can use org-mode. Obsidian supports org-mode via a plugin.

## Scope
There is no scope on content. You can include anything that you think is
interesting, because nobody knows what is relevant ahead-of-time.
Instead of imposing a ceiling, we impose a floor &mdash; at *minimum*
the knowledge base must contain enough knowledge to allow a complete
novice to contribute to our software, but it can contain much more.
Obviously content that is, illegal, inflammatory, or obviously offensive
is forbidden. If you are unsure that your content would meet that
criterion, feel free to start a discussion about it.

