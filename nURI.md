# URI

Uniform Resource Identifier: Structure
http://thehost.tld:8080/path/to/it?name=value#foo
\__/   \______________/\_________/ \________/ \_/
|           |            |            |      |
scheme     authority       path        query  fragment

## Uniform Resource Identifier
naming
addressing
identifying

## HTTP
Hypertext Transfer Protocol

The Hypertext Transfer Protocol (HTTP) is an application-level protocol for distributed, collaborative, hypermedia information systems. It is a generic, stateless, protocol[…].
RFC 2616

## Hypertext Transfer Protocol
request/response
client/server
stateless
resource-oriented
on top of TCP/IP

## HTTP Request Methods

safe	idempotent	cachable
HEAD	✓	✓	(✓)
GET	✓	✓	(✓)
PUT		✓
DELETE		✓
POST

## Operation	in SQL	in HTTP

Create	INSERT	POST / PUT
Read	SELECT	GET / HEAD
Update	UPDATE	PUT / POST
Delete	DELETE	DELETE
Please note: The comparison may be flawe


HTTP Response Status Codes
(very incomplete list, only some exampless)
1xx	informational	100	Continue
2xx	sucess	200	Ok
3xx	redirection	300	Multiple Choices
301	Moved Permanently
4xx	client error	400	Bad Request
404	Not Found
409	Conflict
5xx	server error	500	Internal Server Error

## Some Advanced HTTP Features
conditional requests
content negotiation
caching
partial requests
persistent connections
request pipelining
chunked encoding

## HTTP: Conditional Requests (1)

GET /foo HTTP/1.1
If-Modified-Since: Wed, 18 Nov 2011 19:21:45 GMT
Host: erb.io

HTTP/1.1 200 OK
Date: Wed, 04 Jan 2012 17:01:59 GMT
Server: myserver/0.0.7
Last-Modified: Wed, 25 Nov 2011 12:13:15 GMT
Etag: "3ab23c-21f-12058638"
Content-Length: 11
Connection: close
Content-Type: text/plain; charset=UTF-8

hello world
Resource has been changed (here: Last-Modified mismatch).


## HTTP: Conditional Requests (2)

GET /foo HTTP/1.1
Host: erb.io
If-None-Match: "103-4585efb972780;49711a471c400"

HTTP/1.1 304 Not Modified
Date: Wed, 04 Jan 2012 17:06:01 GMT
Server: myserver/0.0.7
Etag: "103-4585efb972780;49711a471c400"
Connection: close
Resource has not yet changed (here: ETag match).

## HTTP: Content Negotiation (1)

GET /foo HTTP/1.1
Accept: text/plain, text/html
Accept-Language: de; q=1.0, en; q=0.5
Host: erb.io

HTTP/1.1 200 OK
Date: Wed, 04 Jan 2012 17:01:59 GMT
Server: myserver/0.0.7
Etag: "3ab23c-21f-12058638"
Content-Length: 10
Connection: close
Content-Type: text/plain; charset=UTF-8
Content-Language: de

hallo welt
Server returns german text representation, as requested.

## HTTP: Content Negotiation (2)

GET /foo HTTP/1.1
Accept: application/msexcel
Accept-Language: it
Host: erb.io

HTTP/1.1 406 Not Acceptable
Date: Wed, 04 Jan 2012 18:21:15 GMT
Server: myserver/0.0.7
Content-Length: 22
Connection: close
Content-Type: text/plain; charset=UTF-8
Content-Language: en

Sorry, can't do that!
Content negotiation failed, server can't fulfil the request.

## Hypermedia Representations
HTML
XHTML
HTML5
Atom

## Hypermedia: Links
<a href="/foo#bar">Over there!</a>
<link rel="stylesheet" type="text/css" href="mystyle.css" />
<a rel="next" href="http://example.org/entries/3">next item</a>
<a rel="crush" href="http://social.net/hot-person">Hot!</a>

## Hypermedia: Link Relations

Semantic description of link relations.
- [IANA Link Relations](http://www.iana.org/assignments/link-relations/link-relations.xml)
- [HTML rel values](http://microformats.org/wiki/existing-rel-values)

## Hypermedia: Forms

<form action="http://example.org/users" method="post">
  <input name="name" type="text" value="" />
  <input name="login" type="text" value="" />
  <input type="submit" />
</form>

POST /users HTTP/1.1
Host: example.org
User-Agent: Mozilla/5.0 (Ubuntu; X11; Linux x86_64; rv:9.0.1) Gecko/20100101 Firefox/9.0.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: de-de,de;q=0.8,en-us;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.7
Connection: keep-alive
Content-Type: application/x-www-form-urlencoded
Content-Length: 28

name=Benjamin+Erb&login=b_erb

## REST
Representational State Transfer

## REST
Introducing the Architectural Style

## Architectural Constraints
1. client-server
2. stateless
3. uniform interface
4. cacheable
5. layered system
6. code on demand

Source: http://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm#sec_5_1

## Client-Server
[image]

## Statelessness

(Web) Applications without any state?

Almost impossible…

Here: Stateless communication!

server manages resource states
client manages session states

## Statelessness

[...]each request from client to server must contain all of the information necessary to understand the request, and cannot take advantage of any stored context on the server.
Roy T. Fielding

## Statelessness: Example

What's the URI of the 2nd result page of search query?
Stateful Version

http://foo.bar/query?sid=61AUOh6W1TA&page=next

server creates a session for each search
session contains search term and current page
"next" URI contains session ID and action (next)
the state of the search is hidden in the session state

## Statelessness: Example

What's the URI of the 2nd result page of search query?
Stateless Version

http://foo.bar/query?term=uni+ulm&start=10

URI contains all information of the search state
search term 'uni ulm', skip the first 10 results
client manages search state
server answers request without looking up a session

## Cacheability
improve network efficiency & scalability
label cacheability of each response

## Layered System
hierarchical layers of components
client, servers, intermediaries
reverse proxies, proxy caches, load-balancers, etc.
integration of legacy systems

[image]

## Uniform Interface: Sub-constraints

identification of resources
manipulation via representations
self-descriptive messages
hypermedia as the engine of application state

## Identification of Resources

resource-oriented architecture
resources are the nouns of the application
resources are fine-grained entities

Examples
Examples

http://example.com/user/4711
http://example.com/customer/23/order/1/product/0735611319
http://example.com/search?term=foo
http://example.com/blog/the-post-title/comments#latest

## Manipulation via Representations
changes of server-side resource states
based on changes of (altered) representations

## Manipulation via Representations

[image]

## Self-descriptive Messages

messages contain representation of resources
meta-data/description of representation (header)
usage of (custom) MIME types
enough information to process without additional knowledge

## Hypermedia as the Engine of Application State

state changes based on hypermedia
following hyperlinks
submitting forms
accessing resources

## Hypermedia: Resource Representations

representations should support hypermedia
XHTML, Atom, etc.

XML and JSON are also popular generic formats. Note however, that they don't have a standardized way of expressing links or forms.

## Hypermedia as the Engine of Application State

[image]

## Hypermedia as the Engine of Application State

[image]

## REST Triangle

[image]

## REST
in Practice

## RESTful Web Services
REST + HTTP

## RESTful Web Services
web services adhering to the REST style
HTTP + hypermedia formats
e.g. leightweight APIs for mobile/web clients

##

REST is so trendy, let's rebrand our old HTTP API and call it RESTful from now on!
Hipster CTO

## RESTful Web Services in Practice

REST: over-hyped term, much confusion
HTTP-based API vs. RESTful API
different types of REST "compliance"

### Common mistakes

URIs contain actions instead of resources
links are hard-coded
messages are not self-descriptive
ignoring Hypermedia as the Engine of Application State

## RESTful Web Services: Examples

flickr 'REST' API
CouchDB
Twitter API
Atom Publishing Protocol

Source: nordsc.com/ext/classification_of_http_based_apis.html

## Advanced Topics and Challenges

API versioning
representation versioning
authentication and security in RESTful APIs
design of hypermedia-enabled representations

## Use Case
RESTful ToDo API
