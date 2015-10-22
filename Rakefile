require 'nokogiri'
require 'curb'
require 'dotenv'
require 'active_support/all'

namespace :update do

  task :errors do
    `jekyll --no-auto`
    `cp _site/errors/404.html 404.html`
  end

end