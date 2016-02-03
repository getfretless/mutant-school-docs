# Advisees

<aside class="notice">Some mutants are advisors. To create the relationship between advisor and student (both of whom are mutants), create an <em>advisee</em> under the advisor.</aside>

## Get All Advisee Mutants for a Specific Advisor Mutant

```http
GET /api/v1/mutants/2/advisees HTTP/1.1
Host: mutant-school.herokuapp.com
Connection: close
User-Agent: Paw/2.2.9 (Macintosh; OS X/10.11.2) GCDHTTPRequest


```

```shell
curl -X "GET" "https://mutant-school.herokuapp.com/api/v1/mutants/2/advisees"
```

```ruby
require 'net/http'
require 'net/https'

def send_request
  # My API (GET )

  begin
    uri = URI('https://mutant-school.herokuapp.com/api/v1/mutants/2/advisees')

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
// My API (GET https://mutant-school.herokuapp.com/api/v1/mutants/2/advisees)

jQuery.ajax({
    url: "https://mutant-school.herokuapp.com/api/v1/mutants/2/advisees",
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
[
  {
    "id": 1,
    "mutant_name": "Fusionraptor",
    "power": "Creating small, controlled fusion reactions",
    "real_name": "Clarice Sloan",
    "eligibility_begins_at": "2010-01-01T00:00:00.000Z",
    "eligibility_ends_at": "2020-01-01T00:00:00.000Z",
    "may_advise_beginning_at": "2015-06-01T00:00:00.000Z",
    "url": "https://mutant-school.herokuapp.com/api/v1/mutants/1"
  }
]
```

This endpoint retrieves all _advisee mutants_ for the specified _advisor mutant_.

### HTTP Request

`GET https://mutant-school.herokuapp.com/api/v1/mutants/<ADVISOR_ID>/advisees`

### URL Parameters

Parameter  | Description
---------  | -----------
ADVISOR_ID | The ID of the advisor mutant
