## Get a Specific Mutant

```http
GET /api/v1/mutants/1 HTTP/1.1
Host: mutant-school.herokuapp.com
Connection: close
User-Agent: Paw/2.2.9 (Macintosh; OS X/10.11.2) GCDHTTPRequest


```

```shell
curl -X "GET" "https://mutant-school.herokuapp.com/api/v1/mutants/1"
```

```ruby
require 'net/http'
require 'net/https'

def send_request
  # Mutants#show (GET )

  begin
    uri = URI('https://mutant-school.herokuapp.com/api/v1/mutants/1')

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
// Mutants#show (GET https://mutant-school.herokuapp.com/api/v1/mutants/1)

jQuery.ajax({
    url: "https://mutant-school.herokuapp.com/api/v1/mutants/1",
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

> Expected response: **200 OK**, with JSON structured like this:

```json
{
  "id": 1,
  "mutant_name": "Fusionraptor",
  "power": "Creating small, controlled fusion reactions",
  "real_name": "Clarice Sloan",
  "created_at": "2016-02-02T21:24:07.249Z",
  "updated_at": "2016-02-02T22:23:47.482Z",
  "eligibility_begins_at": "2010-01-01T00:00:00.000Z",
  "eligibility_ends_at": "2020-01-01T00:00:00.000Z",
  "may_advise_beginning_at": "2015-06-01T00:00:00.000Z",
  "url": "https://mutant-school.herokuapp.com/api/v1/mutants/1",
  "advisor": {
    "id": 2,
    "mutant_name": "Superdave",
    "power": "Flight",
    "real_name": "Dave",
    "created_at": "2016-02-02T21:24:45.964Z",
    "updated_at": "2016-02-02T21:24:45.964Z",
    "eligibility_begins_at": "2010-01-01T00:00:00.000Z",
    "eligibility_ends_at": "2020-01-01T00:00:00.000Z",
    "may_advise_beginning_at": "2016-01-01T00:00:00.000Z",
    "url": "https://mutant-school.herokuapp.com/api/v1/mutants/2"
  }
}
```

This endpoint retrieves a specific mutant. The advisor, if any, is nested in the results.

### HTTP Request

`GET https://mutant-school.herokuapp.com/api/v1/mutants/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the mutant to retrieve

### Errors

Error Code | Meaning
---------- | -------
400        | Bad Request -- Your request is bad, and you should feel bad
404        | Not Found -- The specified mutant could not be found
500        | Internal Server Error -- It's probably our fault.
