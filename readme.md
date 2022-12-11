# Setup
1. create a package.json 
```
npm init -y
```
2. install webpack
```
npm i -D webpack webpack-cli webpack-dev-server
```
3. install sass
```
npm i -D sass sass-loader css-loader
```
4. install pug
```
npm i -D pug pug-plugin 
```
5. setup webpack.json
```js
//webpack.config.js
const path = require('path');
const PugPlugin = require('pug-plugin');

module.exports = {
  entry: {
    index: './src/views/index.pug',
    about: './src/views/about.pug'
    //☝🏽 Insert your PUG HTML files here
  },
  output: {
    path: path.join(__dirname, 'dist/'),
    publicPath: '/',
    filename: 'assets/js/[name].[contenthash:8].js'
    //☝🏽 Output filename of files with hash for unique id
  },
  plugins: [
    new PugPlugin({
      pretty: true,
      //☝🏽 Format HTML (only in dev mode)
      extractCss: {
        filename: 'assets/css/[name].[contenthash:8].css'
      }
    })
  ],
  module: {
    rules: [
      {
        test: /\.pug$/,
        loader: PugPlugin.loader
        //☝🏽 Load Pug files
      },
      {
        test: /\.(css|sass|scss)$/,
        use: ['css-loader', 'sass-loader']
        //☝🏽 Load Sass files
      },
      {
        // To use images on pug files:
        test: /\.(png|jpg|jpeg|ico)/,
        type: 'asset/resource',
        generator: {
          filename: 'assets/img/[name].[hash:8][ext]'
        }
      },
      {
        // To use fonts on pug files:
        test: /\.(woff|woff2|eot|ttf|otf|svg)$/i,
        type: 'asset/resource',
        generator: {
          filename: 'assets/fonts/[name][ext][query]'
        }
      }
    ]
  },
  devServer: {
    static: {
      directory: path.join(__dirname, 'dist')
    },
    watchFiles: {
      paths: ['src/**/*.*', 'assets/scss/**/*.*'],
      //☝🏽 Enables HMR in these folders
      options: {
        usePolling: true
      }
    }
  },
  stats: 'errors-only'
  //☝🏽 For a cleaner dev-server run
};
```
1. clone [here](https://nicepage.com/ht/1241583/new-technology-perspectives-html-template) 