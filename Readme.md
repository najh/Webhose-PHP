
<br /><img src="https://raw.githubusercontent.com/najh/Webhose-PHP/master/logo.png" />
============================
A simple way to access the [Webhose.io](https://webhose.io) API from your PHP code:

```php
// API Key from: https://webhose.io/dashboard
Webhose::config("API_KEY");

//Perform a "filterWebData" query using "United States" as our keywords.
$params = array("q"=>"United States", "size"=>"3");
$result = Webhose::query("filterWebData", $params);

//Fetch the next results using the same terms.
$result = Webhose::get_next();
```
API Key
-------

To make use of the webhose.io API, you'll need an API key.

To get one, sign up at:
https://webhose.io/auth/signup

And your key will be available here:
https://webhose.io/dashboard


Usage
-----------

To get started, you'll need to import the class and configure it with your API key:

```php
require_once('webhose.php');

// API Key from: https://webhose.io/dashboard
Webhose::config("API_KEY");
```

<br />

**API Endpoints**

The first parameter the query() function accepts is the API endpoint string. Available endpoints:
* filterWebData - access to the news/blogs/forums/reviews API
* productSearch - access to data about eCommerce products/services
* darkWebAPI - access to the dark web (coming soon)

Now you can make a request and inspect the results:

```php
//Helper method to print result:
function print_filterwebdata_titles($api_response)
{
    if($api_response == null)
    {
        echo "<p>Response is null, no action taken.</p>";
        return;
    }
    if(isset($api_response->posts))
        foreach($api_response->posts as $post)
        {
            echo "<p>" . $post->title . "</p>";
        }
}

//Perform a "filterWebData" query using "United States" as our keywords.
$params = array("q"=>"United States", "size"=>"3");
$result = Webhose::query("filterWebData", $params);
print_filterwebdata_titles($result);
```

<br />

Depending on the endpoint used, the resulting JSON array could provide "posts", "products", ...
You can view the JSON in the browser to get a clearer picture of the return data.
In order to view the data in the browser, we can enable a debug flag to expose the URL fed to cURL:

```php
//If true, echoes the parameterised Webhose API URL before executing request.
Webhose::enable_debug(true);
```


Full documentation
------------------

* ``Webhose::config(api_key)``

  * api_key - your API key

* ``Webhose::query(end_point_str, params)``

  * end_point_str
    * filterWebData - access to the news/blogs/forums/reviews API
    * productSearch - access to data about eCommerce products/services
    * darkWebAPI - access to the dark web (coming soon)
  * params: A key value dictionary. [Read about the available parameters](https://webhose.io/documentation).

* ``Webhose::get_next()`` - Fetches the next page of results using the same parameters.

* ``Webhose::enable_debug(debug_enabled)``

  * debug_enabled - boolean, If true, echoes the parameterised Webhose API URL before executing requests.