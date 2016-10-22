# Floating Form Labels ([Demo](http://codepen.io/jChris85/pen/jrZypv))
Floating Form Labels takes [this concept from Matt D. Smit](https://dribbble.com/shots/1254439--GIF-Mobile-Form-Interaction) and wraps it into an easy to use jQuery plugin. [This blog post by Brad Frost](http://bradfrost.com/blog/post/float-label-pattern/) explains why floating labels is a desirable pattern when dealing with inline form labels.

![Floating Form Labels Demo](https://cloud.githubusercontent.com/assets/412895/19565872/9ff91416-9712-11e6-8f2f-2e05fe6ac5d2.gif)

> But there are other code snippets out there that do the same thing! Why should I choose this one?

Floating Form Labels ...
* is [UMD](https://github.com/umdjs/umd) capable (can be loaded with any module loader)
* supports the `placeholder` attribute
* is markup agnostic (works with nearly any markup)
* works with inputs _and_ textareas

## Installation
We recommend using a package manager to install Floating Form Labels as a dependency of your project. Please read the docs of your package manager if you don't know how to use it.

* [npm](https://www.npmjs.com/package/floating-form-labels): `npm install floating-form-labels`
* Bower: `bower install floating-form-labels`

You can add `--save` as parameter if you want to add the plugin into your `package.json` or `bower.json`.

Alternatively, you can download the plugin directly from GitHub, unzip the folder, and copy the file `floating-form-labels/dist/floatingFormLabels.min.js` into your project directory.

## Usage
### HTML
To begin, you'll need to write the markup for the form. It's recommended that you use a unique class name for your container elements, we're using `.ffl-wrapper` in the example below. Add your `label`s and `input`s inside these container elements.

By default Floating Form Labels will look within the containers for `label`s with the class name `ffl-label`, though you can change the class name it searches for in the javascript configuration options.

#### Example
```html
<div class="ffl-wrapper">
    <label class="ffl-label" for="input-1">Label for field 1</label>
    <input id="input-1" type="text">
</div>
<div class="ffl-wrapper">
    <label class="ffl-label" for="input-2">Label for field 2</label>
    <input id="input-2" type="text">
</div>
```

### JavaScript
Next, you need to add `floating-form-labels/dist/floatingFormLabels.min.js` and jQuery somewhere in your project directory, then load them on your page. To activate the script you need to call `floatingFormLabels()` on the container elements as shown below.

#### Example
```javascript
$('.ffl-wrapper').floatingFormLabels();
```

If you don't have the control of the HTML and want to use the plugin on custom markup you can specify the class names in the configuration options.
```javascript
$('.your-custom-wrapper').floatingFormLabels({
    label: 'label',
    floatedClass: 'postponed'
});
```

If you want to check if a label has been floated programmatically, you use can use events like so.
```javascript
$('label#label-for-input-1').on('toggle.ffl', function (event, ffl) {
    // log out the current state of the label
    console.log(ffl.floated);
});
```

#### Javascript Options
| Option | Value | Default | Description |
|---|---|---|---|
| label | _String_ | '.ffl-label' | The selector to use to find label elements within the containers. |
| formElements | _String_ | 'input, textarea' | The element selectors for the form elements Floating Form Labels will watch. |
| floatedClass | _String_ | 'ffl-floated' | The class that is added to a label when it becomes floated. |

#### Events
The following events are fired on your wrapping container:

| Event | Returns | Description |
|---|---|---|
| init.ffl | _Instance of plugin_ | Fires when Floating Form Labels is ready. |
| toggle.ffl | _Instance of plugin_ | Fires on every interaction with the input. |


### Sass
By default Floating Form Labels just adds and removes classes from the affected DOM elements. To actually see the effects you will need to add some CSS to style these classes. You can write the styles yourself or you can include our handy [Sass](http://sass-lang.com/) mixin that will do most of the job for you. Import the file `floating-form-labels/scss/floating-form-labels.scss` into your project's SASS stylesheet, then `@include` our mixin on the wrapping container.

#### Example
```scss
.ffl-wrapper {
    @include floating-form-labels($position-top, $reserved-space);
}
```

As you can see there are **two parameters our mixin expects**. The first one (`$position-top`) is used to move the label from its regular position above the input element. The second one (`$reserved-space`) is used to create a padding-top inside the wrapper to reserve the space for the label to get floated.

> Why didn't you choose a better way to center the label above the input?

With a _normal_ CSS centering solution you could get in trouble when more markup is added to your wrapper container (by a validation script or similar). Also, in case of textareas you don't want to have _true_ centering. This is why you have to move the labels down using a static parameter. The `$reserved-space` is necessary so the form doesn't 'jump' when a label is floated. We didn't want to negatively position the labels because this could cause issues with preceding form elements.

#### Sass Mixin Settings
| Setting | Default | Description |
|---|---|---|
| $ffl-label | ".ffl-label" | The selector string for the label to be floated inside your wrapping container. |
| $ffl-floatedClass | ".ffl-floated | The class name added added to floated labels by the script. |
| $ffl-transition-duration | 200ms | The float animation transition duration. |
| $ffl-transition-easing | ease | The float animation transition easing type. |

#### More SASS Examples
You can change the markup to your own needs or fasten up the transition by just setting two variables.

```scss
$ffl-label: ".my-own-label-class";
$ffl-transition-duration: 100ms;

.your-custom-wrapper {
    @include floating-form-labels(0.7rem, 0.5rem);
}
```

## FAQ
> I've got some ajax content in my form. Is there an update method to init the plugin for this new fields?

You can simply call the plugin again after the ajax is done. The plugin won't get double initialized on the fields that are already present.

> I have nested my input element inside the label to save the for attribute. Is this DOM structure also supported or has the input and the label to be on the same level?

Yes this structure is also supported because Floating Form Label is markup agnostic. You only have to wrap the text of the label inside an element (e.g. a `<span>`) that can be positioned above the input. For example your markup could look like this:

```html
<label class="ffl-wrapper">
    <span class="ffl-label">Label</span>
    <input type="text">
</label>
```

## Credits
- [jChris85](https://github.com/jChris85)
- [Baedda](https://github.com/Baedda)

