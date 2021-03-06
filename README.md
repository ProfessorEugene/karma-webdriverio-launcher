# karma-webdriverio-launcher [forked from tatablack/karma-webdriverjs-launcher]

A plugin for Karma. Launcher for Remote WebDriver instances using WebDriverIO.

## Why another WebDriver launcher?
This implementation is inspired by the [karma-webdriver-launcher](https://github.com/karma-runner/karma-webdriver-launcher) made by the folks at Karma.

However, it uses a different WebDriver implementation ([WebdriverIO](http://webdriver.io/) instead of [wd](https://github.com/admc/wd)), and tries harder to get hold of a browser instance from Selenium Grid.

## Installation
Not published on the NPM registry yet. For the time being, you'll need to add it to your `devDependencies` with its Github url, like this:

```
  "devDependencies": {
    "karma-webdriverio-launcher": "git://github.com/ProfessorEugene/karma-webdriverjs-launcher.git#0.1.1"
  }
```

## Usage
Add a custom launcher to your Karma configuration, specifying the necessary parameters.

```javascript
customLaunchers: {
    'Remote-IE9': {
        base: 'WebdriverIO',
        config: {
            host: 'qa-builder001',
            desiredCapabilities: {
                browserName: 'internet explorer',
                version: '9'
            }
        }
    }
}
```

And then use that launcher in your browser suite configuration.

## Options
### config.host

The hostname of your Selenium Grid server, or Saucelabs instance.

### config.port

Unsurprisingly, the port where your Selenium Grid server is running, or your Saucelabs instance is connected to.

### config.desiredCapabilities

Nothing specific here. Just have a look at [Selenium documentation](https://code.google.com/p/selenium/wiki/DesiredCapabilities), and possibly WebdriverIO [README](https://github.com/webdriverio/webdriverio#desiredcapabilities).
A sample configuration might thus be:

```javascript
config: {
    desiredCapabilities: {                 // Sample configuration.
        browserName: 'internet explorer',  //
        platform: 'XP',                    // Check the documentation links above
        version: '9'                       // for additional capabilities.
    }                                      //
}
```

### config.ieDocumentMode

You might want to trigger (or avoid triggering) a specific compatibility mode for IE (see [MSDN](http://msdn.microsoft.com/en-us/library/jj676915(v=vs.85).aspx) for an explanation).
This will actually just append a parameter to the URL being loaded through Selenium, Karma itself takes care of adding the proper META tag.

```javascript
config: {
    desiredCapabilities: {
        // desired capabilities here
    },

    ieDocumentMode: 'IE=edge' // <--
}
```

### config.loglevel

WebdriverIO can be pretty informative, but you might want to skip some of its output. The loglevel parameter is passed directly to WebdriverIO, so have a look at its [documentation](https://github.com/webdriverio/webdriverio#loglevel) to determine what's the best option for you.

```javascript
config: {
    desiredCapabilities: {
        // desired capabilities here
    },
    
    logLevel: 'silent',  // <-- verbose | silent | command | data | result
}
```
