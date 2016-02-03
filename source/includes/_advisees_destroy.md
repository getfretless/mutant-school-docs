## Delete an Advisor-Advisee relationship

```http
DELETE /api/v1/mutants/2/advisees/4 HTTP/1.1
Host: mutant-school.herokuapp.com
Connection: close
User-Agent: Paw/2.2.9 (Macintosh; OS X/10.11.2) GCDHTTPRequest


```

```shell
curl -X "DELETE" "https://mutant-school.herokuapp.com/api/v1/mutants/2/advisees/4"
```

```ruby
require 'net/http'
require 'net/https'

def send_request
  # My API (3) (DELETE )

  begin
    uri = URI('https://mutant-school.herokuapp.com/api/v1/mutants/2/advisees/4')

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

> Expected response: **200 OK**, with JSON structured like this:

```json
{
  "id": 4,
  "mutant_name": "Megamarie",
  "power": "Super-human strength",
  "real_name": "Marie",
  "created_at": "2016-02-03T05:27:10.292Z",
  "updated_at": "2016-02-03T05:35:21.632Z",
  "eligibility_begins_at": "2010-01-01T00:00:00.000Z",
  "eligibility_ends_at": "2020-01-01T00:00:00.000Z",
  "may_advise_beginning_at": "2016-01-01T00:00:00.000Z",
  "url": "https://mutant-school.herokuapp.com/api/v1/mutants/4"
}
```

This endpoint removes an advisor-advisee relationship between two mutants. No records are destroyed. Rather, the advisee's record is updated with a NULL advisor.

### HTTP Request

`DELETE https://mutant-school.herokuapp.com/api/v1/mutants/<ADVISOR_ID>/advisee/<ID>`

### URL Parameters

Parameter  | Description
---------  | -----------
ADVISOR_ID | The ID of the advisor mutant
ID         | The ID of the advisee mutant

### Errors

Error Code | Meaning
---------- | -------
404        | Not Found -- Either the advisor mutant or the advisee mutant cannot be found, or there is no such relationship between the two.
500        | Internal Server Error -- It's probably our fault.
