# Turbolinks

* See [Turbolinks on Github](https://github.com/rails/turbolinks)
* Currently support 2.5.x of Turbolinks. We plan to update to Turbolinks 5 soon.

## Why Turbolinks?
As you switch between Rails HTML controller requests, you will only load the HTML and you will
not reload JavaScript and stylesheets. This definitely can make an app perform better, even if
the JavaScript and stylesheets are cached by the browser, as they will still require parsing.

### Install Checklist
1. Include the gem "turbolinks".
1. Included the proper "track" tags when you include the javascript and stylesheet:
  ```erb
    <%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track' => true %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track' => true %>
  ```
1. Add turbolinks to your `application.js` file:
   ```javascript
   //= require turbolinks
   ```
Note, in the future, we might change to installing this via npm.

## Troubleshooting
To turn on tracing of Turbolinks events, put this in your registration file, where you register your components. 

```js
   ReactOnRails.setOptions({
     traceTurbolinks: true,
   });
```

Rather than setting the value to true, you could set it to TRACE_TURBOLINKS, and then you could place this in your `webpack.client.base.config.js`:

Define this const at the top of the file:
```js
  const devBuild = process.env.NODE_ENV !== 'production';
```

Add this DefinePlugin option:
```js
  plugins: [
   new webpack.DefinePlugin({
     TRACE_TURBOLINKS: devBuild,
   }),
```

At Webpack compile time, the value of devBuild is inserted into your file.

Once you do that, you'll see messages prefixed with **TURBO:** like this in the browser console:

```
TURBO: WITH TURBOLINKS: document page:before-unload and page:change handlers installed. (program)
TURBO: reactOnRailsPageLoaded
```

We've noticed that Turbolinks doesn't work if you use the ruby gem version of jQuery and jQuery ujs. Therefore we recommend using the node packages instead. See the [tutorial app](https://github.com/shakacode/react-webpack-rails-tutorial) for how to accomplish this.
