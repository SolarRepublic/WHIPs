# WHIP-002: App Profiling in HTML Metadata

```
Number:  WHIP-002
Title:   App Profiling in HTML Metadata
Type:    Standard
Status:  Draft
Authors: Blake Regalia (@blake-regalia)
Created: 2022-09-01
```


## Abstract

WHIP-002 establishes a set of best practices for Web3 Apps to follow when publishing their Web3 profile information (i.e., concise app name, scalable app icon, and so forth) in HTML metadata.


## Motivation

In the current ecosystems, Wallet vendors are forced to make decisions about how to represent a Web3 App's profile to the end-user, due to the lack of an established set of best practices. Oftentimes, Wallets will host or bundle a proprietary set of hard-coded profiles of the Apps they support, rather than dynamically sourcing the profile from the Web3 App itself.


## Specification

### 1. App Name

Sets the name that Wallets will use to represent your App to the end-user.


##### TLDR;

Use the [standard `application-name`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta/name) metadata to define a concise name for your App:
```html
  <!-- overrides name set by <title>, use short name for better UX -->
  <meta name="application-name" content="App Demo">
```


##### Purpose

Apps should provide a concise name for their app, explicitly defined in metadata. It is different from the `<title>` of the page which may differ across the site and include information like document name or status.


##### Requirements

A `<meta>` element with the following requirements:
1. Must be a direct descendent of the document's `<head>` element.
2. Must have its `name` attribute set to `"application-name"`.
3. Must have its `content` attribute set to the name of their app.


##### Supplementals

Wallets may use the following JavaScript snippet to obtain an App's name:
```js
const appName = document.head.querySelector('meta[name="application-name"][content]').content;
```


### 2. App Icon

Sets the icon that Wallets will use to represent your App to the end-user.


##### TLDR;

Include an SVG [link icon](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/rel#attr-icon) in metadata to define a scalable icon for your App:
```html
  <!-- SVG allows Wallet to render your icon at its maximum resolution -->
  <link rel="icon" type="image/svg+xml" href="/favicon.svg">
```


##### Purpose

Apps should provide a scalable icon to represent their app, allowing Wallets to render them at the desired resolution.


##### Requirements

A `<link>` element with the following requirements:
1. Must be a direct descendent of the document's `<head>` element.
2. Must have its `rel` attribute set to `"icon"`.
3. Must have its `type` attribute set to the Media Type: `"image/svg+xml"`.
4. Must have its `href` attribute set to the URL of the SVG.


##### Supplementals

Wallets may use the following JavaScript snippet to obtain the URL of an App's icon:
```js
const appIconUrl = document.head.querySelector('link[rel="icon"][type^="image/svg+xml"][href]').href;
```


##### Considerations

Some Apps might be unable to produce a scalable vector graphic if their icon only exists in raster form. As a fallback, Wallets may choose to use the highest resolution icon available in the metadata, but this behavior is up to the Wallet vendors and is outside the scope of this specification.


## Reasoning

The [Web app manifests standard](https://developer.mozilla.org/en-US/docs/Web/Manifest) for Progressive Web Apps (PWAs), while providing the ability to declare similar attributes, serves a completely different use case. First of all, many Wallets operate as a web extension which PWAs are incompatible with since browsers create a standalone view for them, leaving extensions unable to access the PWA content. Second of all, the intents are mutually exclusive: Web Pages may wish to provide a PWA experience to end users completely separate from a Web3 experience. WHIP-002 provides the least intrusive means for Apps to declare their Web3 profile for such purposes.


## Backwards Compatibility

WHIP-002 is merely a set of best practices on top of existing HTML standards for web applications. Apps should expect to employ minimal changes in order to meet these criteria.


## Examples

A complete example of an App abiding to WHIP-002:

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">

  <!-- HTML page title -->
  <title>Homepage for MyApp: Doing Stuff Right</title>

  <!-- HTML favicons with proper annotations -->
  <link rel="icon" type="image/png" sizes="16x16" href="/favicon-16px.png">
  <link rel="icon" type="image/png" sizes="32x32" href="/favicon-32px.png">

  <!-- Apple's non-standard icons -->
  <link rel="apple-touch-icon" type="image/png" sizes="180x180" href="/apple-touch-icon.png">


  <!-- WHIP-002 App Name: overrides name set by page title -->
  <meta name="application-name" content="MyApp">

  <!-- WHIP-002 App Icon: overrides low-res raster icons -->
  <link rel="icon" type="image/svg+xml" href="/favicon.svg">
</head>
<body>
  <h1>Welcome to MyApp</h1>
</body>
</html>
```


## References

- [Standard `application-name` metadata](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta/name)
- [HTML link icon](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/rel#attr-icon)