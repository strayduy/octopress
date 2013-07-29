---
layout: post
title: "Hosted on Heroku"
date: 2012-08-26 00:00
comments: true
categories: under-the-hood heroku jekyll
---

This blog is hosted on [Heroku](http://www.heroku.com/), a cloud application platform.

### Platform as a Service

Heroku, like [other](https://developers.google.com/appengine/) [cloud platforms](https://openshift.redhat.com/app/), employs a hosting model known as [Platform as a Service (PaaS)](http://www.salesforce.com/paas/). Instead of providing you with raw servers that you would otherwise have to configure yourself, these platforms manage the underlying application environment for you. All you have to worry about is building the application itself.

For those of us not interested or qualified to play [sysadmin](http://en.wikipedia.org/wiki/System_administrator), the PaaS model spares you the responsibility of having to configure an entire web stack or maintain a server cluster. You can focus on what I consider to be the fun part: writing application code.

### A Few Neat Things About Heroku

#### Basic usage is free

[Heroku's pricing model](https://heroku.com/pricing) is based on the computation-hours that your application consumes. You allocate one or more [dynos](https://devcenter.heroku.com/articles/dynos) (process containers) to execute your code, with additional dynos providing more concurrency at a proportional cost.

Heroku spots you a [free dyno](https://devcenter.heroku.com/categories/billing), though. This is probably enough processing power for most low-traffic sites.

#### Scaling is (probably) easy

If you find yourself in the enviable position of requiring more horsepower than the freebie dyno can provide, you can allocate more dynos for your application with [a single command](https://devcenter.heroku.com/articles/scaling#scaling):

``` bash
# Allocate two web dynos
heroku ps:scale web=2

# Allocate two *additional* web dynos
heroku ps:scale web+2
```

Disclaimer: I haven't had the need to scale beyond my one dyno, so I'm just going off of [Heroku's documentation](https://devcenter.heroku.com/articles/scaling) here.

#### Deployment is definitely easy

Heroku [stores your application code in a remote git repository](https://devcenter.heroku.com/articles/git). To deploy changes into production, you simply push commits to that repo.

As an example, [here's how I posted this entry to the site](https://github.com/strayduy/strayharbor-blog/commit/9a366e46cb5ba9909d66bc1393d572d6a537b890): <!-- Pretty meta, right? -->

``` bash
git add _posts/2012-08-26-hosted-on-heroku.md
git commit -m "New post about hosting the site on Heroku"
git push heroku master
```

And if you're already using [git for version control](http://git-scm.com/), then there's not much overhead to deploying to Heroku, following the initial setup.

#### Language options

Heroku supports [a bunch of languages](https://devcenter.heroku.com/articles/cedar#polyglot-platform), like [Ruby](http://devcenter.heroku.com/articles/ruby), [Python](http://devcenter.heroku.com/articles/python), and [Java](http://devcenter.heroku.com/articles/java), as well as frameworks like [Rails](http://devcenter.heroku.com/articles/rails3), [Django](http://devcenter.heroku.com/articles/django), and [Node](http://devcenter.heroku.com/articles/nodejs).

### Deploying Jekyll to Heroku

I discussed [Jekyll](https://github.com/mojombo/jekyll/) in my [previous post](/2012/08/15/generated-by-jekyll/). Here are two guides for deploying a Jekyll site to Heroku:

* [Run Your Jekyll Site On Heroku](http://mwmanning.com/2011/11/29/Run-Your-Jekyll-Site-On-Heroku.html)
* [Deploying Jekyll sites to Heroku with Rack-Jekyll](http://mikemayo.org/2012/deploying-jekyll-sites-to-heroku-with-rack-jekyll/)
