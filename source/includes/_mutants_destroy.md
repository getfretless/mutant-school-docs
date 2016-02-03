## Delete a Specific Mutant

```http
DELETE /api/v1/mutants/3 HTTP/1.1
Host: mutant-school.herokuapp.com
Connection: close
User-Agent: Paw/2.2.9 (Macintosh; OS X/10.11.2) GCDHTTPRequest


```

```shell
curl -X "DELETE" "https://mutant-school.herokuapp.com/api/v1/mutants/3"
```

```ruby
require 'net/http'
require 'net/https'

def send_request
  # Mutants#destroy (DELETE )

  begin
    uri = URI('https://mutant-school.herokuapp.com/api/v1/mutants/3')

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
// Mutants#destroy (DELETE https://mutant-school.herokuapp.com/api/v1/mutants/3)

jQuery.ajax({
    url: "https://mutant-school.herokuapp.com/api/v1/mutants/3",
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

This deletes a specific mutant and any associated enrollments. If the mutant was an advisor, the advisees' records are updated to nullify the advisor relationship.

### HTTP Request

`DELETE https://mutant-school.herokuapp.com/api/v1/mutants/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the mutant to update

### Errors

Error Code | Meaning
---------- | -------
400        | Bad Request -- Your request is bad, and you should feel bad.
404        | Not Found -- The specified mutant could not be found. It may have already been deleted.
500        | Internal Server Error -- It's probably our fault.
