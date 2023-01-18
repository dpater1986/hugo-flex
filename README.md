# Hugo Flex

A lightweight Hugo theme leveraging CSS Flexbox.

This theme is verified to work with Hugo versions v0.105–v0.110.


## Features

- Flexbox-based responsive layout
- 100% speed score on PageSpeed Insight
- No framework
- No javascript
- Full posts in RSS feed
- RSS page looks like a normal page

Optional features:

- Show summaries on homepage
- Schema.org, Open Graph and Twitter Cards metadata
- Utterances comments widget
- Custom CSS and JS may be added [site-wide](#custom-css-and-js), or [dynamically](#dynamically-embedded) with shortcodes
- Built-in shortcodes:
  - [Netlify contact form](#netlify-contact-form)
  - Privacy-friendly [Soundcloud player](#soundcloud-player)


## Example

The [demo site](https://de-souza.github.io/hugo-flex/) is built from the [hugoBasicExample](https://github.com/gohugoio/hugoBasicExample) repository.

A complete starter template specifically made for this theme is also available at [scivision/hugo-flex-example](https://github.com/scivision/hugo-flex-example).


## Installation

1. [Install Hugo](https://gohugo.io/installation/).

2. [Create a Hugo site](https://gohugo.io/getting-started/directory-structure/).

3. Open a command prompt at the root of the site and download the theme:

```bash
git init
git submodule add https://github.com/de-souza/hugo-flex.git themes/hugo-flex
```

4. Add the theme to the [site configuration](https://gohugo.io/getting-started/configuration/). If the configuration file is called `hugo.yaml`:

```bash
echo 'theme: hugo-flex' >> hugo.yaml
```


## Updating

Open a command prompt at the root of the site and update the theme:

```bash
git submodule update --remote --rebase
```


## Configuration

Any part of the default theme configuration can be overwritten in the [site configuration](https://gohugo.io/getting-started/configuration/):

```yaml
params:
  color: teal           # Any color in CSS syntax
  width: 42rem          # Any length in CSS syntax / leave empty to span page
  divider: \a0          # Any string in CSS syntax / leave empty for no divider
  footer: >-            # HTML spaces (&#32;) are needed before HTML elements
  footer: >-            # HTML spaces (&#32;) are needed before HTML elements
    Except where otherwise noted, content on this site is licensed under a &#32;
    <a href="http://creativecommons.org/licenses/by/4.0/" rel="license">Creative
    Commons Attribution 4.0 International License</a>.
  rss: To subscribe to this RSS feed, copy its address and paste it into your
    favorite feed reader.
  summaries: false      # Set to true to show summaries of posts on homepage
  schema: false         # Set to true to add Schema.org metadata
  opengraph: false      # Set to true to add Open Graph metadata
  twittercards: false   # Set to true to add Twitter Cards metadata
  utterances:
    repo:               # Set to Utterances repo URL to add Utterances comments
    issueterm: pathname
    theme: github-light
  netlify:
    honeypot: false     # Set to true to add honeypot field in contact form
    recaptcha: false    # Set to true to add recaptcha challenge in contact form
  # css:                # Uncomment to add custom CSS from the assets directory
  #   - css/foo.css
  #   - bar.css
  # js:                 # Uncomment to add custom JS from the assets directory
  #   - js/foo.js
  #   - bar.js

menu:
  nav:
  - name: About
    url: about/
    weight: 1
  - name: Posts
    url: post/
    weight: 2
  - name: Tags
    url: tags/
    weight: 3
  - name: Categories
    url: categories/
    weight: 4
  - name: RSS
    url: index.xml
    weight: 5
```


## Built-In Shortcodes

### Netlify Contact Form

A contact form that works with the Netlify form handling service can be inserted with the shortcode:

```
{{< contact >}}
```

A custom success page URL may be given as a parameter:

```
{{< contact "/success" >}}
```

### Soundcloud Player

A privacy-friendly Soundcloud player can be inserted with the shortcode:

```
{{< soundcloud 123456789 >}}
```

The parameter is the track ID. It can be extracted from the "embed" sharing menu on the track's webpage.


## Custom CSS and JS

This theme offers two ways to add custom CSS or JS assets, allowing minor modifications to be applied without needing to create a fork.

### Site-Wide

Custom CSS and JS files can be added to the base asset loaded by every page. To do so, their filenames can be added to the site configuration:

```yaml
params:
  css:
    - css/foo.css
    - bar.css
  js:
    - js/foo.js
    - bar.js
```

The paths are relative to the project working directory.
In this example, the file paths relative to the site root would be `assets/css/foo.css`, `assets/bar.css`, `assets/js/foo.js`, and `assets/bar.js`.


### Dynamically Embedded

Sometimes, custom CSS or JS are only needed on specific pages. This theme offers a mechanism to load assets a single time on the pages where a shortcode is used, even if the shortcode is used more than once on the same page.

To load a resource on each page where a shortcode is used, the template for this shortcode must add the resource to the `css` or `js` key of the [Scratch variable](https://gohugo.io/functions/scratch/).
For instance, a shortcode template `myshortcode.html` containing the line

```html
{{ resources.Get "myscript.js" | fingerprint | .Page.Scratch.SetInMap "js" "myscript" }}
```

will load `myscript.js` once on every page where `myshortcode` is used.

As an example, this is the template for the built-in Soundcloud shortcode:

```html
{{ resources.Get "css/soundcloud.css" | minify | fingerprint | .Page.Scratch.SetInMap "css" "soundcloud" }}
{{ resources.Get "js/soundcloud.js" | minify | fingerprint  | .Page.Scratch.SetInMap "js" "soundcloud" }}
<div class="Soundcloud" data-id="{{ .Get 0 }}"></div>
```

## License

This theme is licensed under the [Apache License 2.0](https://github.com/de-souza/hugo-flex/blob/master/LICENSE).
