<div class="toolbar">
    <h1>Laravel mix</h1>
    <div class="actions">
        <a class="action-link" href="/laravel.docs">Home</a>
    </div>
</div>

Laravel mix is a preconfigured webpack instance. The latest mix v6 is based on Webpack 5.x. We will start by installing the npm packages dependencies by running 
```
npm install
```

#### Basic setup
```
//webpack.mix.js

mix.js('resources/js/app.js', 'public/js')
    .postCss('resources/css/app.css', 'public/css', [
        //postCss plugins
    ]);
```

#### Assets compilation
By running the package.json scripts, all the CSS and JavaScript assets will be compiled and placed the public directory:
```
npm run dev

npm run prod
````

#### Advanced setup
We would cover with the advanced setup the:

* Compilation of scss files.
* Eslinting JS with Webpack eslint plugin.
* PurgeCSS.  
* Autoprefixing css with autoprefixer.
* CSS minimization with cssnano.
* Gzipping with Webpack compression plugin.
* Cache busting.


```
//webpack.mix.js

const mix = require('laravel-mix');
const ESLintPlugin = require('eslint-webpack-plugin');
const CompressionPlugin = require('compression-webpack-plugin');
const {CleanWebpackPlugin} = require('clean-webpack-plugin');
const purgecss = require('@fullhuman/postcss-purgecss');
const cssnano = require('cssnano');
const autoprefixer = require('autoprefixer');

const plugins = [
    new ESLintPlugin(),
    new CleanWebpackPlugin({
        cleanOnceBeforeBuildPatterns: [
            '**/*.gz',
            '**/*.js',
            '**/*.json',
            '**/*.txt',
            '**/*.map',
            '**/*.css'
        ]
    }),
];

const options = {};

if (mix.inProduction()) {
    plugins.push(
        new CompressionPlugin({
            filename: '[path][base].gz',
            algorithm: 'gzip',
            test: new RegExp('\\.(js|css)$'),
            threshold: 10240,
            minRatio: 0.8
        })
    );

    options.postCss = [
        purgecss({
            content: [
                './resources/views/**/*.php',
            ],
        }),
        autoprefixer(),
        cssnano()
    ];
}

mix.webpackConfig({
    plugins,
});

mix
.js('resources/js/app.js', 'public/js')
.sass('resources/scss/app.scss', 'public/css')
.options(options)
.version();

```

The Laravel mix configuration can me amended by calling the method mix.webpackConfig and passing a webpack 5 compatible configuration object.
Mix allows function call chaining as shown above. We compile js then sass then call postCSS the plugins and finally for cache busting we call the version method.

#### Reference
<a class="link" href="https://laravel.com/docs/8.x/mix" target="_blank">Laravel mix</a>  
<a class="link" href="https://webpack.js.org/configuration/" target="_blank">Webpack config</a>

