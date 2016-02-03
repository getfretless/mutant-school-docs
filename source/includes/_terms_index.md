# Terms

<aside class="notice">Terms are enrollment periods—like semesters—in <em>Mutant School</em>.</aside>

## Get All Terms

```http
GET /api/v1/terms HTTP/1.1
Host: mutant-school.herokuapp.com
Connection: close
User-Agent: Paw/2.2.9 (Macintosh; OS X/10.11.2) GCDHTTPRequest

```

```ruby
require 'net/http'
require 'net/https'

def send_request
  # Terms#index (GET )

  begin
    uri = URI('https://mutant-school.herokuapp.com/api/v1/terms')

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
// Terms#index (GET https://mutant-school.herokuapp.com/api/v1/terms)

jQuery.ajax({
    url: "https://mutant-school.herokuapp.com/api/v1/terms",
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
curl -X "GET" "https://mutant-school.herokuapp.com/api/v1/terms"
```

> Expected response: **200 OK**, with JSON structured like this:

```json
[
  {
    "id": 1,
    "begins_at": "2017-01-10T00:00:00.000Z",
    "ends_at": "2017-05-25T00:00:00.000Z",
    "url": "https://mutant-school.herokuapp.com/api/v1/terms/1"
  },
  {
    "id": 2,
    "begins_at": "2016-01-10T00:00:00.000Z",
    "ends_at": "2016-05-25T00:00:00.000Z",
    "url": "https://mutant-school.herokuapp.com/api/v1/terms/2"
  },
  {
    "id": 3,
    "begins_at": "2016-08-10T00:00:00.000Z",
    "ends_at": "2016-12-25T00:00:00.000Z",
    "url": "https://mutant-school.herokuapp.com/api/v1/terms/3"
  }
]
```

This endpoint retrieves all terms.

### HTTP Request

`GET https://mutant-school.herokuapp.com/api/v1/terms`
