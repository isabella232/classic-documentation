---
template: page-sidebar
title: "Extensions"
---

<h2 class="js-toc-ignore">Extensions</h2>

Extensions are reusable templates for making changes in the visual editor. A developer can build a extension with HTML, CSS, and JavaScript. Then, a non-technical user can insert the extension in the editor and tweak parameters. For example, a developer could build a carousel extension styled for a homepage and coded to rotate between images, and then a merchandiser could insert it and choose the right images for a specific campaign.

You can create a extension under **Implementation > Extensions**. Each extension has a unique **ID** that identifies it on the page. If the same extension is inserted in multiple places, the code will only be included once and each instance will call into it by ID. Extensions can be inserted on multiple pages, but you can choose one **Editor URL** that will appear in the extension builder. The **Name** and **Description** are human-readable text in the Optimizely interface.

![](/assets/img/js/extension-builder.png)

### Fields

Once you create the extension, you'll land in the Extension Builder. In the left sidebar, you can add optional fields. Each field defines a property that can be customized on the extension. For example, on a popup, you could provide fields to customize the message, the call to action, the width and height, and the timing of when it should appear.

Each field requires an API name, which you can use to reference it in HTML. For example, if you create a field with the **API Name** "height", you can reference it in HTML as `{{ extension.height }}` or in JS as ``extension.height``. The **Label** is a human readable name like "Popup Height", and you can add an optional **Default Value** like `400`.


You can use the extension fields and define its behavior by using the top code boxes.

### HTML

The body of the extension can be written in the HTML box. You can write any HTML here and then decide where it gets injected in the Apply JS section. In addition to vanilla HTML, you can use [mustache syntax](http://mustache.github.io/mustache.5.html) to add more advanced logic like loops and conditionals.

You can reference field values by using the API name on the extension object like ``{{ extension.title }}``. For non-escaped values like an HTML or rich text field, use triple brackets like ``{{{ extension.contents }}}``.

##### Example
```
<div class="banner" style="background-color: {{extension.color}}">
  {{{ extension.text }}}.
  <a href="{{extension.link}}">{{{ extension.link_text }}}</a>
</div>
```

### CSS

Some extensions may not need any CSS because they inherit styles from the page itself. However, you can add additional styling in the CSS box. This will be injected on the page through a `<style>` tag.

Note that CSS doesn't support field values, so if you want to use those in styling you can do it directly in the HTML via inline styles, e.g. `<div class="banner" style="background-color: {{extension.color}}">`.

##### Example
```
.banner {
  color: white;
  padding: 10px;
  position: fixed;
  top: 0px;
  z-index: 100000000;
  width: 100%;
  text-align: center;
  height: 45px;
}

.banner a {
  text-decoration: underline;
  color: white;
}

body {
 margin-top: 45px;
}
```

### Apply JS

The Apply JS code is used to inject the extension onto the page. At a minimum, it should take the HTML and insert it at a selector (which can itself be specified as a field, or hard-coded). You can use [utilities like waitForElement](#waitForElement) to [control the timing](#timing) of how your code runs. Some extensions will also have more complex logic, like calling out to an external service.

The scope of the apply JS code includes:
- `extension`: the configuration of the extension, including all fields as properties e.g. `extension.height`
- `extension.$html`: the compiled HTML
- `extension.$render`: a function to compile the HTML template on the fly, useful when dealing with asynchronous data (see below)
- `extension.$id`: the ID of the extension, e.g. `top_banner`
- `extension.$instance`: a unique identifier for a specific instance of the extension. If the extension is used more than once on a page, each one will have its own instance. Example: `AE8D40E3-785E-4A31-A9DF-4ED6E0681366`

When all the template data is available immediately, `extension.$html` will automatically render the template into final HTML. But when you want to use a extension with asynchronous data, e.g. based on an AJAX request, you can use `extension.$render` to compile the HTML template with a specific context. The render function takes an object with each value to pass through to the template.

##### Examples
```js
var utils = window.optimizely.get('utils');

// Insert at a hard-coded position
$(document).ready(function() {
  $('body').prepend(extension.$html);  
})

// Let the user choose the selector
utils.waitForElement(extension.selector).then(function() {
  $(extension.selector).append(extension.$html)  
})

// Render using asynchronous data
recommender.fetchRecommendations(productId).then(function(recos) {
  var products = recos.slice(0, extension.max);
  var html = extension.$render({
    extension: extension,
    products: products,
  });
  $(extension.selector).after(html);
}
```

### Reset JS

Reset JS is used to "clean up" after a extension. It's used in the editor, when changing field values or removing an existing extension. Reset JS should remove the element and any other side-effects.

One way to write reset JS is to use the `extension.$instance` value. For example, you could create a extension with HTML starting like this:
```html
<div class="banner" data-extension-instance="{{extension.$instance}}">
```

Then remove it using Reset JS like:
```js
$("[data-extension-instance=" + extension.$instance + "]").remove();
```
