# Tailwind 3 – Ember 4 – SCSS Template

Dependencies:
- @csstools/postcss-sass
- ember-cli-postcss
- postcss-import
- postcss-scss
- tailwindcss


```
  /* tailwind.config.js */
  
  module.exports = {
    content: [
      "./app/components/**/*.{html,js,hbs}",
      "./app/templates/**/*.{html,js,hbs}",
    ],
    theme: {
      extend: {},
    },
    plugins: [],
  }
```

```
  /* ember-cli-build.js */

  let app = new EmberApp(defaults, {
    postcssOptions: {
      compile: {
        extension: 'scss',
        enabled: true,
        includePaths: ['app'],
        cacheInclude: [
          /.*\.hbs$/,
          /.*\.css$/,
          /.*\.html/,
        ],
        parser: require('postcss-scss'),
        plugins: [
          { module: require('@csstools/postcss-sass') },
          { module: require('postcss-import'), options: {
            path: ['node_modules']
          } },
          require('tailwindcss')('./tailwind.config.js')
        ]
      }
    }
  });
```

```
  /* app.scss */

  @tailwind base;
  @tailwind components;
  @tailwind utilities;
```