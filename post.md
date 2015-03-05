![Hook shot gif](https://d262ilb51hltx0.cloudfront.net/max/1600/1*yivSOqaBOsnXLN0Lis-y-w.gif)

**[Webhooks](https://developer.github.com/webhooks/) [are](http://www.boomerang.io/blog/why-webhooks-are-awesome) [awesome](http://blog.iron.io/2013/09/7-reasons-webhooks-are-magic.html).**

While I was working at [SendGrid](https://sendgrid.com/), most of the API demos I and the other evangelists did involved using webhooks. For example, I had a [GIF demo](https://github.com/heitortsergent/gimmegif) (GIFs are also awesome), my co-worker [Yamil](https://twitter.com/elbuo8) had a [Pokémon demo](https://github.com/elbuo8/sgdemo-pokemon), and both of them used [SendGrid's Parse Webhook](https://sendgrid.com/docs/API_Reference/Webhooks/parse.html).

These demos were really fun to do as they involve participation from the audience, but running them usually takes a little bit of work. If you wanted to try and run the demo yourself for example, you'd have to go to my demo's github repository and then:

```bash
# 1. git clone the repository
 
$ git clone https://github.com/heitortsergent/gimmegif.git
 
# 2. grab your SendGrid credentials (or create an account first and grab them)
 
# 3. grab any other service credentials (Giphy's API key for example)
 
# 4. set up your environment variables (using something like dotenv) 
 
$ echo SENDGRID_USERNAME=myusername
 
# 5. download ngrok
 
# 6. run ngrok
 
$ ngrok 3000
 
# 7. set up the webhook at SendGrid
 
# 8. run the demo
 
$ npm start
```

That's a few steps, and that's also considering the user has installed whatever node/Ruby/Python version your application is using. So, I decided to grab a few of these demos and add azk to it, to show how it can help new users set up a project and also make sure it's gonna run in their machines. (no more **"but it works on my machine!"**)

---

If you don't have azk installed, head here first: http://docs.azk.io/en/index.html

---

I wrote a little bit about azk in my [previous post](https://medium.com/azuki-news/im-joining-azuki-ac5958ec2687), but basically it's an **open-source CLI tool that you can use to easily orchestrate development environments** in your machine. It uses [VirtualBox](https://www.virtualbox.org/) and [Docker](https://www.docker.com/) under the hood, and it gives you a simple JS file to describe what kind of systems you need (node 0.10, Ruby 2.3, redis, MongoDB) and how they connect to each other. Here's a quick GIF showing it running:

```bash
# 1. git clone the repository
 
$ git clone http://github.com/username/yourawesomerepo.git
 
# 2. add your SendGrid/Twilio/Twitter/Giphy credentials
 
# 3. run azk start
 
$ azk start
```

Two of them use node, and the other two use Ruby, but you won't need them installed in your machine to run it. ☺ After that, you should see an output similar to this in your terminal:

![azk start output](https://d262ilb51hltx0.cloudfront.net/max/2000/1*ZG-hgOtsgxFzRB6PG2qR-w.png)

To access the project, just open the URLs you see in your terminal output. For the example above

- **Accessing [http://giphy-twilio-mms.dev.azk.io](http://giphy-twilio-mms.dev.azk.io/) will open the main application**, just like if you were running it locally by using `bundle exec rackup` and going to `localhost:4567`.
- **Accessing [http://giphy-twilio-mms-ngrok.dev.azk.io](http://giphy-twilio-mms-ngrok.dev.azk.io/) will take you to ngrok's web interface.**
- And finally, to access your application via ngrok, you just have to type whatever you set as the value inside your Azkfile.js NGROK_SUBDOMAIN variable, **for example http://giphy-twilio.ngrok.com.**

After that you can easily set up a webhook (SendGrid/Twilio/Twitter) by pointing it to your POST route and using ngrok's URL!

The steps I had to follow with the projects (and which you might use to add azk to your projects) were usually:

1. Running azk init to create an Azkfile.js
2. Opening Azkfile.js and making sure I had the correct version of the language/framework (for example, node:010)
3. Changing the project setup to use the environment variable HTTP_PORT instead of PORT.
4. Adding any extra systems, like Redis, or ngrok.

I found that this was a good way to easily set up a project, run it together with ngrok, and test out webhooks. What do you think? ☺

---
* This was originally posted on Medium first, [here](https://medium.com/@heitorburger/testing-webhooks-with-azk-and-ngrok-9f3700bad874).