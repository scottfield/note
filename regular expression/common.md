###auto convert string with links:
```js
strContent.replaceAll(/((https|http):\/\/[a-zA-Z0-9\.\/\_\%\-\=\?\&]+)/g,'<a href="$1">$1</a>')
```

###repeat pattern match
```js
/^([A-Z]{1}\d{3}-\w{1})(,[A-Z]{1}\d{3}-\w{1})*$/
```
