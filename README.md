# Atom Tool Bar

This package provides extensible tool bar for Atom.

**Note:** this package by itself adds an empty toolbar. To propagate it with icons you can [install plugins](#plugins).

![Horizontal](http://cl.ly/image/2w0u3c1x1K3W/Screenshot-2015-04-21-16.46.49.png)

![Vertical](http://cl.ly/image/1t3U3F191p35/Screenshot-2015-04-21-16.45.46.png)

![Different Sizes](http://cl.ly/image/3v1N2F3e3I47/Screenshot-2015-04-21-16.45.46_2.png)

![Light Theme](http://cl.ly/image/0g043b1e0P1X/Screenshot-2015-04-21-16.46.02.png)

## Configuration

### Orientation

* Top
* Right
* Bottom
* Left

### Icon size

* Small *(16px)*
* Big *(24px)*
* Large *(32px)*

## Plugins

* [tool-bar-main](https://atom.io/packages/tool-bar-main)
* [flex-tool-bar](https://atom.io/packages/flex-tool-bar)

## Integrating tool bar with your package

By itself this package just shows empty tool bar. To add buttons and spacers to the tool bar, use the following code.

In `package.json`:

```json
"package-dependencies": {
  "tool-bar": "^0.1.0"
},
"consumedServices": {
  "tool-bar": {
    "versions": {
      "^0.1.0": "consumeToolBar"
    }
  }
}
```

In your package main file, add the following method with the same name as in your `package.json`:

```coffeescript
consumeToolBar: (toolBar) ->
  @toolBar = toolBar 'another-tool-bar'

  # Adding button
  @toolBar.addButton
    icon: 'octoface'
    callback: 'application:about'
    tooltip: 'About Atom'

  # Adding spacer
  @toolBar.addSpacer()

  # Using custom icon set (Ionicons)
  button = @toolBar.addButton
    icon: 'gear-a'
    callback: 'application:show-settings'
    tooltip: 'Show Settings'
    iconset: 'ion'

  # Disable button
  button.setEnabled false

  # Function with data as a callback
  @toolBar.addButton
    icon: 'alert',
    callback: (data)->
      alert data
    tooltip: 'Show Alert'
    data: 'foo'

  # Adding spacer and button at the beginning of the tool bar
  @toolBar.addSpacer priority: 10
  @toolBar.addButton
    icon: 'octoface'
    callback: 'application:about'
    priority: 10
```

The method `addButton` requires an object with at least the properties `icon` and `callback`.
The remaining properties `tooltip`, `iconset` (defaults `Octicons`), `data` and `priority` (defaults `50`) are optional.

## Supported icon sets

* [Octicons](https://octicons.github.com) (Atom's flavour)
* [Ionicons](http://ionicons.com)
* [FontAwesome](http://fortawesome.github.io/Font-Awesome)
* [Foundation](http://zurb.com/playground/foundation-icon-fonts-3)

## Authors

* [Wojtek Siudzinski](http://suda.pl)
* [Jeroen van Warmerdam](https://github.com/jerone)

## Contributors

Issues and pull requests are very welcome. Feel free to write your own packages using this one.
For all contributions credits are due:

* [Pascal Bihler](https://github.com/pbihler)
* [Ryo Narita](https://github.com/cakecatz)
* [Nikita Gusakov](https://github.com/nkt)
* Carlos Santos
