#  Lesson 09: Troubleshooting and Package Reliability

In this exercise, you will add a Script Task to an Event Handler to alleviate the problem of sending too many email
 messages when errors occur in your packages. You would like to get messages when errors occur, but not a new message
 for
 every single error. In this script task, you will collect all of the errors and append each error message to the
 previously collected messages. Once all of the messages have been collected, you will use a PostExecute event
 handler to
 send the email message.

Every task in this package is intended to fail and generate an error message.