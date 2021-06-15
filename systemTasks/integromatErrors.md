# Integromat errors

Sometimes, an integromat scenario will fail, returning some HTTP response code.

This can either be due to an error with the way the scenario functions, or downtime with some service used within the scenario

There is error handling in place for some (but not all) scenarios

should an error occur on a module where there is error handling, the error will be handled by the modules following the error handling (usually involving the sending of an email), rather than crashing and stopping the scenario from running

Though there is a small library of these error codes below, the internet is often the best place to figure out what is going on, particularly with errors with well documented api's such as Dropbox

- `[50x] - internal server error`
  - this usually indicates an error with the service in question
  - try waiting or refreshing the connection
- `[40x] - collection error`
  - this usually indicates an error with the data you are trying to manipulate/ obtaining data in an incorrect way
  - try switching the way you're doing things
-
