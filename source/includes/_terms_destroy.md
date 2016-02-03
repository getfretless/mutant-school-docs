## Delete a Specific Term

```http
DELETE /api/v1/terms/5 HTTP/1.1
Host: mutant-school.herokuapp.com
Connection: close
User-Agent: Paw/2.2.9 (Macintosh; OS X/10.11.2) GCDHTTPRequest


```

```shell
curl -X "DELETE" "https://mutant-school.herokuapp.com/api/v1/terms/5"
```

```ruby
require 'net/http'
require 'net/https'

def send_request
  # Terms#destroy (DELETE )

  begin
    uri = URI('https://mutant-school.herokuapp.com/api/v1/terms/5')

    # Create client
    http = Net::HTTP.new(uri.host, uri.port)
    http.use_ssl = true
    http.verify_mode = OpenSSL::SSL::VERIFY_PEER


    # Create Request
    req =  Net::HTTP::Delete.new(uri)

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
// Terms#destroy (DELETE https://mutant-school.herokuapp.com/api/v1/terms/5)

jQuery.ajax({
    url: "https://mutant-school.herokuapp.com/api/v1/terms/5",
    type: "DELETE",
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

> Expected response: **204 No Content**.

This deletes a specific mutant and any associated enrollments.

### HTTP Request

`DELETE https://mutant-school.herokuapp.com/api/v1/terms/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the term to delete

### Errors

Error Code | Meaning
---------- | -------
404        | Not Found -- The specified term could not be found. It may have already been deleted.
500        | Internal Server Error -- It's probably our fault.
