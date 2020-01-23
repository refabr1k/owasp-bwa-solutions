## Role Based Access Control

## Stage 1: Bypass business layer access control
After login as `tom` click `ViewProfile` use burp (or any intercept http tool) to intercept the button action. You will see in the POST request `employee_id=105&action=ViewProfile`

Modify to `action=DeleteProfile`

## Stage 2: Add business layer access control
(skipped)

## Stage 3: Bypass data layer access control
Similar to stage1 (above) intercept POST request for `ViewProfile` button and modify id parameters eg. `employee_id=112`

## Stage 4: Bypass data layer access control
Similar to stage1 (above) intercept POST request for `ViewProfile` button and modify id parameters eg. `employee_id=112`
