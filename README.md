# PROSErial

> A format to include structured data into prose


Some software is mainly used for storing and serving human created date (like office documents, email, blogs, wikis, websites); in contrast to software used to store machine aggregated data (like weather forecasts) or software for real computing (like protein folding).
This human created content gets stored in plain files, files with markup (like xml) or databases. Databases have big benefits in indexing, metadata and integrity of data.
But once you decide using a content-management-system or a framework, you are tied to the applications own database scheme.

Why cant you separate the data storage in real files, like UNIX: [Store data in flat text files](https://en.wikipedia.org/wiki/Unix_philosophy)

It would be very great to unbind applications from the Drupal-, Wordpress-, zend-data etc scheme. For prose orientated applications, with not so structured data, like blogs, wikis or common websites, I would prefer a more __human-readable-writable content format__. Lets call it __PROSErial__. 

Of course you could process any content representation to a content repository (like JCR), but every step of processing is a source of error. So I want an human-readable-writable content repository to have the freedom to work on it direct, without any software between.

Most [staticsitegenerators](https://staticsitegenerators.net/) already use some plain file to store their content in a mix from prose and structure (e.g. [Jekyll](https://raw.githubusercontent.com/mojombo/mojombo.github.io/master/_posts/2015-06-19-replicated.md) ), but not standardized and so not compatible.


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

You can use yaml, JSON, xml or csv. But often you need only key-values like [wordpress custom fields](https://codex.wordpress.org/Custom_Fields), so you could use some syntax from prose. The [definition list](https://www.w3.org/TR/html401/struct/lists.html#h-10.3) is supported by [some](http://talk.commonmark.org/t/description-list/289/12) markdown implementations.

   pagetitle
   : Some alternative title
   metakeywords
   : some us less words used not by dr who



## delimiter
To separate prose from structure you have to use a separator. This should be a string not already used, but easy to remember. 

Jekyll [uses](https://raw.githubusercontent.com/mojombo/mojombo.github.io/master/_posts/2015-06-19-replicated.md) the yaml separator ''---'', but __mandatory__ and before the prose. So why dont use someting like the [unix shebang](https://en.wikipedia.org/wiki/Shebang_%28Unix%29) (''#!'') with the following structure language (''#!yaml'', ''#!xml'', etc). 

lets use a (underline) heading from the used [light markup](https://en.wikipedia.org/wiki/Lightweight_markup_language#Underline), with a [magic string](https://en.wikipedia.org/wiki/Magic_string), so when editing prose you see the structure as own heading (syntaxcoloring, automatic TOC). As magic string you could use some [Disemvoweling](https://en.wikipedia.org/wiki/Disemvoweling) (dsmvwlng):

* meta (mt) is a little bit short
* serialization (srlztn)
* structure (strctr)

<pre>
strctr
===============
</pre>


Or you use no limiter at all. Mediawiki uses a special internal link ''[[Category:xxxxxx]]''. It does not matter where you put on this special link in your text, you will get a tag, but the link to the tag wont show up at the position in text.

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

## Not focused

Some databases offer you workspaces and versioning, but you could use git for this.

## Similar
* NoSQL has also scheme-less, but you have still prose as part of the content. Some NoSQL-DB use JSON, you still have to fill in your (markdown-)prose into a JSON Object. 
* The ((p:Content Repository for Java Technology API)) (JCR), now used by Symfony, is imho very useful for "real" structured data services like flickr, yelp, imdb etc.  


## Status of this documents

I thought about this while I was getting user feedack on my ssg [drfrederson](https://github.com/klml/drfrederson). I am very open for comments or change requests.
