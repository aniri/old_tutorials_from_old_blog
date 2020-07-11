# How to add confirmation emails to google forms

Have you ever used google forms to get some input from your users? It is really easy to set up a google form, add the required input fields and share the form with your users. [Here's an example of a google form](https://docs.google.com/forms/d/e/1FAIpQLSfUGU0w5GMtBxgDKdrj8syo91Z5pdowyoLBi0MZ3yUCvvGZfg/viewform).

After the users fill in the form, they will see a short confirmation message on the screen and their responses will be stored. You might also want your users to get a confirmation email after filling out the form. This is not the default behavior of google forms though so you will have to add a small script to do so.

If you fill in and submit the example form you will receive such a confirmation email and see what we are going to set up.

### Here's what you have to do:

- from the form edit screen choose the tools menu option
- pick `script manager` and click the `new` button
- you will be redirected to a new page for adding the script
- pick `form` in the popup
- add a name for your script file
- clear the code if there is any example code in there
- add the following code:

```
function onFormSubmit(e) {
     var response = e.response;
     var itemResponses = response.getItemResponses();
     var name = itemResponses[0].getResponse();
     var emailAddress = itemResponses[1].getResponse();
     var comments = itemResponses[2].getResponse();
     var subject = "Form confirmation";
     var emailBody = "Hello " + name + "!" +
     "\n\n This is a confirmation email!" +
     "\n\n Your details: " +
     "\n\t Name: " + name +
     "\n\t Email: " + emailAddress +
     "\n\t Comments " + comments +
     "\n\n Thanks for filling out the form!";
     MailApp.sendEmail(emailAddress, subject, emailBody);
}
```

The code is pretty straightforward: it received the user response as a parameter, it gets an array with the individual answers for each question (`itemResponses`), it gets the response for each question, sets the subject and the body of the email to be sent and sends the email to the user.

There's is only one more step to go, we need to set a trigger for this function:

- go to `resources` from the menu
- pick current `projects triggers`
- you will notice there are no triggers set up. click on `click here to add one now`
- you need to select the method to run (`onFormSubmit`) and the trigger event `from form` and `on form submit`
- you can also set the notification options - the default is to receive a daily email with the errors that come up, but for testing purposes you could set it to send error messages immediately
- click save and authorize the app as requested

And that's it! you now have the needed script. You need to go back to the forms edit page, from the scripts manager popup you need to refresh the scripts list and pick the newly added `onFormSubmit` script.

And you're done! You're ready to test out your form and send it out to your users!

Let me know if you have any questions! :)
