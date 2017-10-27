### single page app production deploy with firebase  
* use webpack config template  

* include in `webpack`  
~> `npm install`  
```js
module.exports = config;

if (process.env.NODE_ENV === 'production') {
  config.plugins.push(
    new webpack.DefinePlugin({
      'process.env': {
        'NODE_ENV': JSON.stringify(process.env.NODE_ENV)
      }
    }),
    new webpack.optimize.UglifyJsPlugin()
  )
};

module.exports = config;
```

* set build in `packgage.json`  
```json
//windows need 'SET' and '&&'
"scripts": {
  "build": "SET NODE_ENV=production && webpack -p"
},

//linux
"scripts": {
  "build": "NODE_ENV='production' webpack -p"
},
```
~> build project `npm run build`  

* install firebase  
~> `npm install --save-dev firebase-tools`  
~> add firebase config in `package.json`  
```json
"scripts": {
  //..other scripts
  "deploy": "npm run build && firebase deploy",
  "firebase-init": "firebase login && firebase init"
},
```

* create new project on firebase account  

* init firebase  
~> run `npm run firebase-init`  
~> select `Hosting`, build-directory(public), single-page app = y, overwrite= n  

* run `npm run deploy`