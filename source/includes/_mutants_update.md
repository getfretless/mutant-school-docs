## Update a Specific Mutant

```http
PUT /api/v1/mutants/3 HTTP/1.1
Content-Type: application/json
Host: mutant-school.herokuapp.com
Connection: close
User-Agent: Paw/2.2.9 (Macintosh; OS X/10.11.2) GCDHTTPRequest
Content-Length: 105

{"mutant":{"power":"Invulnerability","may_advise_beginning_at":"2015-08-01"}}
```

```shell
curl -X "PUT" "https://mutant-school.herokuapp.com/api/v1/mutants/3" \
	-H "Content-Type: application/json" \
	-d "{\"mutant\":{\"power\":\"Invulnerability\",\"may_advise_beginning_at\":\"2015-08-01\"}}"
```

```ruby
require 'net/http'
require 'net/https'
require 'json'

def send_request
  # Mutants#update (PUT )

  begin
    uri = URI('https://mutant-school.herokuapp.com/api/v1/mutants/3')

    # Create client
    http = Net::HTTP.new(uri.host, uri.port)
    http.use_ssl = true
    http.verify_mode = OpenSSL::SSL::VERIFY_PEER

    dict = {
            "mutant" => {
                "power" => "Invulnerability",
                "may_advise_beginning_at" => "2015-08-01"
            }
        }
    body = JSON.dump(dict)

    # Create Request
    req =  Net::HTTP::Put.new(uri)
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
// Mutants#update (PUT https://mutant-school.herokuapp.com/api/v1/mutants/3)

jQuery.ajax({
    url: "https://mutant-school.herokuapp.com/api/v1/mutants/3",
    type: "PUT",
    headers: {
        "Content-Type": "application/json",
    },
    contentType: "application/json",
    data: JSON.stringify({
        "mutant": {
            "power": "Invulnerability",
            "may_advise_beginning_at": "2015-08-01"
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

> Expected response: **200 OK**, with JSON structured like this:

```json
{
  "id": 3,
  "mutant_name": "Superdave",
  "power": "Invulnerability",
  "real_name": "Dave",
  "created_at": "2016-02-03T03:37:24.709Z",
  "updated_at": "2016-02-03T03:44:00.123Z",
  "eligibility_begins_at": "2010-01-01T00:00:00.000Z",
  "eligibility_ends_at": "2020-01-01T00:00:00.000Z",
  "may_advise_beginning_at": "2015-08-01T00:00:00.000Z",
  "url": "https://mutant-school.herokuapp.com/api/v1/mutants/3"
}
```

This updates a specific mutant.

### HTTP Request

`PUT https://mutant-school.herokuapp.com/api/v1/mutants/<ID>`

`PATCH https://mutant-school.herokuapp.com/api/v1/mutants/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the mutant to update

### Payload

May be sent as any of the following:

* `application/json` (shown in example code)
* `application/x-www-form-urlencoded`
* `multipart/form-data`

Parameter                       | Required | Description
---------                       | -------  | -----------
mutant[real_name]               | no       | Legal name
mutant[mutant_name]             | no       | Preferred name
mutant[power]                   | no       | Superpower
mutant[eligibility_begins_at]   | no       | Date when eligibility to enroll begins
mutant[eligibility_ends_at]     | no       | Date when mutant is no longer eligible to enroll; must be a date that occurs after `eligibility_begins_at`
mutant[may_advise_beginning_at] | no       | Mutant may be an advisor to students on or after this date.

### Errors

Error Code | Meaning
---------- | -------
400        | Bad Request -- Your request is bad, and you should feel bad. You could be missing parameters, or the parameters are malformed.
404        | Not Found -- There's no mutant with that ID.
422        | Unprocessable Entity -- Probably a data validation error. Check response for details. Sample response: <br><code>{"power":["can't be blank"],"eligibility_ends_at":["is before the eligibility start date"]}</code>
500        | Internal Server Error -- It's probably our fault.
