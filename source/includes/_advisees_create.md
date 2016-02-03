## Create an Advisor-Advisee Relationship

```http
POST /api/v1/mutants/2/advisees HTTP/1.1
Content-Type: application/json
Host: mutant-school.herokuapp.com
Connection: close
User-Agent: Paw/2.2.9 (Macintosh; OS X/10.11.2) GCDHTTPRequest
Content-Length: 22

{"advisee":{"id":"4"}}
```

```shell
curl -X "POST" "https://mutant-school.herokuapp.com/api/v1/mutants/2/advisees" \
	-H "Content-Type: application/json" \
	-d "{\"advisee\":{\"id\":\"4\"}}"
```

```ruby
require 'net/http'
require 'net/https'
require 'json'

def send_request
  # My API (2) (POST )

  begin
    uri = URI('https://mutant-school.herokuapp.com/api/v1/mutants/2/advisees')

    # Create client
    http = Net::HTTP.new(uri.host, uri.port)
    http.use_ssl = true
    http.verify_mode = OpenSSL::SSL::VERIFY_PEER

    dict = {
            "advisee" => {
                "id" => "4"
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
// My API (2) (POST https://mutant-school.herokuapp.com/api/v1/mutants/2/advisees)

jQuery.ajax({
    url: "https://mutant-school.herokuapp.com/api/v1/mutants/2/advisees",
    type: "POST",
    headers: {
        "Content-Type": "application/json",
    },
    contentType: "application/json",
    data: JSON.stringify({
        "advisee": {
            "id": "4"
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
  "mutant_name": "Megamarie",
  "power": "Super-human strength",
  "real_name": "Marie",
  "created_at": "2016-02-03T05:27:10.292Z",
  "updated_at": "2016-02-03T05:28:13.837Z",
  "eligibility_begins_at": "2010-01-01T00:00:00.000Z",
  "eligibility_ends_at": "2020-01-01T00:00:00.000Z",
  "may_advise_beginning_at": "2016-01-01T00:00:00.000Z",
  "url": "https://mutant-school.herokuapp.com/api/v1/mutants/4",
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

This endpoint establishes an advisor-advisee relationship between two mutants.

<aside class="warning">Can advisors be assigned before their <em>may_advise_beginning_at</em> date? Seems like they shouldn't be able to. Is that being compared to the enrollment start date, or what? I don't think I get it. <em>&mdash; Boss Person</em></aside>

### HTTP Request

`POST https://mutant-school.herokuapp.com/api/v1/mutants/<ADVISOR_ID>/advisees`

### URL Parameters

Parameter  | Description
---------  | -----------
ADVISOR_ID | The ID of the advisor mutant

### Payload

May be sent as any of the following:

* `application/json` (shown in example code)
* `application/x-www-form-urlencoded`
* `multipart/form-data`

Parameter    | Required | Description
---------    | -------  | -----------
advisee[id]  | yes      | The ID of the mutant whose advisor is specified by ADVISOR_ID

### Errors

Error Code | Meaning
---------- | -------
400        | Bad Request -- Your request is bad, and you should feel bad. You could be missing parameters, or the parameters are malformed.
404        | Not Found -- Either the advisor mutant or the advisee mutant cannot be found.
500        | Internal Server Error. You might have provided an invalid or blank advisee ID.
