## Intro

There will be two actors involved in two rounds of testing: UserSimple and UserComplex, and all testing will be done manually. In general, the tasks will be divided as follows: UserSimple will be responsible for testing all page size-responsively and all forms with various normal data that will be predetermined by some rule, and UserComplex will be responsible for testing all forms with various data/Payload XSS and closely observing the response detail. The testing can be continuously, during the development process until the final phase on April 5-10, 2023. There are some rules to directive the testing process and how to record the testing results, so the testing will be `inflexible`.

The testing with UserSimple, which attempts to test all forms with various normal data, tends to be more suitable for `black box testing`, where testing is done from the user's point of view or the use of the application without paying attention to internal implementation details. Meanwhile, the testing with UserComplex, which attempts to test with data/Payload XSS and closely observe the response, tends to be more suitable for `grey box testing`, where testing is done with some knowledge of the design and structure of the application.

## Guideline for UserSimple
