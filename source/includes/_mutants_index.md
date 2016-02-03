# Mutants

<aside class="notice">Mutants are people with genetic anomalies that grant them, for lack of a better word, superpowers. In <em>Mutant School</em>, mutants can be enrolled students, advisors, both, or neither.</aside>

## Get All Mutants

```http
GET /api/v1/mutants HTTP/1.1
Host: mutant-school.herokuapp.com
Connection: close
User-Agent: Paw/2.2.9 (Macintosh; OS X/10.11.2) GCDHTTPRequest


```

```ruby
require 'net/http'
require 'net/https'

def send_request
  # Mutants#index (GET )

  begin
    uri = URI('https://mutant-school.herokuapp.com/api/v1/mutants')

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
// Mutants#index (GET https://mutant-school.herokuapp.com/api/v1/mutants)

jQuery.ajax({
    url: "https://mutant-school.herokuapp.com/api/v1/mutants",
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

```shell
curl -X "GET" "https://mutant-school.herokuapp.com/api/v1/mutants"
```

> Expected response: **200 OK**, with JSON structured like this:

```json
[
  {
    "id": 2,
    "mutant_name": "Superdave",
    "power": "Flight",
    "real_name": "Dave",
    "eligibility_begins_at": "2010-01-01T00:00:00.000Z",
    "eligibility_ends_at": "2020-01-01T00:00:00.000Z",
    "may_advise_beginning_at": "2016-01-01T00:00:00.000Z",
    "url": "https://mutant-school.herokuapp.com/api/v1/mutants/2"
  },
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

This endpoint retrieves all mutants.

### HTTP Request

`GET https://mutant-school.herokuapp.com/api/v1/mutants`
