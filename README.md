P2K (Pocket to Kindle)
===
**P2K (Pocket to Kindle)** is a Rails application that sends articles from your Pocket to Kindle e-reader.

**Currently served at** http://p2k.co

**Author:** Emir Aydin - http://emiraydin.com

## Setup Instructions

To make this application work, you'll need 3 more files that I couldn't put in this repo since either they contain sensitive infomation or they were a 3rd party program that was too large.

### 1. config/application.yml

This file stores all your application passwords and constants. Get your Pocket API key here: http://getpocket.com/developer/

Create a file named `application.yml` inside `/config` folder. It should look something like this:

```
# config/application.yml
# This file stores all the application constants

defaults: &defaults
  POCKET_CONSUMER_KEY: "00000-somehash"
  DELIVERY_EMAIL_SMTP: "smtp.mymailprovider.com"
  DELIVERY_EMAIL_PORT: portnumber
  DELIVERY_EMAIL_ADDRESS: "delivery@myapp.com"
  DELIVERY_EMAIL_PASSWORD: "passfor-delivery@myapp"

development:
  <<: *defaults
  APP_PATH: "http://localhost:3000"
  POCKET_REDIRECT_URI: "http://localhost:3000/welcome/home"
  DATABASE_HOST: "localhost"
  DATABASE_USERNAME: "my-db-username"
  DATABASE_PASSWORD: "my-db-password"

test:
  <<: *defaults
  DATABASE_HOST: "localhost"
  DATABASE_USERNAME: "my-test-username"
  DATABASE_PASSWORD: "my-test-password"

production:
  <<: *defaults
  APP_PATH: "http://myapp.com"
  POCKET_REDIRECT_URI: "http://myapp.com/welcome/home"
  DATABASE_HOST: "SOME IP"
  DATABASE_USERNAME: "my-db-username"
  DATABASE_PASSWORD: "my-db-password"
```

### 2. config/secrets.yml
This file contains application secrets for all your Rails environments. You can generate them using `rake secret` command.

```
development:
  secret_key_base: PUT-SOME-HASH-HERE

test:
  secret_key_base: PUT-SOME-HASH-HERE

# Do not keep production secrets in the repository,
# instead read values from the environment.
production:
  secret_key_base: <%= ENV["SECRET_KEY_BASE"] %>
```

### 3. Kindlegen application
We need Kindlegen application to parse our ebook into MOBI format, which will then be delivered to the users. You can download it here: http://www.amazon.com/gp/feature.html?docId=1000765211

Once downloaded, make sure to add the directory you put this file in is located in your PATH.

### P.S. Cron jobs for deliveries
This application uses [whenever] (https://github.com/javan/whenever) gem to run cron jobs for deliveries.
You need to run the command `whenever -i` inside your application directory in order to update your crontab file and start deliveries.

License
===
<a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/">Creative Commons Attribution-NonCommercial 4.0 International License</a>.
