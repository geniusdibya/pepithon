# How to send email using Node.js?

Nodejs is a server-side javascript runtime environment built on chrome v8 engine. It allows us to use javascript on server side. Currently Nodejs 10.16.3 stable version available.

Nodejs is cross-platform. It is available for Windows, linux and Mac. I will be using Windows 10 machine for this tutotial.

## Prerequisites
 - A working windows 10 machine.
 - Nodejs libraries installed.
 - Nodemailer NPM module installed.
  
### Installation
(If you have nodejs and nodemailer module installed, you can skip to execution step) 


![download button for node js](https://i.imgur.com/usNb657.png)
1. Install Node Js: Visit https://nodejs.org/en/ to download the NodeJs MSI installer. I am using version 10.16.3 for this tutorial. 

![Imgur](https://i.imgur.com/m60WFNb.png)

2. Double click on the msi file to start the installer, then click 'Run'. Like any other installation on windows, we will click next button several times  

![accept terms](https://i.imgur.com/RfVrQWC.png)

3. Read and accept the terms in licence agreement
 
![default location](https://i.imgur.com/Ia26o81.png)

4. Select default location for nodejs (remember this location to verify the installation)

![finish installation](https://i.imgur.com/Guh7hvv.png)
- Click on install and finish the installation.

##### Verify nodejs installation working properly:
- Open nodejs installation directory, which we had selected at the time of installation. In our case it is C:\Program Files\nodejs. If you don't remember the installation directory, just go to c drive and find Program Files. In this directory, you should find nodejs directory, as it is the default location. Here we will find node js application, just double click it, A command prompt will appear. 

![Try basic js in nodejs window](https://i.imgur.com/V3JJTjO.png)
- Lets try basic javascript to test our nodejs installation.
```
var message = `Hello world`
console.log(message)
```
#### Nodemailer module Installation :
-. Nodejs comes with NPM. NPM(Node package manager) is the default package manager for Nodejs. Nodejs does not include any preinstalled module or library to send emails. We have to install a third-party modules like NodeMailer or AlphaMail using NPM.

![Powershell window](https://i.imgur.com/pI7Hh3J.png)
1. To begin with, our project to send an email, let's create a folder named send_emails, press shift and right-click in the folder. You should have an option 'Open PowerShell Window Here' click on this option. Windows PowerShell will appear.

2. Incase you dont find the option to open powershell from this folder, just copy the absolute path of the folder, open powershell from windows start menu and change directory in powershell

![Imgur](https://i.imgur.com/VKzJZd9.png)

3. Create package.json file to install nodemailer from NPM. In powershell window, type following npm command

```
npm init
```
- In package.json file, we have to:
  - Add a description in prompt
  - Add entry point  file: mailer.js.
  - Add author name.
  - Type 'yes' to proceed with changes.

This will create package.json file in our project folder.
```
{
  "name": "send_emails",
  "version": "1.0.0",
  "description": "'A simple app to send emails from nodejs'",
  "main": "mailer.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "ghanshyam",
  "license": "ISC",
  "dependencies": {
    "nodemailer": "^6.3.0"
  }
}

```
### Execution

![Imgur](https://i.imgur.com/foo8BlX.png)

1. To send email using gmail as a service from third party apps like our nodejs app, we have to enable 'Allow less secure apps' in gmail. Login in your gmail account and visit "https://myaccount.google.com/lesssecureapps" and enable the 'Allow less secure apps'

2. Now create a file mailer.js where we will write code to send emails.
- In mailer.js, include nodemailer.
```
// include nodemailer
const nodemailer = require('nodemailer');
```

3. declare variables
   - fromMail: sender email address
   - toEmail: recipent email address
   - subject: email subject line
   - text: email body text
```
// declare vars,
let fromMail = 'Enter sender email address';
let toMail = 'Enter recipient email address to which email will be sent';
let subject = 'Enter subject line here';
let text = "Enter email content." 
```


4. Define a transporter object. Make sure to replace account_password with your gmail password. 
```
const transporter = nodemailer.createTransport({
    service: 'gmail',
    auth: {
        user: fromMail ,
        pass: 'account_password'
    }
});
```
5. Set up message options (who sends what to whom)
```
// email options
let mailOptions = {
    from: fromMail,
    to: toMail,
    subject: subject,
    text: text
};
```
6. Deliver the mail options to sendMail method of transport object created previously.
```
// send email
transporter.sendMail(mailOptions, (error, response) => {
    if (error) {
        console.log(error);
    }
    console.log(response)
});
```
![Imgur](https://i.imgur.com/l8BWAog.png)

7. This will send the email to recipent email, you can assign multiple email addresses to toMail variable. This will send email to multiple emails.

```
let toMail = 'gnbaviskar2@gmail.com,gnbaviskar3@gmail.com';
```

You can download the code from:
https://github.com/ghansh22/email_using_nodejs.git
