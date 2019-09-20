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
5. Click on install and finish the installation.

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
4. In package.json file, we have to:
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
  "author": "author name",
  "license": "ISC"
}
```
5. Execute following npm command to install nodemailer in project. This will also add entry to package.json file in dependency array.
```
npm install --save nodemailer
```
### Execution

![Imgur](https://i.imgur.com/foo8BlX.png)

1. To send email using gmail as a service from third party apps like our nodejs app, we have to enable 'Allow less secure apps' in gmail. Login in your gmail account and visit "https://myaccount.google.com/lesssecureapps" and enable the 'Allow less secure apps'

2. Now create a file mailer.js where we will write code to send emails.
3. In mailer.js, include nodemailer.
```
// include nodemailer
const nodemailer = require('nodemailer');
```

4. declare variables
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
6. Set up message options (who sends what to whom)
```
// email options
let mailOptions = {
    from: fromMail,
    to: toMail,
    subject: subject,
    text: text
};
```
7. Deliver the mail options to sendMail method of transport object created previously.
```
// send email
transporter.sendMail(mailOptions, (error, response) => {
    if (error) {
        console.log(error);
    }
    console.log(response)
});
```

![Imgur](https://i.imgur.com/cGDwK1f.png)
```
node mailer.js
```
8. This will send the email to recipent email, you can assign multiple email addresses to toMail variable. This will send email to multiple emails.

```
let toMail = 'gnbaviskar2@gmail.com,gnbaviskar3@gmail.com';
```

![Imgur](https://i.imgur.com/l8BWAog.png)

### Working code:
```
// include nodemailer
const nodemailer = require('nodemailer');
// declare vars
let fromMail = 'ghanshyamnetcore@gmail.com';
let toMail = 'gnbaviskar2@gmail.com';

// let toMail = 'gnbaviskar2@gmail.com,gnbaviskar3@gmail.com';

let subject  = 'An email using nodejs app';
let text = "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book." 

// auth
const transporter = nodemailer.createTransport({
    service: 'gmail',
    auth: {
        user: 'ghanshyamnetcore@gmail.com',
        pass: 'account_password'
    }
});

// email options
let mailOptions = {
    from: fromMail,
    to: toMail,
    subject: subject,
    text: text
};

// send email
transporter.sendMail(mailOptions, (error, response) => {
    if (error) {
        console.log(error);
    }
    console.log(response)
});
```
You can download the code from:
https://github.com/ghansh22/email_using_nodejs.git

### Errors:
```
{ Error: Invalid login: 535-5.7.8 Username and Password not accepted. Learn more at
535 5.7.8  https://support.google.com/mail/?p=BadCredentials w11sm630141pfd.116 - gsmtp
    at SMTPConnection._formatError (C:\Users\light\Desktop\send_emails\node_modules\nodemailer\lib\smtp-connection\index.js:781:19)
    at SMTPConnection._actionAUTHComplete (C:\Users\light\Desktop\send_emails\node_modules\nodemailer\lib\smtp-connection\index.js:1516:34)
    at SMTPConnection._responseActions.push.str (C:\Users\light\Desktop\send_emails\node_modules\nodemailer\lib\smtp-connection\index.js:554:26)
    at SMTPConnection._processResponse (C:\Users\light\Desktop\send_emails\node_modules\nodemailer\lib\smtp-connection\index.js:940:20)
    at SMTPConnection._onData (C:\Users\light\Desktop\send_emails\node_modules\nodemailer\lib\smtp-connection\index.js:746:14)
    at TLSSocket.SMTPConnection._onSocketData (C:\Users\light\Desktop\send_emails\node_modules\nodemailer\lib\smtp-connection\index.js:189:46)
    at TLSSocket.emit (events.js:198:13)
    at addChunk (_stream_readable.js:288:12)
    at readableAddChunk (_stream_readable.js:269:11)
    at TLSSocket.Readable.push (_stream_readable.js:224:10)
  code: 'EAUTH',
  response:
   '535-5.7.8 Username and Password not accepted. Learn more at\n535 5.7.8  https://support.google.com/mail/?p=BadCredentials w11sm630141pfd.116 - gsmtp',
  responseCode: 535,
  command: 'AUTH PLAIN' }
```
- We have to enable gmail service to use it in third party apps. In case we miss to do so, we may face such error. To resolve this error just login in gmail account and enable less secure apps using this link https://myaccount.google.com/lesssecureapps
- Another reason for this error can be wrong email(sender) or password. Please check the email address and password. Also check whether you entered any space in email/password string mistakely.

```
internal/modules/cjs/loader.js:638
    throw err;
    ^

Error: Cannot find module 'nodemailer'
    at Function.Module._resolveFilename (internal/modules/cjs/loader.js:636:15)
    at Function.Module._load (internal/modules/cjs/loader.js:562:25)
    at Module.require (internal/modules/cjs/loader.js:692:17)
    at require (internal/modules/cjs/helpers.js:25:18)
    at Object.<anonymous> (C:\Users\light\Desktop\send_emails\mailer.js:2:20)
    at Module._compile (internal/modules/cjs/loader.js:778:30)
    at Object.Module._extensions..js (internal/modules/cjs/loader.js:789:10)
    at Module.load (internal/modules/cjs/loader.js:653:32)
    at tryModuleLoad (internal/modules/cjs/loader.js:593:12)
    at Function.Module._load (internal/modules/cjs/loader.js:585:3)
```

- If your nodemailer module installation failed, you may face this error. To resolve this error go to installation steps, and install nodemailer.
- You can also install nodemailer globally using following command
```
npm install -g nodemailer
```
linux/mac user do it with sudo to install the nodemailer:
```
sudo npm install -g nodemailer
```
