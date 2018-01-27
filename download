#!/usr/bin/env ruby
# frozen_string_literal: true

require 'koala'
require 'yaml'
require 'logger'

logger = Logger.new(STDOUT)

oauth = Koala::Facebook::OAuth.new(ENV['APP_ID'], ENV['APP_SECRET'])

logger.info('Getting application access token...')
graph = Koala::Facebook::API.new(oauth.get_app_access_token)

fields = %w[
  message
  link
  from
  type
  picture
  created_time
  updated_time
  name
  permalink_url
  place
  shares
  comments.limit(10000)
  reactions.limit(10000)
  attachments.limit(1000)
]

options = {
  limit: 100, # Facebook doesn't allow more than 100
  fields: fields
}

logger.info('Requesting first page of posts...')
posts = graph.get_connections(ENV['GROUP_ID'], 'feed', options)
page = 0

# Iterate on posts pages until we hit the end
until posts.empty?

  page += 1
  logger.info("Writing page ##{page}...")

  posts.each do |post|
    file_name = 'posts/' + post['id'] + '.yml'
    File.write(file_name, post.to_yaml)
  end

  posts = posts.next_page
end
