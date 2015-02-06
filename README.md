Discovery System RESTful API

The National Archives API
-------------------------

Discovery holds more than 32 million descriptions of records held by The
National Archives and more than 2,500 archives and institutions across
the United Kingdom as well as a much smaller number of archives around
the world. The information in Discovery is made up of record
descriptions provided by or derived from the catalogues of the different
archives. Although some of The National Archives records have been
digitised and can be read online, Discovery can't search the words
within them - only their description and title.

Our API allows developers to query the search engine and database within
the Discovery service application programmatically, and returns results
in XML or Json for further processing. The service is offered as a beta
with some functionality still to be developed. In the meantime we
welcome
[feedback](mailto:discovery@nationalarchives.gsi.gov.uk?subject=Discovery%20API%20feedback)
on the functionality in this release.

If you would like access to our API, please [contact
us](mailto:discovery@nationalarchives.gsi.gov.uk?subject=Request%20access%20to%20Discovery%20API)
and please include the IP address from which you will be sending
requests to our API.

Terms of use
============

**Statement of intent**

Our Discovery API is designed to maximise access to the information held
in our Discovery service catalogue.

You are welcome to use the information and the images for personal use,
educational purposes or commercial use under the [Open Government
Licence](http://www.nationalarchives.gov.uk/doc/open-government-licence/).

**Best practice**

Please tell us about your use of the API by [emailing us a
link](mailto:Discovery@nationalarchives.gsi.gov.uk) to your websites and
describing how you are using the API service. Also, please provide
feedback about your experience of using the API so that we can work to
improve the service.

Do not make an unreasonable number of API calls or use the API in a way
which significantly compromises the experience of other users of the
API. As a guideline, you should make no more than 3000 API calls per day
at a rate of no more frequently than one request per second. The
National Archives may choose to limit the number of API calls more
formally in the future.

[Report any concern](mailto:Discovery@nationalarchives.gsi.gov.uk) you
have over copyright to The National Archives.

**Terms and conditions**

If you make a request to this service you are deemed to have accepted
the terms and conditions listed here.

You may not use The National Archives logo on your website without our
specific written permission.

Our Discovery service is still under development. Please do not cache or
store any content returned by the API.

You will not use The National Archives content or API service for any
illegal or defamatory purpose of any nature. You will not use the API
service to juxtapose our content with any illegal or defamatory material
of any nature.

You understand and agree that The National Archives will not provide any
technical support services in connection with any use of the API. We do
not guarantee availability of the API service.

The National Archives reserves the right to extend or alter these terms
and conditions at any time.

Understanding the Discovery service catalogue
---------------------------------------------

**Note that the following information relates to the content, metadata
and structure of The National Archives catalogue dataset; other
catalogues and datasets within Discovery may be different.**

A little understanding of the structure of the Discovery service
catalogue will help with the API methods below. The National Archives
catalogue dataset is organised hierarchically to reflect the origin and
structure of the records. There are seven levels in the catalogue,
ranging from Department at the top of the tree to pieces and,
occasionally items at the bottom:

1.  **Department** (a government department, agency or body that creates
    the records)

2.  Division (administrative section of a department, when appropriate)

3.  **Series** (the main grouping of records with a common function or
    subject)

4.  Sub-series (smaller groupings of records with a common function or
    subject)

5.  Sub sub-series (smaller groupings of records with a common function
    or subject)

6.  **Piece** (it is not a single piece of paper. A piece can be a box,
    volume or file)

7.  Item (it is a part of a piece. It can be a bundle, a single
    document, or a letter and so on)

Every level of description in the hierarchy is described within a
catalogue entry according to the international standard [ISAD
(G)](http://www.icacds.org.uk/icacds.htm). The dataset follows its rules
for multi-level catalogues (specificity, relevancy, hierarchy position
and non-repetition of information at different levels).

When using the API methods below, you’ll find that some of the normally
‘invisible’ levels (levels which are present but not reflected in the
citable reference, such as ‘Division’) will become relevant and may be
initially confusing when using methods like Children which traverse the
levels of the catalogue.

Every record in Discovery is an Information Asset and is uniquely
referenced by its IAID. Some of the Information Assets have children,
and this parent-child relationship defines the hierarchy.

The API uses two methods:

-   **Search**

> Search method is processed by our Discovery service search engine. It
> offers a basic search where you can enter a single or multiple search
> terms. The default is to search for any of the words. To search for a
> phrase use double quotation marks.

Note that the Discovery service database comprises three primary record
collections:

-   The National Archives catalogue

-   Catalogues from other archives

-   Records compiled from record creator collections

Search will return results and individual information assets from all
three collections.

-   **Information assets**

> The remainder of the methods take an Information Asset IAID and return
> results directly from our Discovery service database.

The information assets method returns metadata for

-   The National Archives catalogue

-   Catalogues from other archives

-   Records compiled from record creator collections

-   Archive contacts

You can return selected metadata for all four source types but at the
moment most of information asset methods only return results from The
National Archives catalogue.

Operations at
<http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/>

This page describes the service operations at this endpoint.

<table>
<thead>
<tr class="header">
<th align="left"><strong>Uri </strong></th>
<th align="left"><strong>Method </strong></th>
<th align="left"><strong>Description </strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">search/page/{pageid}/{query}</td>
<td align="left">GET</td>
<td align="left"><p>Service at</p>
<p><a href="http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/search/" class="uri">http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/search/</a></p>
<p>Standard search</p>
<p>Page/{PageID}/query={QUERY}</p>
<p>Exact match using quotes</p>
<p>Page/{PageID}/query={“QUERY”}</p>
<p>Search for reference</p>
<p>Page/{PageID}/Reference={REFERENCE}</p>
<p>Search for terms within dates</p>
<p>Page/{PageID}/query={QUERY};DateFrom=DD-MM-YYYY;DateTo=DD-MM-YYYY</p>
<p>Search for terms within a specific archive’s catalogue</p>
<p>Page/{PageID}/query={QUERY};repositorycodes={archon code}</p></td>
</tr>
<tr class="even">
<td align="left">informationassets/{id}</td>
<td align="left">GET</td>
<td align="left">Service at <a href="http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/informationassets/%7bID%7d" class="uri">http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/informationassets/{ID}</a></td>
</tr>
<tr class="odd">
<td align="left">informationassets/{ID}/children/Page/{pageid}</td>
<td align="left">GET</td>
<td align="left"><p>Service at <a href="http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/InformationAssets/%7bID%7d/children/page/%7bPageID%7d" class="uri">http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/InformationAssets/{ID}/children/page/{PageID}</a></p>
<p>[The National Archives collection only]</p></td>
</tr>
<tr class="even">
<td align="left">informationassets/{ID}/totalchildren</td>
<td align="left">GET</td>
<td align="left"><p>Service at <a href="http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/InformationAssets/%7bID%7d/totalchildren" class="uri">http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/InformationAssets/{ID}/totalchildren</a></p>
<p>[The National Archives collection only]</p></td>
</tr>
<tr class="odd">
<td align="left">informationassets /{ID}/parent</td>
<td align="left">GET</td>
<td align="left"><p>Service at</p>
<p><a href="http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/InformationAssets/%7bid%7d/parent" class="uri">http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/InformationAssets/{id}/parent</a></p>
<p>[The National Archives collection only]</p></td>
</tr>
</tbody>
</table>

Note that a page comprises 30 results.

Some examples: the results are returned as XML by default

Page 1 of search results for Titanic:

-   <http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/search/page/1/query=titanic>

Page 1 of search results for Nelson held by The National Archives

-   <http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/search/page/1/query=nelson;repositorycodes=66>

You can get the archon code from the archive contact page. Search for
this from <http://discovery.nationalarchives.gov.uk/archives-home>

Page 1 of a list of records containing the National Archives reference
CO 28 [note that to improve the results you can enter the reference in
quotes and maybe add repository code]

<http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/search/page/1/Reference=%22co%2028%22>

Page 1 of a list of results for Cranham held by Gloucestershire Archives
between 1900 and 1920

-   <http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/search/page/1/query=cranham;repositorycodes=40;datefrom=01-01-1900;dateto=31-12-1920>

Search for Gloucestershire Archives reference P103a acc 11059, acc
11117:

-   <http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/search/page/1/Reference=P103a%20acc%2011059,%20acc%2011117>

Information Asset details for C1007252, an example from The National
Archives

-   <http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/InformationAssets/C10072525>

Information Asset details for f313499d-0a90-41c6-9c2b-1b4633b68c27, an
example from another archive catalogue

-   <http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/InformationAssets/f313499d-0a90-41c6-9c2b-1b4633b68c27>

Information Asset details for N13861434, an example of a record creator
record

-   <http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/InformationAssets/N13861434>

Information Asset details for A13532926, contact details for
Gloucestershire Archives

-   <http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/InformationAssets/A13532926>

Parent Information Asset for IAID=C57915

-   <http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/InformationAssets/C57915/Parent>
    [The National Archives collection only]

Querying The National Archives catalogue directly
-------------------------------------------------

**PCOM 3 Example**

Some series in The National Archives catalogue contain structured data,
for example PCOM 3 (Licences for early release from prison) has a
standardised ScopeContent description across the entire series which
could be extracted and parsed into a dataset.

Here’s how you might extract this data:

First we need to identify the IAID of the container series, PCOM 3. The
Search method allows searching for document references, so the following
query will return records matching “PCOM 3”:

-   <http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/search/page/1/Reference=%22pcom%203%22>

Checking the CitableReference values we see that one of the results is
for an information asset which represents the series PCOM 3. We see that
the IAID for this series is C11498.

We can find out how many child information assets PCOM 3 has by
supplying its IAID to the totalchildren method:

-   <http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/InformationAssets/C11498/totalchildren>

Which shows that 770 information assets have PCOM 3 as their parent.

To find out more about those children we use the children method:

-   <http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/InformationAssets/C11498/children/page/1>

This returns the first page (30 records) of child information assets for
PCOM 3. The IAID of the first child IA is C2389021, and its citable
reference is “PCOM 3/1”. The SourceLevelId value shows that this
Information Asset is at level 6 of the catalogue (i.e. a piece). The
descriptions may be more granular still if the piece has been itemised
further. Let’s check if PCOM 3/1 has further details by checking if it
has any children:

-   <http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/InformationAssets/C2389021/totalchildren>

This reveals that PCOM 3/1 has been itemised and has 100 child
Information Assets.

We need to get the IAIDs of those children and then iterate through
them, sending them to the InformationAssets method to return the
detailed descriptions. There are 30 IAIDs per page

-   <http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/InformationAssets/C2389021/children/page/1>

This returns InformationAssetIdentity objects which are a brief summary
of the Information Asset, but include the IAID which can be sent to the
InformationAssets method to return the detailed Information Asset
information. The first child of PCOM 3/1 is PCOM 3/1/1 with IAID
C10127419

-   <http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/InformationAssets/C10127419>

**C 3 example**

C 3 is another series where the information has been entered in a
standardised format which could be parsed into a structured dataset.

Get the IAID for C 3:

-   <http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/search/page/1/Reference=%22c%203%22>

The IAID for C 3 is C3566

Get a list of its Children:

-   <http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/InformationAssets/C3566/children/page/1>

The children of C 3 are at level 6, piece level (though confusingly, the
citable reference of these pieces is in the format c3/x/x, which would
more commonly be an item reference).

For each child we need to:

-   confirm if it has children

-   fetch the detailed Information Asset object

-   if there are Children, call this procedure recursively for them

The method calls we need to make for each child IA are therefore:

-   [http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/InformationAssets/{IAID}/totalchildren](http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/InformationAssets/%7bIAID%7d/totalchildren)

-   [http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/InformationAssets/{IAID}](http://discovery.nationalarchives.gov.uk/DiscoveryWebAPI/InformationAssets/%7bIAID%7d)

If TotalChildren \> 0, recurse
