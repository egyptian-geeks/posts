# Posts

A repository that includes all EgyptianGeeks group posts.

## Purpose

The purpose of this repository is to have the graph API dump for EgyptianGeeks
group without any post-processing, also the `download` script can run on any
group specified in the environment file `.env`, so a fork can be done for any
other group.

## Content

* posts/ : all posts in YAML format, dumped from facebook graph API
* download : a ruby script that download group posts to `posts/`


## Requirements

* Ruby 2.5.0
* Facebook application

## Installation

* Install dependencies

  ```shell
  bundle install
  ```
* Create a facebook application
* Copy `.env.sample` to `.env`

  ```shell
  cp .env.sample .env
  ```
* Set variables values in `.env`
* Execute `download` at well

  ```shell
  ./download
  ```

## How it works

* `download` will use your application id and secret to acquire application
  access token
* the application access token will be used to get all posts in the group
  specified in `.env`
* the script will get posts in batches of 100 post per page, with all likes and
  comments
* for each post a file will be writen with the post object converted to YAML,
  file name is the post ID

## Updating `posts` Directory

* fork this repository
* clone it to your machine
* create a branch
* run `download` script
* keep it running for couple pages then kill it
* commit all new posts
* open a PR with your update

## Using this download script for other groups

* Fork this repository
* Delete all files in `posts`

  ```shell
  rm posts/*
  ```
* Put your group ID in `.env`
* Run `download` script
* Commit all your posts

  ```shell
  git add posts/
  git commit -m"group posts for <your group name>"
  git push origin master
  ```
* To update the script in case you want to be up to date, create a branch in you
  repo pointing to this repo master, pull it and cherry-pick the commit you want
  to your branch.
