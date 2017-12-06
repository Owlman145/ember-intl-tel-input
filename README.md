# ember-intl-tel-input2

[![Build Status](https://travis-ci.org/cdatehortuab/ember-intl-tel-input.svg?branch=master)](https://travis-ci.org/cdatehortuab/ember-intl-tel-input)
[![npm version](https://badge.fury.io/js/ember-intl-tel-input2.svg)](http://badge.fury.io/js/ember-intl-tel-input2)
[![Dependency Status](https://david-dm.org/cdatehortuab/ember-intl-tel-input.svg)](https://david-dm.org/cdatehortuab/ember-intl-tel-input)
[![devDependency Status](https://david-dm.org/cdatehortuab/ember-intl-tel-input/dev-status.svg)](https://david-dm.org/cdatehortuab/ember-intl-tel-input#info=devDependencies)

An Ember.js addon for entering and validating international telephone numbers.
This project is a fork of [justin-lau/ember-intl-tel-input](https://github.com/justin-lau/ember-intl-tel-input) that is outdated.

Please check out the [demo page](http://cdatehortuab.github.io/ember-intl-tel-input/) to see the addon in action.

For more information on using ember-cli, visit [http://www.ember-cli.com/](http://www.ember-cli.com/).

## Installation

```bash
$ ember install ember-intl-tel-input2
```

## Basic Usage

Just place the `{{intl-tel-input}}` component in the handlebars template, as you would have guessed.

```htmlbars
{{intl-tel-input}}
```

The component derives from `Ember.TextField`, anything you can do with the input helper can also be done with this component.

```htmlbars
{{intl-tel-input value="555-5555"}}
```

## With Utilities Script

With the [utilities script](https://github.com/jackocnr/intl-tel-input#utilities-script) included, the `autoPlaceholder` option is automatically enabled.

```javascript
// ember-cli-build.js
module.exports = function(defaults) {
  let app = new EmberApp(defaults, {
    ...
    'ember-intl-tel-input': {
      includeUtilsScript: true, // default to false
    },
    ...
  });
  ...
};
```
Or if you want to specify your own compatible utils script (like a custom build).
```javascript
// ember-cli-build.js
module.exports = function(defaults) {
  let app = new EmberApp(defaults, {
    ...
    'ember-intl-tel-input': {
      utilsScript: 'path/to/utilsScript.js',
    },
    ...
  });
  ...
};
```
If you use both options the default utilsScript will be exported to the path specified.

```htmlbars
{{intl-tel-input}}
```

## Properties Binding

Use the following properties for binding:

*   `value` for input value
*   `selectedCountryData` for data of the currently selected country
*   `number` for formatted phone number
*   `extension` for the extension part of the number
*   `numberType` for the type of the current number
*   `isValidNumber` for the validity of the number
*   `validationError` for information about a validation error

```htmlbars
{{intl-tel-input
  allowExtensions=true
  value=value
  selectedCountryData=selectedCountryData
  number=number
  extension=extension
  numberType=numberType
  isValidNumber=isValidNumber
  validationError=validationError}}
```

## Lookup User's Country
`intl-tel-input` provides a convenient way to look up the user's country based on their IP addresses. This example uses [ipinfo.io](http://ipinfo.io/) for demonstration.

```javascript
// controller
...
geoIpLookupFunc: function(callback) {
  $.getJSON('http://ipinfo.io/')
   .always(function(resp) {
     if (!resp || !resp.country_code) {
       callback('');
     }

     callback(resp.country_code);
   });
}
...
```

```htmlbars
{{intl-tel-input
  initialCountry="auto"
  geoIpLookup=geoIpLookupFunc}}
```

## Running The Demo Page Locally

Run `ember server`, and visit the demo page at `http://localhost:4200`.

## Credits

This is a wrapper library. It simply wraps the API of [the original jQuery plugin](http://jackocnr.com/intl-tel-input.html) created by [Jack O'Connor](http://jackocnr.com/) into an [Ember.js](http://emberjs.com/) component.

The original jQuery plugin also depends on several other open-source libraries:

*   Flag images from region-flags
*   Original country data from mledoze's World countries in JSON, CSV and XML
*   Formatting/validation/example number code from Google's libphonenumber
*   Lookup user's country using ipinfo.io

~~This [addon's demo page](http://cdatehortuab.github.io/ember-intl-tel-input/) uses [Telize](http://www.telize.com/) for a fast, SSL-supported, yet FREE Geo IP service.~~

[Telize no longer provide free services due to heavy abuse](http://www.cambus.net/adventures-in-running-a-free-public-api/). The demo has switched over to [ipinfo.io](http://ipinfo.io).

The layout and color theme of the demo page comes from [Twitter's Bootstrap](http://getbootstrap.com/) and [Ember.js](http://emberjs.com/), respectively.
