# Less css handler for connect-assetmanager

connect-assetmanager: https://github.com/mape/connect-assetmanager

connect-assetmanager-handlers: https://github.com/mape/connect-assetmanager-handlers


## Express 3 config

#### package.json dependencies:

```
"dependencies": {
  "express": "3.4.0",
  "jade": "*",
  "connect-assetmanager": "*",
  "connect-assetmanager-handlers": "*",
  "connect-assetmanager-less-handler": "*"
}
```

#### app.js config:

```
var assetManager = require('connect-assetmanager');
var assetHandler = require('connect-assetmanager-handlers');
var lessHandler = require('connect-assetmanager-less-handler');

var assetManagerGroups = {
    'css': {
        'route': /\/static\/css\/[0-9]+\/.*\.css/,
        'path': './assets/less/',
        'dataType': 'css'
        'files': [
            'style.less'
        ],
        'preManipulate': {
            '^': [
            	  lessHandler,
                assetHandler.yuiCssOptimize,
                assetHandler.fixVendorPrefixes,
                assetHandler.fixGradients,
                assetHandler.replaceImageRefToBase64(root)
            ]
        }
    }
};

var assetsManagerMiddleware = assetManager(assetManagerGroups);

app.use(assetsManagerMiddleware);
```

#### /assets/less/style.less:
```
@import "variables.less";

body {
  padding: 50px;
  font: 14px "Lucida Grande", Helvetica, Arial, sans-serif;
}

a {
  color: @color;
}
```
