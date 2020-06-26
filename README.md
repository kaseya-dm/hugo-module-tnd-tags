# Tags Hugo Module

Hugo Module to genererate HTML tags. 

Remove HTML/templating concern when having to generate large amount of tags (SEO etc...)

## Requirements

Requirements:
- Go 1.14
- Hugo 0.61.0


## Installation

If not already, [init](https://gohugo.io/hugo-modules/use-modules/#initialize-a-new-module) your project as Hugo Module:

```
$: hugo mod init {repo_url}
```

Configure your project's module to import this module:

```yaml
# config.yaml
module:
  imports:
  - path: github.com/theNewDynamic/hugo-module-tnd-tags
```

## Usage

### tag

The tag partial takes 3 parameters
- name*: the tag's name: `link` or `script` etc...
- inner: The tag's content. If not set, the tag will self close.
- attr: A map with the tag's attributes.

#### Examples

##### title
```
{{ partial dict "name" "title" "inner" "Hugo Tags!") }}
```

```html
<title>Hugo Tags!</title>
````

##### link
```
{{ range resources.Match "fonts/**/*.woff*" }}
{{ $params := dict "name" "link" "attr" (dict "href" .RelPermalink "rel" "prefetch" "as" "font" "crossorigin" "") }}
{{ partial "tnd-tags/tag" $params }}
```

```html
<link as="font" crossorigin href="/fonts/files/4fe94f2e-7892-4785-9663-0350a7adf8c0.woff" rel="prefetch">
<link as="font" crossorigin href="/fonts/files/5b4bd9d6-75be-4d76-8292-7f6434b9e997.woff" rel="prefetch">
<link as="font" crossorigin href="/fonts/files/6e8e8927-5a98-49ae-9123-db1798ec6d92.woff2" rel="prefetch">
```

##### script
```
{{ with resources.Get "main.js" }}
  {{ $param := dict "name" "script" "attr" (dict "type" "text/javascript" "src" .RelPermalink "defer" "")) }}
  {{ partial "tnd-tags/tag $param }}
{{ end }}
```

```html
<script defer src="/js/main.js" type="text/javascript"></script>
```
----
```
{{ partial "tnd-tags/tag" (dict "name" "script" "inner" `
  console.log('bonjour vous!')
`) }}
```
```html
<script >
  var text = 'Hello Tag!';
  console.log(text);
</script>
```

## theNewDynamic

This project is maintained and love by [thenewDynamic](https://www.thenewdynamic.com).