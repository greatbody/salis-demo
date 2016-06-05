# demo

a [Sails](http://sailsjs.org) application

# 1.tag "0.0.0"
by typing the following code,and execute it,we got a empty but well organzed structure code of  sails web site
```bash
sails new sails-demo
```
we can type
```bash
sails lift
```
then open a browser,type [http://localhost:1337](http://localhost:1337),then you can see a welcome page of sails
this demonstrate that you have successfully lunched a sails project
# 2.tag "0.0.1"
create api,by typing and execute the following code,we will be able to generate a api for "user"
```bash
sails generate api user
```
by executing the code, sails generates
```
api/controllers/UserController.js
api/models/User.js
```
then we goto `config/models.js`,change some settings
```js
module.exports.models = {
  connection: 'localDiskDb', //uncomment this
  migrate: 'alter' //uncomment this
};
```
save the file, and now we switch to bash, type
```bash
sails lift
```
then , we can visit [http://localhost:1337/user](http://localhost:1337/user)
all we got is something like this
```html
[]
```
try to create some data?
visit
[http://localhost:1337/user/create?name=vb6&birthyear=1998](http://localhost:1337/user/create?name=vb6&birthyear=1998)
you will got this
```js
{
  "name": "vb6",
  "birthyear": "1998",
  "createdAt": "2016-06-05T10:34:12.281Z",
  "updatedAt": "2016-06-05T10:34:12.281Z",
  "id": 1
}
```
# 3.tag "0.0.2"
before query, we need to add some data
visit:
http://localhost:1337/user/create?name=vb.net&birthyear=2002
http://localhost:1337/user/create?name=vb8&birthyear=2008
http://localhost:1337/user/create?name=vbs&birthyear=1998

now that we have enough data, we can do some test now

test is performed using [Postman](https://github.com/postmanlabs/postman-chrome-interceptor)

Set postman:
url:http://localhost:1337/user/find
method:POST
raw:JSON
```javascript
{
  "name": {
    "like": "%s%"
  }
}
```
then send the request,we shell get
```javascript
[
    {
        "name": "vbs",
        "birthyear": "1998",
        "createdAt": "2016-06-05T10:45:23.348Z",
        "updatedAt": "2016-06-05T10:45:23.348Z",
        "id": 4
    }
]
```
as you can see,`vbs` is the only name wish the word `s`

if we change the request to something like this
```js
{
  "name": {
    "like": "%vb%"
  }
}
```
we are certain to get
```js
[
    {
        "name": "vb6",
        "birthyear": "1998",
        "createdAt": "2016-06-05T10:34:12.281Z",
        "updatedAt": "2016-06-05T10:34:12.281Z",
        "id": 1
    },
    {
        "name": "vb.net",
        "birthyear": "2002",
        "createdAt": "2016-06-05T10:44:46.743Z",
        "updatedAt": "2016-06-05T10:44:46.743Z",
        "id": 2
    },
    {
        "name": "vb8",
        "birthyear": "2008",
        "createdAt": "2016-06-05T10:44:56.748Z",
        "updatedAt": "2016-06-05T10:44:56.748Z",
        "id": 3
    },
    {
        "name": "vbs",
        "birthyear": "1998",
        "createdAt": "2016-06-05T10:45:23.348Z",
        "updatedAt": "2016-06-05T10:45:23.348Z",
        "id": 4
    }
]
```
as the response
