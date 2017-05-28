---
layout: post
title: "Weather notification application"
date: 2017-05-27
permalink: /knowledge/:year/:month/:day/:title
section: "win"
---

Sometimes we get bored with checking notification section of our phone to see the weather changes. Comparatively speaking I'd prefer receiving text messages only when there is change that worth my attention. This is where my idea comes from.

At present, I only want the following features:
- Text me at certain time of day (e.g. 8 AM) about today's weather, temperature, recommendation of sun screen, rain gear, and other alerts
- Text me when there is a drastic change in weather.
- Huge plus: The weather information should be based on my current location.

## Getting weather data

- There is existing API to make use of. I just choose the first one - [OpenWeatherMap](https://openweathermap.org/api). From its description, I can get a all information I want using a free account. Good.
- Reqeusts to this API needs an appKey, so I created an account there. Maybe I need a *secret store* to save my username, password and appKey.
- Try a sample request, such as http://samples.openweathermap.org/data/2.5/weather?q=London,uk&appid=<my app key>. It works.
- Spend sometime reading through the API documentation. Easy step so skip it from here.

## Sending ans receiving SMS

- Thanks to those Python experts, I have found existing platforms that supports sending and receiving SMS, [Twilio](https://www.twilio.com/blog/2016/09/how-to-receive-and-respond-to-a-text-message-with-python-flask-and-twilio.html).

![Figure 1]({{ site.url }}/assets/send-receive-sms.png){:class="post-image"}

- In the Twilio blog post, [Flask](http://flask.pocoo.org/docs/0.12/quickstart/#a-minimal-application) is mentioned as a web framework to build web application.

- Also, [ngrok](https://ngrok.com/docs#getting-started) is mentioned, which allows you to expose a web server running on your local machine to the internet.

## Implement basic functionality

- With all the given tools and information, all we need to do for the first step is to build a single-thread web server that gets weather information, do simple analysis, and send SMS to user if necessary. Also we listen to user's request to update location information.

- Install Flask
    - I skipped installation of virtualenv, might regret for it later.
    - Received warning "A true SSLContext object is not available. This prevents urllib3 from configuring SSL appropriately and may cause certain SSL connections to fail".

- Run sample application
    - export FLASK_APP=<file name>.py
    - flask run
    - --host=0.0.0.0 parameter makes OS listen on all public IPs
    - export FLASK_DEBUG=1 makes debugging mode

- Get, parse and represent data

- Schedule job

- Redirect, reverse proxy

- SMS bond

- Create boundle, including dependency injection

## Run as a simple webservice on VM