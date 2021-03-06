# Free Responsive HTML Email Template

Sometimes all you want is a really simple responsive HTML email template with a clear call-to-action button. Here it is.

[See live preview - email.html](email.html?raw=true).

[See live preview- email-inlined.html](https://github.com/sk-rama/interested/blob/main/html-email-templates/responsive-html-email-template/email-inlined.html).

![](img/email.png?raw=true)

## Inline your CSS before sending

Email is notorious for inconsistent CSS support. Therefore you should always inline your CSS and send a test to yourself before sending.

### Sending emails directly from your codebase or using a developer service?

For an API service (like Mailgun, SendGrid, Postmark) **you need to inline the CSS before sending**. See `email-inlined.html` for an example.

You can use this [Email CSS Inliner](https://htmlemail.io/inline/) and then [send a test email to yourself](https://postdrop.io) to verify it works as expected. 

* Copy all of email.html
* Paste the HTML as the source into the inliner
* Copy the HTML output and use this as the email template you send

### Sending emails using a marketing service like Mailchimp?

Use the template `email.html` as is. They'll put the CSS inline for you when you put together your campaign.

## Images in email

When inserting images remember to include the following attributes or risk them breaking in different clients:

* `src`
* `alt`
* `width`
* `height`
* `border`

Example:

`<img src="https://absolute-path-to-image.jpg" alt="Useful alt text" width="500" height="300" border="0" style="border:0; outline:none; text-decoration:none; display:block;">`

[More information here](https://www.smashingmagazine.com/2017/01/introduction-building-sending-html-email-for-web-developers/)

## Tried and tested on all major email clients

Tested on mobile, desktop and web.

![Templates Tested on Email Clients]!(img/email2.jpg?raw=true)


## More HTML email resources

* [10 HTML Email Templates for Developers](https://htmlemail.io)
* [An Introduction To Building And Sending HTML Email](https://www.smashingmagazine.com/2017/01/introduction-building-sending-html-email-for-web-developers/)
* [Grunt Email Design Workflow](https://github.com/leemunroe/grunt-email-design)
* [Everything Web Developers Need To Know About Transactional Email](https://webdesign.tutsplus.com/articles/everything-developers-need-to-know-about-sending-transactional-email--cms-31759)
* [Manage and Send Email Templates To Yourself](https://postdrop.io)

