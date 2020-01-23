
## Bypass a Path Based Access Control Scheme

Choose a file to view and intercept the HTTP request. I used burp and the follow POST request is seen

`File=OffByOne.html&SUBMIT=View+File`

Change the `File=` parameter to `../../reportBug.jsp` and forward request to successfully traverse to a directory that isnt allowed.

Note: I wasnt able to get `tomcat/conf/tomcat-users.xml` but because we know there is this `reportBug.jsp` file by mouse over the link **Report Bug** at the bottom of the page - you could see that the absolute path of this file has the same webapp root directory (`http://ipaddress/WebGoat/reportBug.jsp`) as the original file.

eg. From `WebGoat/lesson_plans/English/OffByOne.html` using the `../../` we could navigate back `WebGoat/` directory

