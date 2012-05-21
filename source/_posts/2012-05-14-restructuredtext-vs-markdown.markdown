---
layout: post
title: "reStructuredText vs. Markdown"
date: 2011-04-17
comments: true
categories: Programming
permalink: /blog/restructuredtext-vs-markdown
---

Markdown wins. (For generating html anyway)

Why? You decide for yourself:

<a href="http://docutils.sourceforge.net/"><img src="http://readncode.com/media/images/reStructuredText.png"></a>
<p></p>
<a href="http://daringfireball.net/projects/markdown/"><img src="http://readncode.com/media/images/markdown.png"></a>

Markdown is a perl file with a README on how to use it to convert text to html.

Installing reST means manually installing docutils, with <a target=blank href="http://docutils.sourceforge.net/README.html#quick-start">these instructions</a> because of course installing it with pip doesn't give you the tools you need in the next step.

Then, in the tar ball there is a /tools directory in which all of the parsers are. Of which I only need rst2html.py, which I have to now put on the path.

In reST, the underline/overline for a title must be at least as long as the title text. Why? Markdown doesn't care. It's only semantic anyway.

Underscores, double colons and quotes are not easy to get right. Markdown feels more natural with parans.

So, markdown generates HTML fast and easily. reST has a greater depth with LaTeX and <a target=blank href="http://sphinx.pocoo.org/">Sphinx</a>, which is the best documentation generation tool ever.

This discussion was also nicely covered <a target=blank href="http://stackoverflow.com/questions/34276/markdown-versus-restructuredtext">here</a>.

