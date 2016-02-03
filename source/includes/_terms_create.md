## Create a Term

```http
POST /api/v1/terms HTTP/1.1
Content-Type: application/json
Host: mutant-school.herokuapp.com
Connection: close
User-Agent: Paw/2.2.9 (Macintosh; OS X/10.11.2) GCDHTTPRequest
Content-Length: 58

{"term":{"begins_at":"2014-08-10","ends_at":"2014-12-25"}}
```

```shell
curl -X "POST" "https://mutant-school.herokuapp.com/api/v1/terms" \
	-H "Content-Type: application/json" \
	-d "{\"term\":{\"begins_at\":\"2014-08-10\",\"ends_at\":\"2014-12-25\"}}"
```

```ruby
require 'net/http'
require 'net/https'
require 'json'

def send_request
  # Terms#create (POST )

  begin
    uri = URI('https://mutant-school.herokuapp.com/api/v1/terms')

    # Create client
    http = Net::HTTP.new(uri.host, uri.port)
    http.use_ssl = true
    http.verify_mode = OpenSSL::SSL::VERIFY_PEER

    dict = {
            "term" => {
                "begins_at" => "2014-08-10",
                "ends_at" => "2014-12-25"
            }
        }
    body = JSON.dump(dict)

    # Create Request
    req =  Net::HTTP::Post.new(uri)
    # Add headers
    req.add_field "Content-Type", "application/json"
    # Set header and body
    req.add_field "Content-Type", "application/json"
    req.body = body

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
// Terms#create (POST https://mutant-school.herokuapp.com/api/v1/terms)

jQuery.ajax({
    url: "https://mutant-school.herokuapp.com/api/v1/terms",
    type: "POST",
    headers: {
        "Content-Type": "application/json",
    },
    contentType: "application/json",
    data: JSON.stringify({
        "term": {
            "begins_at": "2014-08-10",
            "ends_at": "2014-12-25"
        }
    })
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

> Expected response: **201 Created**, with JSON structured like this:

```json
{
  "id": 4,
  "begins_at": "2014-08-10T00:00:00.000Z",
  "ends_at": "2014-12-25T00:00:00.000Z",
  "created_at": "2016-02-03T04:26:10.979Z",
  "updated_at": "2016-02-03T04:26:10.979Z"
}
```

This endpoint creates a new term.

### HTTP Request

`POST https://mutant-school.herokuapp.com/api/v1/terms`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the term to retrieve

### Query Parameters

Parameter        | Required | Description
---------        | -------  | -----------
term[begins_at]  | yes      | Date when the term begins
term[ends_at]    | yes      | Date when the term ends

### Errors

Error Code | Meaning
---------- | -------
400        | Bad Request -- Your request is bad, and you should feel bad.
422        | Unprocessable Entity -- Probably a data validation error. Check response for details. Sample response: <br><code>{"ends_at":["can't be blank"]}</code>
500        | Internal Server Error -- It's probably our fault.
