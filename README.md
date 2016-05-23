# PROSErial

> under construction

Most [staticsitegenerators](https://staticsitegenerators.net/) use plain file to store their content in a mix from prose and structure: [Jekyll Front Matter](https://jekyllrb.com/docs/frontmatter/) ([standalone](https://github.com/jxson/front-matter)) is widely used by several other systems.

There are some confussing disadvantages for "normal" users:

* it is __mandatory__, if you just want to write text, users will stumble over the YAML front matter block
* [files must __begin__ with YAML Front Matter.](https://jekyllrb.com/docs/posts/) 

## form
A "human-readable-writable content format" should start with a plain part in Markdown (or any other light markup) and after a [delimiter](#delimiter) structured content (for attributes, metadata, tagging etc), written in YAML (or similar). The position of structured content should be __below__ the prose, prose is always more important.
And structured content should be __not__ be mandatory, somtimes you just want to have text. If you have only content, just start with the delimiter (like a shebang).

## prose
### prose included structure

Next to classic text-intrinsic structure (like headings, list) there are some new text structure elements, you should handle.

* ''#'' hashtag are often used as  tags. But this will conflict with markdown headings.
* ''@'' for personal mentions or places

### prose additionals
Most light markup dont have links to internal pages or references. Most wikimarkups like mediawikitext, tikiwiki, dokuwiki use two and closing square brackets (''[[other page]]''), some ticketing systems (like github) use a hashtag (''#1234'').

And you have to define some specialties:

* how to define the [html page title](http://www.w3schools.com/tags/tag_title.asp), if not defined from the metadata. You could use the a pre h1 header on the page like [gollum](https://github.com/gollum/gollum/wiki#custom-titles-via-cli), but why not use the first h1 header on the page itselfe. In 89% of all cases "the" h1 is equal to the titletag. For the rest use metadata. Fortunately you can [Tell Gollum to use the first \<h1> as page title](https://github.com/gollum/gollum).
* in the same way you could define __excerpts__ or the __metadescription__: use the first paragraph or override it with structured data. Or, like Wordpress, expand the excerpt with the [more tag](https://en.support.wordpress.com/more-tag/).

## structure

Of course [yaml](http://yaml.org/), the _human friendly data serialization standard for all programming languages_, should be the standard.

Beside yaml you could use JSON, xml or csv. Define this in the [delimiter](#delimiter). 

To have it more easier for users, use some, well known, syntax from prose. Often you need only key-values like [wordpress custom fields](https://codex.wordpress.org/Custom_Fields). The [html definition list](https://www.w3.org/TR/html401/struct/lists.html#h-10.3) is supported by [some](http://talk.commonmark.org/t/description-list/289/12) markdown implementations.

```
pagetitle
: Some alternative title
metakeywords
: some us less words used not by dr who
```
The advantage is, users could use the same syntax for key-values in prose text as for document structure.  

## delimiter
To separate prose from yaml-structure you have to use a separator. This should be a string not already used, but easy to remember. 

Jekyll [uses](https://raw.githubusercontent.com/mojombo/mojombo.github.io/master/_posts/2015-06-19-replicated.md) the yaml separator ''---'', but __mandatory__ and before the prose. 

lets use a (underline) heading from the used [light markup](https://en.wikipedia.org/wiki/Lightweight_markup_language#Underline), with a [magic string](https://en.wikipedia.org/wiki/Magic_string), so when editing prose you see the structure as own heading (syntaxcoloring, automatic TOC). As magic string you could use some [Disemvoweling](https://en.wikipedia.org/wiki/Disemvoweling) (dsmvwlng):

* meta (mt) is a little bit short
* serialization (srlztn)
* structure (strctr)

<pre>
strctr
===============
</pre>

### non yaml

If you want to use a alternative to yaml for [structure](#structure), define it with the [unix shebang](https://en.wikipedia.org/wiki/Shebang_%28Unix%29) (''#!'').

('''', etc).

<pre>
#!xml
</pre>
or
<pre>
#!json
</pre>
or
<pre>
#!md
</pre>


### no delimiter
Or you use no limiter at all. Mediawiki uses a special internal link ''[[Category:xxxxxx]]''; _Category_ is the magic word to create a category for the page instead a link. It does not matter where you put on this special link in your text, you will get a tag, but the link to the tag wont show up at the position in text.

Of course this is only useful for key-value information, like tags, and not complex objects.

## identify

Which extension and mimetype should to choose? Using the  extension from the prose-markup or an own (and again another;() extension like ''.mdyaml'' and ''text/markdown-yaml''


## Pro Cons
Of course there are some disadvantages:

* not [well formed](https://en.wikipedia.org/wiki/Well-formed_document) like xml, (but it is possible to parse this md-yaml mixup)
* no datatype specification for structured data (but in most blogs or wikis most metadata are strings and dates)

but also advantages:
* you could work with these file directly in your (web)-editor and with bash: grep, sed, etc
* decoupling CMS: work with different processing tools on the same application 
* no processing needed from user input to storage (despite the user wants some WYSIWI{G|M}- markdowneditor)
* easy and direct diff views (done by git)
* better control of your prose, due no interpretation is needed to store (but this is more a markdown pro)

## Status of this document

I thought about this while I was getting user feedack on my ssg [drfrederson](https://github.com/klml/drfrederson). I am very open for comments or change requests. 

### Not focused

Some databases offer you workspaces and versioning, but you could use git for this.

### Similar
* NoSQL has also scheme-less, but you have still prose as part of the content. Some NoSQL-DB use JSON, you still have to fill in your (markdown-)prose into a JSON Object. 
* The [Content Repository for Java Technology API](https://en.wikipedia.org/wiki/Content_repository_API_for_Java) (JCR), now used by Symfony, is imho very useful for "real" structured data services like flickr, yelp, imdb etc.  

