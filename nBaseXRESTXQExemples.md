---
author: emchateau
tags: basex, webapp
---

Exemples de webApp BaseX
==========

[XQuery Web App Skeleton](https://github.com/micheee/xquery-webapp-skeleton)

https://mailman.uni-konstanz.de/pipermail/basex-talk/2017-July/012142.html

https://github.com/BaseXdb/basex/issues/1220

https://mailman.uni-konstanz.de/pipermail/basex-talk/2017-July/012142.html

My/our workaround is to branch in a single XQuery function using sth. like:

```xquery
if (some $a in tokenize(request:header("ACCEPT"), ',') satisfies $a = 
('text/xml', 'application/xml')) then $xml else $xhtml
```



<https://www.mail-archive.com/basex-talk@mailman.uni-konstanz.de/msg10527.html>

To process https://duckduckgo.com?q=BaseX

```xquery
declare
  %rest:path("/list/{$category}")
  %rest:query-param("page:category", "{$page-category}")
  %output:method("html")
function page:list(
  $page:category as xs:string,
  $page-category as xs:string?
) {
  (: etc :)
};
```



https://github.com/BaseXdb/basex/issues/1220

Hi Steve,

A rather late reply to [1] (but maybe better than fully ignore it): We

have fully revised our quality factor handling. The best RESTXQ

function candidates will now be chosen in multiple steps, and your old

use case (with wildcard content types) should now work as expected. If

you still want to give a try, your feedback is welcome [2].

Best,

Christian

[1] 

https://github.com/BaseXdb/basex/issues/1220

[2] 

http://files.basex.org/releases/latest/

On Tue, Nov 22, 2016 at 7:19 PM, Steve Baskauf

<

steve.baskauf@vanderbilt.edu

\> wrote:

> I'm also wondering about the issue
> <https://github.com/BaseXdb/basex/issues/1220> which prevents using BaseXHttp
> for content negotiation.  I realize that you have to prioritize what gets
> fixed in the releases.  However, I probably should make a decision about
> whether to plan on using BaseXHttp to provide Linked Data content
> negotiation for our project and if that bug isn't likely to be fixed any
> time soon, we probably should start looking for a different solution.
>
> Steve

Hi Omar, hi Emmanuel,

BaseX 9 will provide support for server-side quality factors [1,2]:
With these extensions, it will eventually be possible to handle cases
in which a client provides no content types, and in which multiple
RESTXQ conflicting functions exist for that request.

Hope this helps,
Christian

[1] <https://github.com/BaseXdb/basex/issues/1220>
[2] <http://docs.basex.org/wiki/RESTXQ#Content_Negotiation>

Voir nouveautés 2018

## update:output

https://stackoverflow.com/questions/36960628/how-to-return-results-together-with-update-operations-in-basex