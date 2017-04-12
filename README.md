# Example apitest repo.

###Apigeetool
#####Download and install Apigeetool a Node.js module you can install with npm:
$ npm install –g apigeetool
```
MGMTSVR=https://api.enterprise.apigee.com (this is the default, override with –L $MGMTSVR)
ORG=your-org-name
UN=username@email.com:password
PW=username@email.com:password
```

#####Create (new or revision) do not Deploy
In current directory
* apigeetool deployproxy -u $UN -p $PW -o $ORG -n apitest -e test -i -d .
Create (new or revision) and Deploy
* apigeetool deployproxy -u $UN -p $PW -o $ORG -n apitest -e test -d .
#####Downlowd
* apigeetool fetchproxy -u $UN -p $PW -o $ORG -n apitest -r 2
#####List Deployments in environment
* apigeetool listdeployments -u $UN -p $PW -o $ORG -e test 
#####List Deployments for API
* apigeetool listdeployments -u $UN -p $PW -o $ORG –n apitest

###Curl commands to Management API
```
MGMTSVR = https://api.enterprise.apigee.com
UNPW = username@email.com:password
ORG = your-org-name
```

#####Create
* curl -X POST -u $UNPW "$MGMTSVR/v1/o/$ORG/apis" -d '{ "name": "apitest" }' -H 'Content-Type:application/json’

#####Download
* curl -X GET -u $UNPW ”$MGMTSVR/v1/o/$ORG/apis"
* curl -X GET -u $UNPW “$MGMTSVR/v1/o/$ORG/apis/apitest"
* curl -X GET -u $UNPW ”$MGMTSVR/v1/o/$ORG/apis/apitest/revisions"
* curl -X GET -u $UNPW ”$MGMTSVR/v1/o/$ORG/apis/apitest/revisions/1"
* curl -X GET -u $UNPW ”$MGMTSVR/v1/o/$ORG/apis/apitest/revisions/1?format=bundle" -o apitest.zip

#####Upload new revision
* curl -v -X POST -u $UNPW “$MGMTSVR/v1/o/$ORG/apis?name=apitest&validate=true&action=import -F file=@apitest.zip -H Content-Type:multipart/form-data

#####Update existing revision
* curl -v -X POST -u $UNPW $MGMTSVR/v1/o/$ORG/apis/apitest/revisions/2?validate=true -F file=@apitest.zip -H Content-Type:multipart/form-data

Docs: http://docs.apigee.com

