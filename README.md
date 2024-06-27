# customise-google-form
## Description
Google Forms is a convenient tool for collecting data, but sometimes you want more control over the design and functionality of your form. Create your custom redirect URL when the form is submitted or a popup is shown. Converting Google Forms to HTML forms provides flexibility and customization options that fit your needs. In this direction, we'll walk through a straightforward method of converting Google Forms to HTML forms, including storing the data in an Excel sheet and adding custom form notifications and re-directions using jQuery.

## Step 1: Create Your Google Form
Begin by creating a Google Form with all the necessary fields and settings. Once you have your form ready, proceed to the next steps.

## Step 2: Obtain Pre-filled Link
Google Forms allow you to pre-fill form fields by generating a pre-filled link. This link can be used to populate specific fields in your HTML form automatically. To obtain a pre-filled link:
Open your Google Form.
Click on the three dots menu in the upper right corner.
Select "Get pre-filled link" from the dropdown menu.
Adjust the pre-filled fields as needed and click "Submit."
Copy the generated link.

Get pre-filled link: After clicking on the link, a page like this will open, then after filling this form, click on get link.

Then after clicking on the copy link, we will get a link like this:
https://docs.google.com/forms/d/e/1FAIpQLSdHGzK7M_BRLKgZugftxJv4jilrcuvXjRkd5Fdo9Gw3aOwO0A/viewform?usp=pp_url&entry.2005620554=ranjan&entry.1045781291=ranjanroy881753@gmail.com&entry.1065046570=sitamarhi&entry.1166974658=7347404501&entry.839337160=this+is+test

## Step 3: Convert to HTML Form
To convert your Google Form to an HTML form:
Open a text editor (like Notepad Sublime Text or VS code ).
Start creating your HTML form structure. You can use standard HTML form elements such as <input>, <select>, and <textarea>.
Paste the pre-filled link obtained in Step 2 as the value of the corresponding form field.
Customize the design and layout of the HTML form according to your preferences.
Save the file with the .html extension.
I am using bootstrap for this, I got the ready form from here, so you can also take the code from it if you want.

<form action="https://docs.google.com/forms/u/0/d/e/1FAIpQLSdHGzK7M_BRLKgZugftxJv4jilrcuvXjRkd5Fdo9Gw3aOwO0A/formResponse" id="gform">
                            <div class="row">
                                <div class="col-sm-12" style="padding: 5px;">
                                    <h1>Contact form</h1>
                                </div>
                            </div>
    
                            <div class="row">
                                <div class="col-sm-6">
                                    <div class="inputBox ">
                                        <div class="inputText">Name</div>
                                        <input type="text" name="entry.2005620554" class="input" required>
                                    </div>
                                </div>
    
                                <div class="col-sm-6">
                                    <div class="inputBox">
                                        <div class="inputText">Address</div>
                                        <input type="text" name="entry.1065046570" class="input" required>
                                    </div>
                                </div>
                            </div>
    
                            <div class="row">
                                <div class="col-sm-6">
                                    <div class="inputBox">
                                        <div class="inputText">Email</div>
                                        <input type="text" name="entry.1045781291" class="input" required>
                                    </div>
                                </div>
    
                                <div class="col-sm-6">
                                    <div class="inputBox">
                                        <div class="inputText">Mobile</div>
                                        <input type="text" name="entry.1166974658" class="input" required>
                                    </div>
                                </div>
                            </div>
    
                            <div class="row">
                                <div class="col-sm-12">
                                    <div class="inputBox">
                                        <div class="inputText">Message</div>
                                        <textarea class="input" name="entry.839337160"></textarea>
                                    </div>
                                </div>
                            </div>
    
                            <div class="row">
                                <div class="col-sm-12">
                                    <input type="submit" name="" class="button" value="Send Message">
                                </div>
                            </div>
                    </form>

The action attribute specifies the URL where form data will be submitted. In this case, it's a Google Form URL.

<form action="https://docs.google.com/forms/u/0/d/e/1FAIpQLSdHGzK7M_BRLKgZugftxJv4jilrcuvXjRkd5Fdo9Gw3aOwO0A/formResponse" id="gform">

The action attribute specifies the URL where form data will be submitted. In this case, it's a Google Form URL.

Form Fields: The form includes several input fields for collecting user information:
Name :

<input type="text" name="entry.2005620554" class="input" required>

Address:
<input type="text" name="entry.1065046570" class="input" required>

Email:
<input type="text" name="entry.1045781291" class="input" required>

Mobile:
<input type="text" name="entry.1166974658" class="input" required>

Message:
<textarea class="input" name="entry.839337160"></textarea>
Each input field has a name attribute corresponding to the field ID in the Google Form. The required attribute makes these fields mandatory.
Note : It is important to keep one thing in mind the filled form that we have kept as required in Google form will also be required in filled HTML.
Submit Button:

<input type="submit" name="" class="button" value="Send Message">

## Step 5: Custom Form Notifications and Redirection with jQuery
To add custom form notifications and redirection using jQuery:
Include the jQuery library in your HTML file by adding the following script tag before the closing </body> tag:

<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>

and also add jQuery form Plugin as well 

<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery.form/4.2.2/jquery.form.min.js" integrity="sha256-2Pjr1OlpZMY6qesJM68t2v39t+lMLvxwpa8QlRjJroA=" crossorigin="anonymous"></script> 

Write jQuery scripts to handle form submission, validation, notifications, and redirection based on your requirements.

<script>
 $('#gform').submit(function (event) {
            event.preventDefault()
            var extraData = {}
            $('#gform').ajaxSubmit({
                data: extraData,
                dataType: 'jsonp',  // This won't really work. It's just to use a GET instead of a POST to allow cookies from different domain.
                error: function () {
                    // Submit of form should be successful but JSONP callback will fail because Google Forms
                    // does not support it, so this is handled as a failure.
                    alert('Form Submitted. Thanks.')
                    // You can also redirect the user to a custom thank-you page:
                    // window.location = 'http://www.mydomain.com/thankyoupage.html'
                }
            })
        })
</script>

## Step 6: Store Data in Excel Sheet

To store form submissions in an Excel sheet, you can utilize Google Sheets integration with Google Forms. Follow these steps:
Open your Google Form.
Click on the "Responses" tab.
Click on the Sheets icon to create a new Google Sheets spreadsheet linked to your form.
All form submissions will be automatically stored in the linked spreadsheet.

## Credits
I have used the work on this website:
https://www.linkedin.com/pulse/google-form-html-conversion-easy-method-customization-ranjan-roy-1fose/