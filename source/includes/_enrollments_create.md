## Create an Enrollment

```http
POST /api/v1/mutants/1/enrollments HTTP/1.1
Content-Type: application/json
Host: mutant-school.herokuapp.com
Connection: close
User-Agent: Paw/2.2.9 (Macintosh; OS X/10.11.2) GCDHTTPRequest
Content-Length: 28

{"enrollment":{"term_id":4}}
```

```shell
curl -X "POST" "https://mutant-school.herokuapp.com/api/v1/mutants/1/enrollments" \
	-H "Content-Type: application/json" \
	-d "{\"enrollment\":{\"term_id\":4}}"
```

```ruby
require 'net/http'
require 'net/https'
require 'json'

def send_request
  # Enrollments#create (POST )

  begin
    uri = URI('https://mutant-school.herokuapp.com/api/v1/mutants/1/enrollments')

    # Create client
    http = Net::HTTP.new(uri.host, uri.port)
    http.use_ssl = true
    http.verify_mode = OpenSSL::SSL::VERIFY_PEER

    dict = {
            "enrollment" => {
                "term_id" => 4
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
// Enrollments#create (POST https://mutant-school.herokuapp.com/api/v1/mutants/1/enrollments)

jQuery.ajax({
    url: "https://mutant-school.herokuapp.com/api/v1/mutants/1/enrollments",
    type: "POST",
    headers: {
        "Content-Type": "application/json",
    },
    contentType: "application/json",
    data: JSON.stringify({
        "enrollment": {
            "term_id": 4
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
  "id": 6,
  "student": {
    "id": 1,
    "mutant_name": "Fusionraptor",
    "power": "Creating small, controlled fusion reactions",
    "real_name": "Clarice Sloan",
    "eligibility_begins_at": "2010-01-01T00:00:00.000Z",
    "eligibility_ends_at": "2020-01-01T00:00:00.000Z",
    "may_advise_beginning_at": "2015-06-01T00:00:00.000Z"
  },
  "term": {
    "id": 4,
    "begins_at": "2014-08-10T00:00:00.000Z",
    "ends_at": "2014-12-25T00:00:00.000Z"
  },
  "created_at": "2016-02-03T05:01:02.758Z",
  "updated_at": "2016-02-03T05:01:02.758Z",
  "url": "https://mutant-school.herokuapp.com/api/v1/mutants/1/enrollments/6"
}
```

This endpoint enrolls a mutant in a term.

<aside class="warning">Is this goofy system letting students enroll in terms that start before they're eligible or after they've become ineligible? We should test for that. <em>&mdash; Boss Person</em></aside>

### HTTP Request

`POST https://mutant-school.herokuapp.com/api/v1/mutants/<MUTANT_ID>/enrollments`

### URL Parameters

Parameter | Description
--------- | -----------
MUTANT_ID | The ID of the mutant to be enrolled.

### Payload

May be sent as any of the following:

* `application/json` (shown in example code)
* `application/x-www-form-urlencoded`
* `multipart/form-data`

Parameter            | Required | Description
---------            | -------  | -----------
enrollment[term_id]  | yes      | The ID of the term in which to enroll the mutant.

### Errors

Error Code | Meaning
---------- | -------
400        | Bad Request -- Your request is bad, and you should feel bad. You could be missing the term ID parameter, or the term ID could be invalid.
500        | Internal Server Error. You might have provided an invalid or blank term ID.
