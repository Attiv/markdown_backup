在 `webpack.base.conf.js` 里

```Plain
 {
        test: /\\.js$/,
        loader: 'babel-loader',
        include: [
          resolve('src'),
          resolve('test'),
          resolve('node_modules/element-ui/src'),
          resolve('node_modules/vue-line-clamp/dist') 
          需要添加的地方用resolve
        ],
        query: {
          presets: ['env'(或者是es2015,看装的是哪个), 'stage-2']
        }
      },
```