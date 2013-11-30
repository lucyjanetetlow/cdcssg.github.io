require 'nokogiri'
require 'open-uri'

namespace :update do

  task :errors do
    `jekyll --no-auto`
    `cp _site/errors/404.html 404.html`
  end

  task :fundraisers do
    output = File.open('_includes/fundraisers.html', 'w')
    list = Nokogiri::HTML(open('http://www.justgiving.com/criduchat/friend-search?q=&s=CharitySpecific&p=1'))
    list.css('a.img_thumb').each do |link|
      url = 'http://www.justgiving.com' + link['href']
      puts url
      page = Nokogiri::HTML(open(url))
      owner = page.css('div#fundraising-panel figcaption a').first
      event = page.css('.event').first
      output << "<dt><a href='#{url}'>#{owner.content || ''}</a></dt>\n"
      output << "<dd>#{(event ? event.content : '').gsub("Event:", '').gsub(/\s/, ' ').strip.squeeze(' ')}</dd>\n"
    end
    output.close
  end
  
end