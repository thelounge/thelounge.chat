---
layout: documentation
title: Heroku
---

This document will explain how to install The Lounge on Heroku. To learn more
about Heroku, read their
[documentation](https://devcenter.heroku.com/articles/getting-started-with-nodejs#introduction).

<div class="alert alert-warning" role="alert">
  <p>
    Please be aware that Heroku automatically kills unpaid apps after 1 hour of
    inactivity, and then spins them back up the next time a request comes in.
    This does not apply to paid accounts.
    If you scale up to two servers and pay for the second one, you get two
    always-on servers.
    <a href="https://devcenter.heroku.com/articles/dynos#dyno-sleeping">
      Read more
    </a>
  </p>

  <p>
    When Heroku kills The Lounge, you need to connect to servers and channels
    again from scratch.
    In practice, you get no always-on functionality with an unpaid Heroku
    account.
  </p>
</div>

## Login to the toolbelt

Begin by logging in to the [Heroku toolbelt](https://toolbelt.heroku.com/):

```
heroku login
```

## Build The Lounge

Clone the repository and install The Lounge from source:

```
git clone https://github.com/thelounge/thelounge
cd thelounge
yarn install
NODE_ENV=production yarn build
```

## Create the Heroku app

In the `thelounge/` directory, run:

```
heroku create
```

## Set up private mode (optional)

_This step is only useful if you want to run The Lounge with users accounts._

Create a `Procfile` and edit the content to look like this:

```
web: THELOUNGE_HOME=/app node index --private
```

_You can read more about Procfiles [here](https://devcenter.heroku.com/articles/procfile)._

To create users, run the following in the `thelounge/` directory:

```
THELOUNGE_HOME=. ./index.js add <username>
```

### Publish to Heroku

If you have made any changes to the repository (like adding users or the
Profile), save the changes with `git`:

```
git add .
git commit -m "Added Heroku files"
```

Then push it to Heroku:

```
git push heroku
```
