---
layout: single
title: "Projects"
---
## [Whodat](https://github.com/bperlik/whodat){:target="_blank"} ##

A quick, easy Ruby Gem that adds very simple users and sessions to your Rails app, removing the task of long set up of more complex user gems during development. I used a Rails engine and BCrypt. It's very simple to add to a Rails project and have a user to start development right away. It's an open source project, so contributions are desired and welcomed!


## [Blocipedia](https://blocipedia-bperlik.herokuapp.com/){:target="_blank"} ##

A social, markdown wiki app that lets users create their own wikis and share them publicly or privately with other collaborators. Its built on Ruby on Rails, using Bootstrap, SQLite (for testing and development) and PostgreSQL (for production). I used Devise for user authentication, SendGrid for email confirmation, Pundit for authorization, and Stripe for payments.

### Features: ###
* Users can create a standard account in order to create, edit, and collaborate on public wikis using Markdown syntax. Anyone can view public wikis.
* Users can pay to upgrade their account to Premium in order to view and create private wikis.
* Premium users can allow others to view and collaborate on the private wikis they create.
* Premium users can downgrade their account back to Standard.
* When a user downgrades his or her account, his or her private wikis will automatically become public.

