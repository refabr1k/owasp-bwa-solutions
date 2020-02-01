# Contents

  - [DOM-Based cross-site-scripting](/WebGoat/AJAX_security.md#1)
  - [Client Side Filtering](/WebGoat/AJAX_security.md#2)


---

## <a href="1"></a> Bypass a Path Based Access Control Scheme

Choose a file to view and intercept the HTTP request. I used burp and the follow POST request is seen

`File=OffByOne.html&SUBMIT=View+File`

Change the `File=` parameter to `../../reportBug.jsp` and forward request to successfully traverse to a directory that isnt allowed.

Note: I wasnt able to get `tomcat/conf/tomcat-users.xml` but because we know there is this `reportBug.jsp` file by mouse over the link **Report Bug** at the bottom of the page - you could see that the absolute path of this file has the same webapp root directory (`http://ipaddress/WebGoat/reportBug.jsp`) as the original file.

eg. From `WebGoat/lesson_plans/English/OffByOne.html` using the `../../` we could navigate back `WebGoat/` directory


---

## <a href="2"></a> Role Based Access Control

## Stage 1: Bypass business layer access control

After login as `tom` click `ViewProfile` use burp (or any intercept http tool) to intercept the button action. You will see in the POST request `employee_id=105&action=ViewProfile`

Modify to `action=DeleteProfile`

## Stage 2: Add business layer access control

(skipped)

## Stage 3: Bypass data layer access control

Similar to stage1 (above) intercept POST request for `ViewProfile` button and modify id parameters eg. `employee_id=112`

## Stage 4: Bypass data layer access control

Similar to stage1 (above) intercept POST request for `ViewProfile` button and modify id parameters eg. `employee_id=112`
