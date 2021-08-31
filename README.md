# learn-rest

## Good API Design

#### What is REST?
> REpresentational State Transfer

#### Why REST?
* Separation of Client and Server
* Requests are Stateless
* Requests are Cachable
* Uniform Interface (URI)

### Different Components of REST API
> Request
 > * URI
 > * Verb
 > * Headers
 > * Request Body

> Response
 > * Status Code
 > * Headers
 > * Response Body


### Verbs
GET | POST | UPDATE | DELETE | PATCH

### Request 
Verb, URI, Header, Content 

### Response 
Status Code, Header,  Content


### Hypermedia
* allows results to be self describing thus enabling programmatic navigation.Common practice is \_links with urls to different navigation points

 
### Associations
* It is about consistency of results returned to show relationship between data

### Paging
* Consider paging for list of data
* Consider query strings for paging control
* Example:
```json
{
 "totalResults": 200,
 "nextPage": "/api/site?page=5",
 "prevPage": "/api/site?page=3"
}
```

## Error Handling
* Consider - Return status code and error info to help users resolve those, however consider security concerns while disclosing information about error
* Example: 404 Not Found - Access/ Auth error, 400 - Bad request, validation error

```json
{
 "errors":{ 
   "Name": [
     "Name field data is required"
   ]
 },
 "title": "Validation Error on input data",
 "status": 400,
 "traceId": "012345ABCDE"
}
```

### Caching (HTTP Caching)
* Point to Note: Postman usually has an option selected in setting for no-cache header, so it makes explicit request to server to ignore any cache related headers. To enable caching we must disable this option. In real world applications, enabling caching can increase efficiency


**HTTP for caching**
* Send version number in request header to compare if the resource version has changed on server side, Response comes as 304 - Not Modified. This is more like versioning the data returned by calling the API to make it more efficient. The header used is called ```If-Match```


**ETags (Entity Tags)**
* Some kind of unique key to identify if match or not 
* Example: The response header sends a series of alpha numeric character, when next request comes it checks for If-Not-Match then put 
* ```If-None-Match``` header with ETag data is used to check if the content is modified, if not then ```304 - Not Modified``` code is returned
* ```If-Match``` header with ETag is used to modify if ETag matches. This ensures that only intended version can be updated


**Functional APIs**
* These are not typical RESTful type, rather one of operational work needed few times needs to be done exceptionally
* These should be well documented as they may leave some side effect
* Standard verbs can be used, can be skipped. ```OPTIONS``` is a good choice for functional API
* Consider making it secured to only allow authorized and intended users access it

**Async APIs**
* Some APIs can't be RESTful always such as need for waiting longer to complete
* Some new solutions for async apis are: Comet, gRPC, SignalR, Firebase, Socket.IO, Etc.



### Best Practices
* Design your API first, as after release any change to end point would impact consumers
* Match verbs for intended purpose to make it more readable and manageable and remain consistent
* Use query string for trivial changes, DO NOT use as data related (e.g. use for sorting, formating etc.)
* DO NOT use verbs or actions as URIs, use nouns instead (e.g. DO NOT use /getCustomers use /customers)
* DO NOT expose server details or underlying implementation language, use camelCase for json element naming
* While designing data collections, do not return the entire collection if huge, consider less results in a batch, and a next page url
* Decide formats during design thoughtfully, DO NOT use query params to determin format to be returned, 
* Common Header for formats are Accept : application/json, text/xml
* For dynamically increasing data consider paging
* For paging consider query params. 
* Use wrappers to imply paging, that contains info such as total results, next page url etc. 

### Versioning APIs
* Various Types of Versioning are:
* * Versioning URI path ```/v2/```
* * Query string versioning ```?version=2```
* * Versioning with custom Headers ```X-Version: 2.0```
* * Versioning with Accept Header ```Accept: application/json; version=2.0```
* * Versioning with Content Type by introducing a custom content-type header
* * * ```Content-Type: application/vnd.appname.camp.v1+json``` ```Accept: application/vnd.appname.camp.v1+json```


### API Security
Transfer security, network security are major concerns other than data. 

**Cross Origin Resource Sharing (CORS)
* This applies to browser based access to APIs, does not matter to mobile apps or other ways of accessing APIs. 
* CORS allows fine grained control on what can be done on APIs exposed to external apps through browser
* Usually supported by most typical infrastructure, so not a lot to be done to build this

**Auth and Authz**
* App Authentication : API should use apps for authentication
* Authenticate as developer
* Authentication as user (OAuth)

**Types of Authentication to APIs**
* Cookies : easy but vulnerable
* Basic Auth: easy, pass info on query string or header, but can easily be leaked. Using SSL can prevent still not the most secured. Also sends credentials in every request
* Token Auth: commonly used, secured, simple. Follows standard form, hence middleware is needed. Expires faster than cookie hence better. 
*  * **JWT** Json Web Token - has User info, Claims, Validation Signature and other information.
* OAuth: allows trusted third party to identify the users, requests do not include user id, password. Returns a token to confirm identity. This de-risks the situation of storing user credentials 


### Common Commands
```linux
# get content from webpage
curl arest.me

# get only header from webpage
curl arest.me -I

# get header and content from webpage
curl arest.me -i

```
