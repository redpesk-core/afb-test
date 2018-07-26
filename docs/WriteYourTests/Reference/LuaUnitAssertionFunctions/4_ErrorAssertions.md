# Error assertions

Error related assertions, to verify error generation and error messages.

* **_AFT.assertError(func, ...)**

    Assert that calling functions func with the arguments yields an error. If the function does not yield an error, the assertion fails.

    Note that the error message itself is not checked, which means that this function does not distinguish between the legitimate error that you expect and another error that might be triggered by mistake.

    The next functions provide a better approach to error testing, by checking explicitly the error message content.

>**Note**
>When testing LuaUnit, switching from assertError() to assertErrorMsgEquals() revealed quite a few bugs!

* **_AFT.assertErrorMsgEquals(expectedMsg, func, ...)**

    Assert that calling function func will generate exactly the given error message. If the function does not yield an error, or if the error message is not identical, the assertion fails.

    Be careful when using this function that error messages usually contain the file name and line number information of where the error was generated. This is usually inconvenient. To ignore the filename and line number information, you can either use a pattern with assertErrorMsgMatches() or simply check if the message contains a string with assertErrorMsgContains() .

* **_AFT.assertErrorMsgContains(partialMsg, func, ...)**

    Assert that calling function func will generate an error message containing partialMsg . If the function does not yield an error, or if the expected message is not contained in the error message, the assertion fails.

* **_AFT.assertErrorMsgMatches(expectedPattern, func, ...)**

    Assert that calling function func will generate an error message matching expectedPattern . If the function does not yield an error, or if the error message does not match the provided pattern the assertion fails.

    Note that matching is done from the start to the end of the error message. Be sure to escape magic all magic characters with % (like -+.?\*) .