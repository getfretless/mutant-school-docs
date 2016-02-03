## Get a Specific Enrollment for a Specific Mutant

```http
GET /api/v1/mutants/1/enrollments/1 HTTP/1.1
Host: mutant-school.herokuapp.com
Connection: close
User-Agent: Paw/2.2.9 (Macintosh; OS X/10.11.2) GCDHTTPRequest


```

```shell
curl -X "GET" "https://mutant-school.herokuapp.com/api/v1/mutants/1/enrollments/1"
```

```ruby
require 'net/http'
require 'net/https'

def send_request
  # Enrollments#show (GET )

  begin
    uri = URI('https://mutant-school.herokuapp.com/api/v1/mutants/1/enrollments/1')

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
// Enrollments#show (GET https://mutant-school.herokuapp.com/api/v1/mutants/1/enrollments/1)

jQuery.ajax({
    url: "https://mutant-school.herokuapp.com/api/v1/mutants/1/enrollments/1",
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
  "id": 1,
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
  "created_at": "2016-02-02T21:27:31.461Z",
  "updated_at": "2016-02-02T21:27:31.461Z",
  "url": "https://mutant-school.herokuapp.com/api/v1/mutants/1/enrollments/1"
}
```

This endpoint retrieves a specific enrollment for a specific mutant.

### HTTP Request

`GET https://mutant-school.herokuapp.com/api/v1/mutants/<MUTANT_ID>/enrollments/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
MUTANT_ID | The ID of the enrolled mutant
ID        | The ID of the enrollment to retrieve

### Errors

Error Code | Meaning
---------- | -------
404        | Not Found -- Either the mutant cannot be found, the enrollment cannot be found, or the enrollment is not associated with the mutant.
500        | Internal Server Error -- It's probably our fault.
