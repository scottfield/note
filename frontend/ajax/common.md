###how to send a cros site request with fetch API
```
let myHeaders = new Headers();
    myHeaders.append('Content-Type', 'application/json');
    myHeaders.append('Accept', 'application/json');
    let request = new Request('http://somehost.com/api/', {method: 'POST', body: '{name:'value'}',headers:myHeaders});
    fetch(request).then(res=>res.json()).then(data=>console.log(data));
```
