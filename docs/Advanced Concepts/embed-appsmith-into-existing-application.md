---
description: Guide on how to embed Appsmith into an existing application
---

# Embed Apps

{% embed url="https://www.youtube.com/watch?v=l7508s-5VwU" %}

Tools and Dashboards are great as an app and on a website, and now, you can have it both in one go by embedding apps to your website! In this guide, you'll learn how to embed Appsmith Apps into any website.

For this guide, we’ll be considering the [Customer Support Dashboard](https://app.appsmith.com/applications/5f2aeb2580ca1f6faaed4e4a/pages/5f2d61b580ca1f6faaed4e79) from the demo app’s, and embed that into an HTML page. You can also check out the live preview [here](https://appsmith-embed.netlify.app/).

### Creating HTML Page

Firstly, let’s create an HTML page and call it \``cs_dashboard.html`\`. Now, add the basic HTML structure to make it an HTML page:

```markup
<!DOCTYPE html>
<html>
<head>
    <title> Customer Support Dahboard </title>
</head>
<body>

</body>
</html>
```

You’ll also have to make sure that your app is public to embed into other application. You can do this by clicking on the Share option on the top toolbar and toggle the viewing option to **Public**. Here’s a GIF showing the same:

![Making the Application Public on Appsmith](https://lh3.googleusercontent.com/qpfBY24qpHXf\_21sq52dNAXR52axc260x\_ZFClh2fb8zUuEeM3Cd9fbKeLslK4jUXb4KTYucJXB92AxAOkHwKpj0ke15OJ5EH8EXHoN2bmtz5loZHmQ9ofvcCGEdsYyDVJQ04SUg)

Next, create an `iframe` tag and add the shareable link from share options to the `src` attribute with height and width set to `500` and `100%` respectively.

Include the meta tag in head to ensure that the embedded application renders responsively on different screen sizes:

```markup
<!DOCTYPE html>
<html>
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1"
    <title></title>
</head>
<body>
    <iframe src="https://app.appsmith.com/applications/5f2aeb2580ca1f6faaed4e4a/pages/5f2d61b580ca1f6faaed4e79" height="700" width="100%"></iframe>
</body>
</html>
```

### Opening the HTML Page

{% hint style="info" %}
If you are opening the HTML page as a `file:` then the browser won't allow you to do that. The HTML file needs to come from a server.
{% endhint %}

After creating the HTML page, save it as `cs_dashboard.html` and have it be served by a HTTP server. This can be done in several ways:

#### Serving a HTML file with Node.js&#x20;

Once you have created your HTML file, create a new `app.js`` `**``** file. Paste the below mentioned code and edit your HTML file name.

```
const http = require('http');
const fs = require('fs');

http.createServer(function(req, res) {
    res.writeHead(200, { 'content-type': 'text/html' });
    const html = fs.readFileSync('./cs_dashboard.html');
    res.end(html);
}).listen(3000, () => {
    console.log('running on 3000');
});
```

Now, in the terminal, run `node app.js`

This will prompt a `running on 3000` message. Next, go to your browser and open [http://localhost:3000/](http://localhost:3000/)&#x20;

This will open your HTML file.

![Sceenshot of Appsmith Embed](../.gitbook/assets/Appsmith\_embed.png)

#### Running npx http-server

Let's look at another way to open an HTML file.

Now, if you have _Node JS_ installed, go to the command terminal and run:

```
npx http-server
```

Next, open [http://localhost:8080/cs\_dashboard.html](http://localhost:8080/cs\_dashboard.html) and it should open the HTML File.

### Modifying Layout

If you want to get your app to use the whole page in your browser, you can still change your height and width parameters like so:

```markup
<!DOCTYPE html>
<html>
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1"
    <title></title>
</head>
<body>
    <iframe src="https://app.appsmith.com/applications/5f2aeb2580ca1f6faaed4e4a/pages/5f2d61b580ca1f6faaed4e79"frameborder="0" scrolling="yes" seamless="seamless" style="display:block; width:100%; height:100vh;"></iframe>
</body>
</html>
```

#### Remove Appsmith Top Bar

Additionally, you can also see the Appsmith toolbar on the top, you can remove this by adding **`?embed=true`** to the share URL. Update the code to the following:

```markup
<!DOCTYPE html>
<html>
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1"
    <title></title>
</head>
<body>
    <iframe src="https://app.appsmith.com/applications/5f2aeb2580ca1f6faaed4e4a/pages/5f2d61b580ca1f6faaed4e79?embed=true" height="700" width="100%"></iframe>
</body>
</html>
```

Awesome! Now you can see the app without any toolbar! Below is a screenshot:

![Appsmith Embed with ?embed=true propert](../.gitbook/assets/embed=true.png)
