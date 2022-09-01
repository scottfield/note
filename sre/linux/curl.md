###Ignore ssl check:
curl -k

###download file with remote file name
curl -OJ

###show verbose info and follow up redirection without progress status info:
curl -Lvs

###specify request method:
curl -X GET/POST/PUT/DELETE

###add headers:
curl -H 'headerName: header value'

###send post request with json payload
curl -d '{"xxx": "emma", "zzz": "123"}' -H 'Content-Type: application/json' https://google.com/login


###send post request with form data
curl -d 'xxx=emma&zzz=123' -X POST https://google.com/login
###curl cookbook
https://catonmat.net/cookbooks/curl
