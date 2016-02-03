## Create an Enrollment

```http
POST /api/v1/terms/2/enrollments HTTP/1.1
Content-Type: application/json
Host: mutant-school.herokuapp.com
Connection: close
User-Agent: Paw/2.2.9 (Macintosh; OS X/10.11.2) GCDHTTPRequest
Content-Length: 30

{"enrollment":{"mutant_id":1}}
```

```shell
curl -X "POST" "https://mutant-school.herokuapp.com/api/v1/terms/2/enrollments" \
	-H "Content-Type: application/json" \
	-d "{\"enrollment\":{\"mutant_id\":1}}"
```

```ruby
require 'net/http'
require 'net/https'
require 'json'

def send_request
  # Enrollments#create by Term (POST )

  begin
    uri = URI('https://mutant-school.herokuapp.com/api/v1/terms/2/enrollments')

    # Create client
    http = Net::HTTP.new(uri.host, uri.port)
    http.use_ssl = true
    http.verify_mode = OpenSSL::SSL::VERIFY_PEER

    dict = {
            "enrollment" => {
                "mutant_id" => 1
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
// Enrollments#create by Term (POST https://mutant-school.herokuapp.com/api/v1/terms/2/enrollments)

jQuery.ajax({
    url: "https://mutant-school.herokuapp.com/api/v1/terms/2/enrollments",
    type: "POST",
    headers: {
        "Content-Type": "application/json",
    },
    contentType: "application/json",
    data: JSON.stringify({
        "enrollment": {
            "mutant_id": 1
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
  "id": 12,
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
    "id": 2,
    "begins_at": "2016-01-10T00:00:00.000Z",
    "ends_at": "2016-05-25T00:00:00.000Z"
  },
  "created_at": "2016-02-03T06:39:48.319Z",
  "updated_at": "2016-02-03T06:39:48.319Z",
  "url": "https://mutant-school.herokuapp.com/api/v1/mutants/1/enrollments/12"
}
```

This endpoint enrolls a mutant in a term.

<aside class="warning">Is this goofy system letting students enroll in terms that start before they're eligible or after they've become ineligible? We should test for that. Wait, I already said that earlier, didn't I? <em>&mdash; Boss Person</em></aside>

### HTTP Request

`POST https://mutant-school.herokuapp.com/api/v1/terms/<TERM_ID>/enrollments`

### URL Parameters

Parameter | Description
--------- | -----------
TERM_ID   | The ID of the term in which to enroll the mutant.

### Payload

May be sent as any of the following:

* `application/json` (shown in example code)
* `application/x-www-form-urlencoded`
* `multipart/form-data`

Parameter            | Required | Description
---------            | -------  | -----------
enrollment[mutant_id]  | yes      | The ID of the mutant to be enrolled.

### Errors

Error Code | Meaning
---------- | -------
400        | Bad Request -- Your request is bad, and you should feel bad. You could be missing the mutant ID parameter.
500        | Internal Server Error. You might have provided an invalid or blank mutant ID.
