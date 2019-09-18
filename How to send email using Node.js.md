# How to send email using Node.js?

Nodejs is server side javascript runtime built on chrome v8 engine. Node js allows us to use javascript on server side.

We will be using windows 10 machine for this tutorial. Visit 'https://nodejs.org/en/' you will find following options. Right now 10.16.3 stable version available.

### Prerequisites
You shoud be having a working windows machine to begin with this tutorial.

### Installation
![download button for node js](https://i.imgur.com/usNb657.png)

- Click on this button to download msi installer to install nodejs. Double click on the msi file to start the installer. Like any other installation on windows, we will click next buttons several times

![accept terms](https://i.imgur.com/RfVrQWC.png)

- Read and accept the terms in licence agreement
 
![default location](https://i.imgur.com/Ia26o81.png)

- select default location for nodejs (remember this location to verify the insatllation)

![finish installation](https://i.imgur.com/Guh7hvv.png)
- click on install and finish the installation.

##### Verify whether nodejs installation:
- Open nodejs installation directory, which we had selected at the time of installation.  In our case it is C:\Program Files\nodejs. If you dont remember the insatllation directory, just go to c drive and find Program Files. In this directory you should find nodejs directory, as it is default location. Here we will find node js application, just double click it, A command prompt will appear. 

![Try basic js in nodejs window](https://i.imgur.com/V3JJTjO.png)
- Lets try basic javascript to test our nodejs installation.
```
var message = `Hello world`
console.log(message)
```

Nodejs comes with NPM. NPM(Node package manager) is the default package manager for Nodejs. Unfortunately Nodejs does not include any preinstalled module or library to send emails. We have to install a third party module like NodeMailer or AlphaMail using NPM.

- To begin with our project to send email, lets create a folder named send_emails, press shift and right click in the folder. You should have an option 'Open PowerShell Window Here' click on this option. Windows PowerShell will appear.

![Powershell window](https://i.imgur.com/pI7Hh3J.png)

- Incase you dont find the option to open powershell from this folder, just copy the absolute path of the folder, open powershell from windows start menu and change directory in powershell

![Imgur](https://i.imgur.com/VKzJZd9.png)

- We will use package.json file to install nodemailer from NPM. In powershell window, type following command

```
npm init
```
 - Add description in prompt, then write mailer.js as entry point file.write your name in author. Press enter to proceed

- Now package.json file will be available in the project folder. In powershell window, make sure your powershell working directory is the project folder. Type following command to install nodemailer using NPM.

```
npm install --save nodemailer
```

- This will add dependecies array to package.json

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
  "license": "ISC",
  "dependencies": {
    "nodemailer": "*"
  }
}
```

- Now create a file mailer.js which is entry point mentioned earlier in package.json.

![Imgur](https://i.imgur.com/foo8BlX.png)

- To send email using gmail as service from third party apps like our nodejs app, we have to enable 'Allow less secure apps' in gmail. Login in your gmail account and visit "https://myaccount.google.com/lesssecureapps" and enable the 'Allow less secure apps'


- In mailer.js, include nodemailer.
```
// include nodemailer
const nodemailer = require('nodemailer');
```

- declare variables
   - fromMail: sender email address
   - toEmail: recipent email address
   - subject: email subject line
   - text: email body text
```
// declare vars,
let fromMail = 'ghanshyamnetcore@gmail.com';
let toMail = 'gnbaviskar2@gmail.com';
let subject  = 'An email using nodejs app';
let text = "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book." 
```


- Define a transporter object. Make sure to replace account_password with your gmail password. 
```
const transporter = nodemailer.createTransport({
    service: 'gmail',
    auth: {
        user: fromMail ,
        pass: 'account_password'
    }
});
```
- Set up message options (who sends what to whom)
```
// email options
let mailOptions = {
    from: fromMail,
    to: toMail,
    subject: subject,
    text: text
};
```
- Deliver the mail options to sendMail method of transport object created previously.
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

- This will send the email to recipent email, you can assign multiple email addresses to toMail variable. This will send email to multiple emails.

```
let toMail = 'gnbaviskar2@gmail.com,gnbaviskar3@gmail.com';
```

You can download the code from:
```
https://github.com/ghansh22/email_using_nodejs.git
```