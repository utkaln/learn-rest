# learn-rest

#### What is REST?
> REpresentational State Transfer

#### Why REST?
* Separation of Client and Server
* Requests are Stateless
* Requests are Cachable
* Uniform Interface (URI)
### Verbs
GET | POST | UPDATE | DELETE | PATCH

### Request 
Verb, URI, Header, Content 

### Response 
Status Code, Header,  Content

### Common Commands
```linux
# get content from webpage
curl arest.me

# get only header from webpage
curl arest.me -I

# get header and content from webpage
curl arest.me -i

```
### What is Hypermedia
> allows results to be self describing thus enabling programmatic navigation.Common practice is \_links with urls to different navigation points
> 
 
### Associations
> It is about consistency of results returned to show relationship between data


### Caching (HTTP Caching)
* Use HTTP for caching
* Send version number in request header to compare if the resource version has changed on server side, Response comes as 304 - Not Modified
* 

## Best Practices
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
