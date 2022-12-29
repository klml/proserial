# PROSErial

> under construction

Most [staticsitegenerators](https://staticsitegenerators.net/) use plain file to store their content in a mix from prose and structure.
[Front Matter](https://github.com/jxson/front-matter) is widely used by several other systems, like [Jekyll](https://jekyllrb.com/docs/frontmatter/) or [HUGO](https://gohugo.io/content-management/front-matter/).

There are some confusing disadvantages for "normal" users:

* it is __mandatory__, if you just want to write text, users will stumble over the YAML front matter block
* [files must __begin__ with YAML Front Matter.](https://jekyllrb.com/docs/posts/) 

## form

A "human-readable-writable content format" should start with a plain part in Markdown (or any other light markup) and after a [delimiter](#delimiter) structured content (for attributes, metadata, tagging etc).
The position of structured content should be __below__ the prose, prose is always more important.

Front-matter requires a start_delimiter _and_ an end_delimiter.
You can omit the delimiter next to end-of-file (or beginning) and use just __one__ [delimiter](#delimiter).

And structured content should be __not__ be mandatory, somtimes you just want to have text.
If you have only structured content, just start with the delimiter (like a shebang).

The structured content should use [YAML](https://yaml.org).
[Beside yaml](#non-yaml) you could use JSON, xml or csv. Define this in the [delimiter](#delimiter). 

## delimiter

To separate prose from yaml-structure you have to use a separator. This should be a string not already used, but easy to remember. 
Jekyll [uses](https://raw.githubusercontent.com/mojombo/mojombo.github.io/master/_posts/2015-06-19-replicated.md) the yaml separator ''---'', but __mandatory__ and before the prose. 

Lets use the [shebang](https://en.wikipedia.org/wiki/Shebang_(Unix)) (''#!'') and the used markup.

```
#!yaml
metakeywords: "some us less words used not by dr who"
pagetitle: "Some alternative title"
```

### non yaml

If you want to use an alternative to yaml for [structure](#structure):

```
#!json
{
  "metakeywords": "some us less words used not by dr who",
  "pagetitle": "Some alternative title"
}
```
or even

```
#!xml
<?xml version="1.0" encoding="UTF-8" ?>
<root>
  <metakeywords>some us less words used not by dr who</metakeywords>
  <pagetitle>Some alternative title</pagetitle>
</root>
```

To have it more easier for users, use some, well known, syntax from prose. Often you need only key-values like [wordpress custom fields](https://codex.wordpress.org/Custom_Fields).
The [html definition list](https://www.w3.org/TR/html401/struct/lists.html#h-10.3) is supported by [some](http://talk.commonmark.org/t/description-list/289/12) markdown implementations.

```
#!md
pagetitle
: Some alternative title
metakeywords
: some us less words used not by dr who
```
The advantage is, users could use the same syntax for key-values in prose text as for document structure.  



## Cons

Of course there are some disadvantages:

* not [well formed](https://en.wikipedia.org/wiki/Well-formed_document) like xml, (but it is possible to parse this md-yaml mixup)
* no datatype specification for structured data (but in most blogs or wikis most metadata are strings and dates)

## In the wild

Not exactly PROSErial, but hitting my main requirement: _optionality_ and _end-of-file_.

* [pandoc extension-yaml_metadata_block](https://pandoc.org/MANUAL.html#extension-yaml_metadata_block)


## Status of this document

I thought about this while I was getting user feedack on my ssg [drfly](https://github.com/klml/drfly).
I am very open for comments or change requests.
