## Get a Specific Term

```http
GET /api/v1/terms/3 HTTP/1.1
Host: mutant-school.herokuapp.com
Connection: close
User-Agent: Paw/2.2.9 (Macintosh; OS X/10.11.2) GCDHTTPRequest

```

```shell
curl -X "GET" "https://mutant-school.herokuapp.com/api/v1/terms/3"
```

```ruby
require 'net/http'
require 'net/https'

def send_request
  # Terms#show (GET )

  begin
    uri = URI('https://mutant-school.herokuapp.com/api/v1/terms/3')

    # Create client
    http = Net::HTTP.new(uri.host, uri.port)
    http.use_ssl = true
    http.verify_mode = OpenSSL::SSL::VERIFY_PEER


    # Create Request
    req =  Net::HTTP::Get.new(uri)

    # Fetch Request
    res = http.request(req)
    puts "Response HTTP Status Code: #{res.code}"
    puts "Response HTTP Response Body: #{res.body}"
  rescue StandardError => e
    puts "HTTP Request failed (#{e.message})"
  end
end
```

```javascript
// Terms#show (GET https://mutant-school.herokuapp.com/api/v1/terms/3)

jQuery.ajax({
    url: "https://mutant-school.herokuapp.com/api/v1/terms/3",
    type: "GET",
})
.done(function(data, textStatus, jqXHR) {
    console.log("HTTP Request Succeeded: " + jqXHR.status);
    console.log(data);
})
.fail(function(jqXHR, textStatus, errorThrown) {
    console.log("HTTP Request Failed");
})
.always(function() {
    /* ... */
});
```

> The above command returns JSON structured like this:

```json
{
  "id": 3,
  "begins_at": "2016-08-10T00:00:00.000Z",
  "ends_at": "2016-12-25T00:00:00.000Z",
  "created_at": "2016-02-02T21:26:26.496Z",
  "updated_at": "2016-02-02T21:26:26.496Z"
}```

This endpoint retrieves a specific term.

### HTTP Request

`GET https://mutant-school.herokuapp.com/api/v1/terms/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the term to retrieve

### Errors

Error Code | Meaning
---------- | -------
400        | Bad Request -- Your request is bad, and you should feel bad
404        | Not Found -- The specified term could not be found
500        | Internal Server Error -- It's probably our fault.
