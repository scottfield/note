###auto convert string with links:
```js
strContent.replaceAll(/((https|http):\/\/[a-zA-Z0-9\.\/\_\%\-\=\?\&]+)/g,'<a href="$1">$1</a>')
```
