api-client-javascript
=====================

## Getting started

There are html and js files in this repository.
You can open the `index.html` files in your browser directly, but the javascript APIs won't work unless
the HTML is hosted somewhere. (The Bootstrap css won't load from a `file://` prefix either)

To run a simple HTTP server locally, you can use python:
```
cd api-client-javascript
python -m SimpleHTTPServer 8000
```

This will start a local server. Visit `http://localhost:8000/traitviewer`
to see the first javascript example.

To get data from the API, you will also need to use a real Client ID.

* First create a [Genomics enabled project](https://console.developers.google.com/flows/enableapi?apiid=genomics)
  in the Google Developers Console.

* Once you are redirected to the **Credentials** tab, click **Create new Client ID** under
  the OAuth section.

* Set **Application type** to **Web application**, and change
  the **Authorized javascript origins** to `http://localhost:8000`

* Click the **Create Client ID** button

* From the newly created **Client ID for web application**, copy the `Client ID`
  value into the `clientId` variable inside `traitviewer/index.html`.
  The clientId line that used to look like this:

  `$.initGenomics({clientId: 'your-client-id-goes-here'});`

  should now be more like this:

  `$.initGenomics({clientId: '12345.apps.googleusercontent.com'});`

* Save the traitviewer/index.html file, reload the `http://localhost:8000/traitviewer` page, and
  all of the API calls should work.


Note: If you want to run the code on any other domain, make sure you update the
javascript origins on your Client ID to include that new domain.


## BigQuery javascript integration example

Google Genomics data can also be exported to BigQuery, and there are many SQL
snippets in the [bigquery-examples repository](https://github.com/googlegenomics/bigquery-examples)
that can be used to query over the resulting data.

The `bigquery/index.html` file in this repository provides an example of how you can
execute those same SQL snippets from javascript using BigQuery's javascript
client library and the `googlegenomics.jquery.js` helper code.

Just like the instructions above, you need a valid client ID. This time
though, make sure you have a [BigQuery enabled project](https://console.developers.google.com/flows/enableapi?apiid=bigquery). (You can use the same
project as before)

Replace `'your-client-id-goes-here'` on line 79 in `bigquery/index.html`
with your client ID, and run your server as before.

The BigQuery example code will then be at `http://localhost:8000/bigquery`

Note: You must have a project with BigQuery billing turned on to query against.
(the second text box in the demo) Follow the [instructions from the
bigquery-examples repo](https://github.com/googlegenomics/bigquery-examples#getting-started)
if you don't have a project already. This may or may not be the
same project that you set up the client ID for.


## Code layout

* traitviewer/index.html:

  loads [Bootstrap](getbootstrap.com) and [jQuery](http://jquery.com/)

  The file contains some simple html construction based on the `traits` json variable.
  It then uses `googlegenomics.jquery.js` to search variants and lookup
  genotype information for a callset.

* bigquery/index.html

  An example of how to use the [BigQuery APIs](https://developers.google.com/bigquery/docs/reference/v2/) 
  with javascript to execute a SQL query against the available genomics data. See 
  [bigquery-examples](https://github.com/googlegenomics/bigquery-examples) for query and table details.

* googlegenomics.jquery.js:

  this is a work-in-progress jQuery plugin that makes fetching data from the
  [Genomics API](http://developers.google.com/genomics) a bit easier. It wraps
  [Google's javascript client library](https://developers.google.com/api-client-library/javascript/).


## Project status

### Goals

* Provide an example of how to use the javascript client library.
* Demonstrate how the variant APIs can be used to get callset data.

### Current status

Code needs some cleanup, but not much else is planned at this time.
