## Create a Mutant

```http
POST /api/v1/mutants HTTP/1.1
Content-Type: application/json
Host: mutant-school.herokuapp.com
Connection: close
User-Agent: Paw/2.2.9 (Macintosh; OS X/10.11.2) GCDHTTPRequest
Content-Length: 185

{"mutant":{"real_name":"Dave","mutant_name":"Superdave","power":"Flight","eligibility_begins_at":"2010-01-01","eligibility_ends_at":"2020-01-01","may_advise_beginning_at":"2016-01-01"}}
```

```shell
curl -X "POST" "https://mutant-school.herokuapp.com/api/v1/mutants" \
	-H "Content-Type: application/json" \
	-d "{\"mutant\":{\"real_name\":\"Dave\",\"mutant_name\":\"Superdave\",\"power\":\"Flight\",\"eligibility_begins_at\":\"2010-01-01\",\"eligibility_ends_at\":\"2020-01-01\",\"may_advise_beginning_at\":\"2016-01-01\"}}"

```

```ruby
require 'net/http'
require 'net/https'
require 'json'

def send_request
  # Mutants#create (POST )

  begin
    uri = URI('https://mutant-school.herokuapp.com/api/v1/mutants')

    # Create client
    http = Net::HTTP.new(uri.host, uri.port)
    http.use_ssl = true
    http.verify_mode = OpenSSL::SSL::VERIFY_PEER

    dict = {
            "mutant" => {
                "eligibility_begins_at" => "2010-01-01",
                "power" => "Flight",
                "may_advise_beginning_at" => "2016-01-01",
                "eligibility_ends_at" => "2020-01-01",
                "real_name" => "Dave",
                "mutant_name" => "Superdave"
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
// Mutants#create (POST https://mutant-school.herokuapp.com/api/v1/mutants)

jQuery.ajax({
    url: "https://mutant-school.herokuapp.com/api/v1/mutants",
    type: "POST",
    headers: {
        "Content-Type": "application/json",
    },
    contentType: "application/json",
    data: JSON.stringify({
        "mutant": {
            "eligibility_begins_at": "2010-01-01",
            "power": "Flight",
            "may_advise_beginning_at": "2016-01-01",
            "eligibility_ends_at": "2020-01-01",
            "real_name": "Dave",
            "mutant_name": "Superdave"
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
```

This endpoint creates a new mutant.

### HTTP Request

`POST https://mutant-school.herokuapp.com/api/v1/mutants`

### Query Parameters

Parameter                       | Required | Description
---------                       | -------  | -----------
mutant[real_name]               | yes      | Legal name
mutant[mutant_name]             | yes      | Preferred name
mutant[power]                   | yes      | Superpower
mutant[eligibility_begins_at]   | no       | Date when eligibility to enroll begins
mutant[eligibility_ends_at]     | no       | Date when mutant is no longer eligible to enroll; must be a date that occurs after `eligibility_begins_at`
mutant[may_advise_beginning_at] | no       | Mutant may be an advisor to students on or after this date.

### Errors

Error Code | Meaning
---------- | -------
400        | Bad Request -- Your request is bad, and you should feel bad.
422        | Unprocessable Entity -- Probably a data validation error. Check response for details. Sample response: <br><code>{"power":["can't be blank"],"eligibility_ends_at":["is before the eligibility start date"]}</code>
500        | Internal Server Error -- It's probably our fault.
