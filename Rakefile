require 'nokogiri'
require 'curb'
require 'dotenv'
require 'active_support/all'

namespace :update do

  task :errors do
    `jekyll --no-auto`
    `cp _site/errors/404.html 404.html`
  end

  task :fundraisers do
    output = File.open('_includes/fundraisers.html', 'w')
    Dotenv.load
    uri = "https://api.justgiving.com/#{ENV['JUSTGIVING_API_KEY']}/v1/fundraising/search?charityId=#{ENV['JUSTGIVING_CHARITY_ID']}"
    http = Curl.get(uri)
    xml = Nokogiri::XML.parse(http.body_str)
    xml.xpath('//Fundraiser').each do |fundraiser|
      date = Date.parse(fundraiser.xpath('EventDate').text) rescue nil
      created = Date.parse(fundraiser.xpath('CreatedDate').text) rescue nil
      active = fundraiser.xpath('Status').text == "Active"
      url = 'http://' + fundraiser.xpath('PageUrl').text
      owner = fundraiser.xpath('PageOwner').text
      event = fundraiser.xpath('EventName').text
      if active && date >= 3.months.ago
        puts [owner, event, date].inspect
        output << "<dt><a href='#{url}'>#{owner}</a></dt>\n"
        output << "<dd>#{(event)}"
        if date
          output << " on #{date.to_formatted_s(:long_ordinal)}"
        end
        output << "</dd>\n"
      end
    end
  end

end


# <Fundraiser>
#   <EventDate>2010-01-26T00:00:00</EventDate>
#   <EventId>355753</EventId>
#   <EventName>Supporting Public Health IT's fundraising</EventName>
#   <PageName>Solutions for Public Health's page</PageName>
#   <PageOwner>Supporting Public Health IT</PageOwner>
#   <PageUrl>www.justgiving.com/Supporting-Public-Health-IT</PageUrl>
#   <PercentageTargetAchieved>0</PercentageTargetAchieved>
#   <Photo>www.justgiving.com/Utils/imaging.ashx?img=Stock/liquorice.jpg</Photo>
#   <Status>Active</Status>
#   <TargetAmount>0.0000</TargetAmount>
#   <TeamMembers/>
# </Fundraiser>
