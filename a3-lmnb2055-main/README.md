# The Web

To complete this assignment, open it in a codespace, and use Visual
Studio Code to edit this file.

For the first question, edit the example answer and replace it with
your own.

For the subsequent questions, replace `ANSWER GOES HERE` with your
answers.

When you are finished, commit and sync your changes.

This file is written in [Markdown][md]. Read about [editing Markdown
in Visual Studio
Code](https://code.visualstudio.com/docs/languages/markdown).

[md]: <https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax>

## 1. Resources that exist and that don’t

Choose a Web site that you use frequently.

Identify a few kinds of resource that the site identifies with URIs,
making it possible to link to them.

Then, identify something that conceivably *could* be a kind of
resource that the site makes addressable, but does not.

Sidney's answer:

---
I often use [Splunk](https://www.splunk.com/). Splunk identifies several different kinds of resources with URIs, including:  

* **Dashboards** such as [Search & Reporting](https://help.splunk.com/en/splunk-enterprise/create-dashboards-and-reports/reporting-manual/10.0/report-management/create-and-edit-reports) or [IT Service Intelligence Overview](https://splunkbase.splunk.com/app/1841/)  
* **Apps** such as [Splunk Enterprise Security](https://splunkbase.splunk.com/app/263/) or [Splunk Machine Learning Toolkit](https://splunkbase.splunk.com/app/2890/)  
* **Reports** such as saved search results or scheduled alerts  
* **Datasets** such as indexes or data models  

However, even though Splunk organizes information about **individual log events** inside an index, it does *not* identify each event with a stable URI. There is no way to directly link to one specific event, view its raw data, or share it as a unique resource outside the Splunk interface.  

A hypothetical example might look like:  
[<https://splunk.unc.edu/sils/syslog/12345> ](<https://splunk.unc.edu/sils/syslog/12345> )  

A representation of this resource could consist of the raw log message, its timestamp, the host and source, as well as the extracted fields associated with that event.  

---

* Includes a link to the main website <https://splunk.com/>  
* Lists several types of resources that can be linked, and provides **example links** for each (e.g., dashboards, apps, datasets)  
* Points out something that is *not* currently an addressable resource, but could be (such as individual log events)  
* Invents a sample URL showing what such a resource might look like, e.g. <https://splunk.unc.edu/sils/syslog/12345>  
* Suggests what information a representation of that resource could include (for example, “the raw log message, timestamp, host, source, and extracted fields”)  


## 2. HTTP requests and responses
  
[Open a new Incognito
window](https://support.google.com/chrome/answer/95464) in the Chrome
Web browser. Then [open the Chrome
DevTools](https://developer.chrome.com/docs/devtools/open/#chrome). Open
the Network Panel by clicking on the Network tab at the top of the
DevTools window. Then type `unc.edu` into the Chrome address bar, and
press return.

Now answer the following questions:

* How many HTTP requests were made?

4 requests

* Were all the requests successful? How do you know?

Yes. I saw Code200->3, Code304->1, so they are all successful.

* How many different types of representations were returned? List some
  of the different types you saw.
  
5 types of representations were returned: sytlesheet, avif, gif, xhr, fetch.

## 3. The same resource

How can you determine whether two different URLs refer to the same
resource?

We can determine whether two different URLs point to the same resource from these perspectives:

1. HTTP Status Codes and Redirects
If one URL directly issues a 301 or 302 redirect to the other URL, you can be almost certain they represent the same resource.
For example:
http://unc.edu → 301 → https://www.unc.edu

2. Content Comparison
Request both URLs and check the Content-Location header and the body.
If the returned content is identical (the same HTML or JSON), you can judge that they are the same resource.

3. Unique Identifiers
Some websites return headers like ETag or Last-Modified. If two URLs have the same ETag, it indicates they are two different addresses for the same resource.

## Exploring a Wikidata resource

Wikidata is a free and open knowledge base that can be read and edited
by both humans and machines. Wikidata acts as central storage for the
structured data of its Wikimedia sister projects, including
Wikipedia. For this question you will use `curl` to explore a Wikidata
resource, its related resources, and their representations. Mainly,
you’ll be using `curl` to request URLs and to look at the headers of
HTTP responses.

### Quick `curl` cheatsheet

You can use `curl` in the [Visual Studio Code
terminal](https://code.visualstudio.com/docs/terminal/getting-started).

Make an HTTP GET request to a URL, and show only the **body** of the
response:

```sh
curl https://programming-for-info-pros-is.fun
```

Make an HTTP GET request to URL, and show only the **headers** of the
response:

```sh
curl --head https://programming-for-info-pros-is.fun
```

or

```sh
curl -I https://programming-for-info-pros-is.fun
```

Make an HTTP GET request to URL, and **add a header to the request**
(for example, `Accept: text/plain`, requesting a plain text
representation):

```sh
curl --header "Accept: text/plain" https://programming-for-info-pros-is.fun
```

or

```sh
curl -H "Accept: text/plain" https://programming-for-info-pros-is.fun
```

Make an HTTP GET request to URL, adding a header to the request, and
show only the headers of the response:

```sh
curl -I -H "Accept: text/plain" https://programming-for-info-pros-is.fun
```

### 4. `curl`ing Wikidata

Use `curl` to request a representation of the following resource:

<https://www.wikidata.org/entity/Q192334>

Examine the headers and body the the response to your request.

* Does this resource have any representations? Why or why not?

No. Requesting https://www.wikidata.org/entity/Q192334 returns 303 See Other with a Location header, which means the /entity/ URI is an identifier and Wikidata instructs clients to retrieve a representation from another URI.

The `location` header of the response should refer to another resource
related to <https://www.wikidata.org/entity/Q192334>.

* What is the URL of this second resource?

https://www.wikidata.org/wiki/Special:EntityData/Q192334

* What is the relationship between these two resources? (Hint: look at
  the [HTTP status
  code](https://www.rfc-editor.org/rfc/rfc9110.html#name-status-codes)
  of the response.)

  /entity/Q192334 is the canonical identifier for the Wikidata entity. The 303 See Other redirect points to /wiki/Special:EntityData/Q192334, which is where concrete representations of that entity are served.

Investigate this second resource using `curl`.

* Does it have a representation?

Yes. If you follow content negotiation, it serves machine-readable data.

Examine the headers returned by a request for this second
resource. Again, the `location` header should refer to another (third)
resource. Investigate this third resource using `curl`.

* Does it have a representation? If so, what is the [media
  type](https://www.rfc-editor.org/rfc/rfc9110.html#section-8.3) of
  that representation?

Yes, it has a representation. The media type of that representation is application/json.

Wikidata supports *content negotiation* to obtain data in different
formats: JSON, RDF+XML, Turtle, and N-Triples. To do content
negotiation (i.e., to inform the server what kind of representation
you want), you need to add an HTTP header to your request. For
example, if you wanted to request a representation in plain text
format, you could add the header:

```text
Accept: text/plain
```

Of course, just because you request a certain type of representation
doesn’t mean that that type of representation is actually available.

Now, make a new request for the **second** resource you discovered
above. This time, specify the media type of the representation you
want.

Remember that Wikidata only publishes data in the formats listed above
(JSON, RDF+XML, Turtle, and N-Triples), so you'll need to choose one
of these. You can look up the media type for each of these formats on
this [IANA web
page](https://www.iana.org/assignments/media-types/media-types.xhtml). The
format names (lowercased) are in the first column, and the media types
are in the second column.

* How does specifying a media type change the response you get when
  requesting the second resource? Be specific.

At first, the response for each request was a 303 See Other with Content-Type: text/html, because the server was issuing a redirect. The Location header pointed to the format-specific URL. When I followed the redirect, each format returned a 200 OK with its correct media type (application/json, application/rdf+xml, text/turtle, or application/n-triples).