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

### Error Handling
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

**ETags (Entity Tags)
* Some kind of unique key to identify if match or not 

## Best Practices
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
* 
* 

### Common Commands
```linux
# get content from webpage
curl arest.me

# get only header from webpage
curl arest.me -I

# get header and content from webpage
curl arest.me -i

```
