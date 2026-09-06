---
banner: "Assets/Banners/makimadevil.jpg"
banner_y: 0.36807
banner_x: 0.37512
banner_icon: 🕰️
---
```dataviewjs
const container = dv.container;
container.style.cssText = `margin: 0 0 24px 0;`;

const style = document.createElement('style');
style.textContent = `
  @keyframes borderFlow {
    0%   { background-position: 0% 50%; }
    50%  { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
  }
  @keyframes glowPulse {
    0%, 100% { box-shadow: 0 0 8px #00f0ff44, 0 0 20px #00f0ff22; }
    50%       { box-shadow: 0 0 16px #00f0ff88, 0 0 40px #00f0ff44; }
  }
  @keyframes scanline {
    0%   { left: -100%; }
    100% { left: 200%; }
  }
  .home-btn-wrap {
    display: inline-block;
    padding: 2px;
    border-radius: 10px;
    background: linear-gradient(270deg, #00f0ff, #7928ca, #ff0080, #00f0ff);
    background-size: 400% 400%;
    animation: borderFlow 4s ease infinite, glowPulse 2.5s ease-in-out infinite;
    cursor: pointer;
  }
  .home-btn-inner {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 10px 22px;
    border-radius: 8px;
    background: rgba(0, 0, 0, 0.75);
    position: relative;
    overflow: hidden;
  }
  .home-btn-inner::after {
    content: '';
    position: absolute;
    top: 0; height: 100%;
    width: 40%;
    background: linear-gradient(to right, transparent, rgba(0,240,255,0.08), transparent);
    animation: scanline 3s ease-in-out infinite;
  }
  .home-btn-icon {
    font-size: 1.1em;
    line-height: 1;
  }
  .home-btn-label {
    font-family: 'Courier New', monospace;
    font-size: 0.88em;
    font-weight: 400;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: #00f0ff;
    text-shadow: 0 0 8px #00f0ff88;
  }
  .home-btn-arrow {
    font-family: 'Courier New', monospace;
    font-size: 0.9em;
    color: #7928ca;
    text-shadow: 0 0 6px #7928caaa;
    transition: transform 0.2s ease;
  }
  .home-btn-wrap:hover .home-btn-arrow {
    transform: translateX(4px);
  }
  .home-btn-wrap:hover .home-btn-inner {
    background: rgba(0, 240, 255, 0.06);
  }
`;
document.head.appendChild(style);

const btnWrap = container.createEl('div');
btnWrap.className = 'home-btn-wrap';

btnWrap.onclick = () => {
    app.workspace.openLinkText('Homepage', '', false);
};

const btnInner = btnWrap.createEl('div');
btnInner.className = 'home-btn-inner';

const icon = btnInner.createEl('span');
icon.className = 'home-btn-icon';
icon.textContent = '⌂';

const label = btnInner.createEl('span');
label.className = 'home-btn-label';
label.textContent = 'Go to Homepage';

const arrow = btnInner.createEl('span');
arrow.className = 'home-btn-arrow';
arrow.textContent = '→';
```

https://portswigger.net/web-security/learning-paths/api-testing/api-testing-api-documentation/api-testing/lab-exploiting-api-endpoint-using-documentation
### API recon
To Start API testing we need to find out the api first how much data we have what is the attack surface.
If we talk about the location where the api recieves request from the server it looks like GET /api/book HTTP/1.1 
Host:example.com


### Using machine-readable documentation
We can use range of tools to analyze any machine redable api docs like burp crawler

### Identifying API endpoints
Browsing the  application which uses api can also be a good way to identify the attack surface as even u have documentation it maybe outdated while browsing the application look for paterns of /api/ or scripts that may contain something related to it even in error message of application you may find how the server actually accepts the endpoints.

### Identifying supported HTTP methods

There are some of these  methods to use HTTP request 
GET -- retrieves the data form the resource 
PATCH -- applies the partial changes to the resources
OPTION -- retrieves info on the types of request method that can be used on a resource 

An api endpoint can support different http methods. so its important to test all the possible available endpoints api can open up more attack surface 

suppose the api endpoint /api/tasks if we use 
GET /api/tasks -- it may retrieves a list of tasks 
POST /api/tasks -- creates an task
DELETE /api/tasks/1 -- Deletes an tasks

### Identifying supported content types
Api endpoints expects an specifi format data so they might give errors after changing the data format which can be usefull and can give information about it how it works 
suppose an api expects json format but u cant attack or do some injection in it bcz it will be already protected but u might able to inject something via using some other data type like xml instead of json format 

### Using Intruder to find hidden endpoints
After finding the api endpoints we can use intruder option in burp to find the hidden endpoints 

### Finding hidden parameters
When doing api recon we may find the undocumented api endpoints and parameters that api supports . and use them to change the behaviour of the application  there are some built in tools in burpsuite like burp intruder then param miner BApp can be used to guess 65k parameter names per request then content discovery 

### Mass assignment vulnerabilities
Mass assignment also known as auto-binding can create hidden parameters. it occours when the software framework automaticly bind request parameters to fields. Mass assignment may therefore result in the application supporting parameters that were never intended to be processed by the developer.

### Identifying hidden parameters
Since mass assignment creates parameters from object fields, you can often identify these hidden parameters by manually examining objects returned by the API.
For example, an api patch request was send in json format
{ "username": "wiener", "email": "wiener@example.com", }
and after calling the A concurrent `GET /api/users/123` request returns the following JSON:
we get { "id": 123, "name": "John Doe", "email": "john@example.com", "isAdmin": "false" }
means that id and isAdmin parameter are bound to the internal object , along side the updated username and email parameters.

### Testing mass assignment vulnerabilities
To test whether u can modify the hidden paramenter from false to true to get admin access 
we can send an PATCH request like 
{ "username": "wiener", "email": "wiener@example.com", "isAdmin": false, }
and also send an PATCH request with the invalid parameter value 
{ "username": "wiener", "email": "wiener@example.com", "isAdmin": "foo", }

if sending the invalid para value makes the application behaves differently or gives an error that can indicate that the hidden parameter can be changed and modified by the user 

the we try to send the PATCH request again with the value true to cheak if we actually get the admin access
{ "username": "wiener", "email": "wiener@example.com", "isAdmin": true, }
if the admin parameter is bind to the user object then we will be able to get the admin access if it doesnt cheak the validation and the sanatization the user may get the admin privilages and able to modify things 

### Preventing vulnerabilities in APIs
To make the API secure as possible we should always 
--> Secure the documentation of the Api so it cant be publically accessiable
--> The Documentations should be up to date so the real testers can have full visibility of the Api attack surface 
--> Apply an allowedliist para HTTP method 
--> Validate the content type expected for each request of response 
--> User generic error message 
--> use protective measures on all versions of api , not just the current version 

### Server-side parameter pollution
Some system use internal api that arent directly accessable from internet . but if the server embeds user input into server side request to internal api without any encoding . then this is called server side parameter pollution and the attacker can use this to override the existing parameters and modify the application behaviours , and access unauth data using injection from the userside. 
This is also called HTTP parameter vulnerability . This term can also be refered as the WAF bypass ( web application firewall ) . this vulnerability is very less found 

### Testing for server-side parameter pollution in the query string
To test the server-side para pollution in a query string (injection) we can use syntax char such as #, &, = in the input and observe how the application responds 
for eg the user sends this request GET /userSearch?name=peter&back=/home
but internally the server sends this request to receave the data of that 
`GET /users/search?name=peter&publicProfile=true`

### Truncating query strings
As we cant direcly use the # in the request so we encode it and send it to the server suppose like this `GET /userSearch?name=peter%23foo&back=/home`
so in the frontend it will cheak for this `GET /users/search?name=peter#foo&publicProfile=true`
Its essential to encode the the # char in the url otherwise if u send directly it will be
passed as fragment identifier and it wont be passes to the internal api.

###  Injecting invalid parameters
We can use an URL-encoded `&` character to attempt to add a second parameter to the server-side request.
suppose  we send `GET /userSearch?name=peter%26foo=xyz&back=/home`
This results in the following server-side request to the internal API:
`GET /users/search?name=peter&foo=xyz&publicProfile=true`

###  Injecting valid parameters
If we able to modify the query string, you can then attempt to add a second valid parameter to the server-side request.
Suppose for email parameter 
we can add into query strings as `GET /userSearch?name=peter%26email=foo&back=/home`
the api will take it as `GET /users/search?name=peter&email=foo&publicProfile=true`

### Overriding existing parameters
To confirm whether the application is vulnerable to server-side parameter pollution, you could try to override the original parameter. Do this by injecting a second parameter with the same name.
`GET /userSearch?name=peter%26name=carlos&back=/home`
the api will process it as 
`GET /users/search?name=peter&name=carlos&publicProfile=true`
The internal API interprets two `name` parameters. The impact of this depends on how the application processes the second parameter. This varies across different web technologies
--> PHP parses the last parameter only. This would result in a user search for `carlos`.
--> ASP.NET combines both parameters. This would result in a user search for `peter,carlos`, which might result in an `Invalid username` error message.
--> Node.js / express parses the first parameter only. This would result in a user search for `peter`, giving an unchanged result.
If you're able to override the original parameter, you may be able to conduct an exploit.like add `name=administrator` to the request. This may enable you to log in as the administrator user.

### Testing for server-side parameter pollution in REST paths
A RESTful api is different from the other api it may place parametere names and values in the url rather than query string suppose /api/user/123
this path will be read as /api >> is the root api endpoint /users >> represents a resource in case users and /123 is the parameter passed in the users as an identifier for the specific user 
Suppose an application that enables you to edit the user profile on the usernames the request can be send as `GET /edit_profile.php?name=peter`  and in the server side it will be processed as  `GET /api/private/users/peter`
An attacker may be able to manipulate server-side URL path parameters to exploit the API.
To test for this vulnerability, add path traversal sequences to modify parameters and observe how the application responds.
You could submit URL-encoded `peter/../admin` as the value of the `name` parameter: `GET /edit_profile.php?name=peter%2f..%2fadmin`
This may result in the following server-side request: `GET /api/private/users/peter/../admin` if the bakend api process and accepts the request the it will be resolved as /api/private/users/admin

### Testing for server-side parameter pollution in structured data formats
An attacker may be able to manipulate parameters to exploit vulnerabilities in the server's processing of other structured data formats, such as a JSON or XML
To test for this, inject unexpected structured data into user inputs and see how the server responds.Consider an application that enables users to edit their profile, then applies their changes with a request to a server-side API. When you edit your name, your browser makes the following request:
POST /myaccount name=peter so in the server side it will be process as 
`PATCH /users/7312/update {"name":"peter"}` as patch is used for minor changes we might able to add the access_level parameter to the request to gain access  POST /myaccount name=peter","access_level":"administrator
if the user input is directly put in the server side json without any sanatization we might be able to gain admin access PATCH /users/7312/update {"name":"peter","access_level":"administrator"}

### Testing for server-side parameter pollution in structured data formats - Continued
Suppose the client side request is in json instead of direct the browser sends api request as POST /myaccount {"name": "peter"} in the server side it will be processed as PATCH /users/7312/update {"name":"peter"} then we can also use the access_level to gain access POST /myaccount {"name": "peter\",\"access_level\":\"administrator"} in the server side it will be processed as
PATCH /users/7312/update {"name":"peter","access_level":"administrator"}


### Testing with automated tools
We can use automated tools to cheak the server side pollution vulnerability 
burp scanner auto detects suspicious input trasfromation when performing and audit. this happen when an application receives user input , transform it in some way then perform further processing on the resutlt 
we can also use BApp (backslash powered scanner ) to identify the server-side injection vulnerabilities , the scanner classifies input as boring , interesting or vulnerable . then u need to invesitage further input manually 

### Preventing server-side parameter pollution
To prevent server-side parameter pollution, use an allowlist to define characters that don't need encoding, and make sure all other user input is encoded before it's included in a server-side request. You should also make sure that all input adheres to the expected format and structure.

