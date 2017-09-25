# Alternative codesample and preview plugins for TinyMCE 4

Those are alternative implementations of `codesample` and `preview` plugins for [TinyMCE 4](https://www.tinymce.com/)
JavaScript editor.

## codesample

This version of `codesample` plugin supports all syntax highlighting definitions provided by [PrismJS](http://prismjs.com/)
library. By default this `codesample` plugin supports the same languages as the official plugin, but you can configure
the list of available languages via [`codesample_languages`](https://www.tinymce.com/docs/plugins/codesample/#codesample_languages)
option. Note that, unlike the official plugin, this plugin does not include any PrismJS components of its own
and you need to include the necessary links to `prism.js` and `prism.css` with all language definitions
that you want to support.

## preview

This is a drop-in replacement for the official `preview` plugin. The only difference is that it can show code blocks
with syntax coloring by PrismJS.

## Usage

- Copy plugin folders to your web server content directory.
- Download the necessary [PrismJS](http://prismjs.com/) `.js` and `.css` files.
- Add links to the necessary `.js` and `.css` files to HTML code of the page which
you want to use TinyMCE 4 editor in.
- Add all the necessary options to TinyMCE 4 configuration

Example configuration:
```html
<!DOCTYPE html>
<html>
<head>
...
  <script src="/your/server/path/js/prism/prism.min.js"></script>
  <script src="/your/server/path/js/tinymce/tinymce.min.js"></script>
  <link href="/your/server/path/css/prism/prism.css" rel="stylesheet">
</head>
<body>
...

  <textarea id="editableContent"></textarea>
  <script>
    tinymce.init({
      selector: 'textarea#editableContent',
      plugins: 'advlist autolink link image', // No codesample and preview!
      toolbar: 'codesample preview',
      external_plugins: {
        codesample: '../../../common_content/js/codesample/plugin.min.js',
        preview: '../../../common_content/js/preview/plugin.min.js'
      },
      codesample_languages: [
        {text: 'Python', value: 'python'},
        {text: 'HTML/XML', value: 'markup'},
        {text: 'Django/Jinja2', value: 'django'},
        {text: 'CSS', value: 'css'},
        {text: 'JavaScript', value: 'javascript'},
        {text: 'C++', value: 'cpp'},
        {text: 'C', value: 'c'},
        {text: 'C#', value: 'csharp'},
        {text: 'Windows BAT', value: 'batch'},
        {text: 'Bash', value: 'bash'},
        {text: 'YAML', value: 'yaml'},
        {text: 'SQL', value: 'sql'},
        {text: 'reStructuredText', value: 'rest'},
        {text: 'Plain Text', value: 'none'},
    });
  </script>

...
</body>
</html> 
```

**Important Notes**:

- Do **not** include `codesample` and `preview` plugins in `plugins` configuration option! They are loaded via
  [`external_plugins`](https://www.tinymce.com/docs/configure/integration-and-setup/#external_plugins) option.
- Paths in `external_plugins` list are relative to `tinymce.min.js` file.
- Prism.js files with the necessary language definitions need to be added both to pages where
  you use TinyMCE 4 editor and to pages with authored content.

# License

LGPL v.2.1
