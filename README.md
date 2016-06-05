# demo

a [Sails](http://sailsjs.org) application, and is a demo only

thanks to [Intro to Sails.js](https://www.youtube.com/watch?v=GK-tFvpIR7c) from where I get most of the demos

# 1.tag "0.0.0"
by typing the following code,and execute it,we got a empty but well organzed structure code of  sails web site
>code-0.0.0-1

```bash
sails new sails-demo
```
we can type
>code-0.0.0-2

```bash
sails lift
```
then open a browser,type [http://localhost:1337](http://localhost:1337),then you can see a welcome page of sails
this demonstrate that you have successfully lunched a sails project
# 2.tag "0.0.1"
create api,by typing and execute the following code,we will be able to generate a api for "user"
>code-0.0.1-1

```bash
sails generate api user
```
by executing the code, sails generates
>code-0.0.1-2

```
api/controllers/UserController.js
api/models/User.js
```
then we goto `config/models.js`,change some settings
>code-0.0.1-3

```js
module.exports.models = {
  connection: 'localDiskDb', //uncomment this
  migrate: 'alter' //uncomment this
};
```
save the file, and now we switch to bash, type
>code-0.0.1-4

```bash
sails lift
```
then , we can visit [http://localhost:1337/user](http://localhost:1337/user)
all we got is something like this
>code-0.0.1-5

```html
[]
```
try to create some data?
visit
[http://localhost:1337/user/create?name=vb6&birthyear=1998](http://localhost:1337/user/create?name=vb6&birthyear=1998)
you will got this
>code-0.0.1-6

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
>code-0.0.2-1

```javascript
{
  "name": {
    "like": "%s%"
  }
}
```
then send the request,we shell get
>code-0.0.2-2

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
>code-0.0.2-3

```js
{
  "name": {
    "like": "%vb%"
  }
}
```
we are certain to get
>code-0.0.2-4

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
# 4.tag "0.0.3"
how about limit the numbers?
>code-0.0.3-1

```js
{
  "name": {
    "like": "%vb%"
  },
  "limit": 2
}
```
then we can get only 2 of all queried results
>code-0.0.3-2

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
    }
]
```
now we get limited results but yet we have not idea how those results are arraged.
let's look at this
>code-0.0.3-3

```js
{
  "name": {
    "like": "%vb%"
  },
  "limit": 2,
  "sort": "name ASC"
}
```
and  now we can see data has been rearranged as we wish
>code-0.0.3-4

```js
[
    {
        "name": "vb.net",
        "birthyear": "2002",
        "createdAt": "2016-06-05T10:44:46.743Z",
        "updatedAt": "2016-06-05T10:44:46.743Z",
        "id": 2
    },
    {
        "name": "vb6",
        "birthyear": "1998",
        "createdAt": "2016-06-05T10:34:12.281Z",
        "updatedAt": "2016-06-05T10:34:12.281Z",
        "id": 1
    }
]
```
there are something like "LIKE",contains for instanse
now,we replace `like` from `code-0.0.3-3` with `contains` and removed "%" away 
>code-0.0.3-5

```js
{
  "name": {
    "contains": "vb"
  },
  "limit": 2,
  "sort": "name ASC"
}
```
what we get is same as `code-0.0.3-3`

If we need to get names that start with "v"
we can do this
>code-0.0.3-6

```js
{
  "name": {
    "like": "v%"
  }
}
```

or like this
>code-0.0.3-7

```js
{
  "name": {
    "startsWith": "v"
  }
}
```
