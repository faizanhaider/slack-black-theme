# Slack Black Theme

A darker, more contrasty, Slack theme.

# Installing into Slack

Find your Slack's application directory.

* Windows: `%homepath%\AppData\Local\slack\`
* Mac: `/Applications/Slack.app/Contents/`
* Linux: `/usr/lib/slack/` (Debian-based)


Open up the most recent version (e.g. `app-2.5.1`) then open
`resources\app.asar.unpacked\src\static\index.js`

For versions after and including `3.0.0` the same code must be added to the following file
`resources\app.asar.unpacked\src\static\ssb-interop.js`

At the very bottom, add

```js
// First make sure the wrapper app is loaded
document.addEventListener('DOMContentLoaded', function() {
  const cssURI = 'https://raw.githubusercontent.com/faizanhaider/slack-black-theme/master/slack-dark-theme.css',
    codeMirrorThemURI = 'https://raw.githubusercontent.com/faizanhaider/slack-black-theme/master/cobalt.css';  // also add the "cobalt" theme for the CodeMirror snippets

  Promise.all([cssURI, codeMirrorThemURI].map((file)=>{
    return fetch(file)
        .then( response => {
          return response.text();
        });
  })).then(files => {
    files[1] = files[1].replace(/cm-s-cobalt/g, 'cm-s-default')
    $("<style></style>").appendTo('head').html(files.join('\n'));
  });
});
```
