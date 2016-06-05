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
