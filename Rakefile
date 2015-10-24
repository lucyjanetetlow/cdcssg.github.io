require 'nokogiri'
require 'curb'
require 'dotenv'
require 'active_support/all'
require 'csv'

namespace :update do

  task :errors do
    `jekyll --no-auto`
    `cp _site/errors/404.html 404.html`
  end

  task :locations, [:filename] do |task, args|
    CSV.open("_data/locations.csv", "wb") do |output|
      output << ['postcode','latitude','longitude']
      CSV.foreach(args[:filename]) do |row|
        incode = row[0]
        unless incode.blank?
          sleep(2)
          uri = URI.parse("http://mapit.mysociety.org/postcode/partial/#{incode}")
          data = JSON.parse(Net::HTTP.get(uri))
          if data["wgs84_lat"] && data["wgs84_lon"]
            output << [incode, data["wgs84_lat"], data["wgs84_lon"]]
          end
        end
      end
    end
  end

end