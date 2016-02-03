## Delete a Specific Enrollment

```http
DELETE /api/v1/mutants/1/enrollments/10 HTTP/1.1
Host: mutant-school.herokuapp.com
Connection: close
User-Agent: Paw/2.2.9 (Macintosh; OS X/10.11.2) GCDHTTPRequest


```

```shell
curl -X "DELETE" "https://mutant-school.herokuapp.com/api/v1/mutants/1/enrollments/10"
```

```ruby
require 'net/http'
require 'net/https'

def send_request
  # Enrollments#destroy (DELETE )

  begin
    uri = URI('https://mutant-school.herokuapp.com/api/v1/mutants/1/enrollments/10')

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
// Enrollments#destroy (DELETE https://mutant-school.herokuapp.com/api/v1/mutants/1/enrollments/10)

jQuery.ajax({
    url: "https://mutant-school.herokuapp.com/api/v1/mutants/1/enrollments/10",
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

This endpoint deletes a specific enrollment for a specific mutant.

### HTTP Request

`DELETE https://mutant-school.herokuapp.com/api/v1/mutants/<MUTANT_ID>/enrollments/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
MUTANT_ID | The ID of the enrolled mutant
ID        | The ID of the enrollment to delete

### Errors

Error Code | Meaning
---------- | -------
404        | Not Found -- Either the mutant cannot be found, the enrollment cannot be found (possibly because it was already deleted), or the enrollment is not associated with the mutant.
500        | Internal Server Error -- It's probably our fault.
