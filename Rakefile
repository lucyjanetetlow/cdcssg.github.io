require 'csv'
require 'html/proofer'

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

task :rebuild do
  sh "rm -rf _site"
  sh "bundle exec jekyll build"
end

task :htmlproofer => :rebuild do
  ignored = [
    "http://githubeditor.herokuapp.com"
  ]
  HTML::Proofer.new("./_site", 
    typhoeus: {ssl_verifypeer: false, timeout: 30}, 
    url_ignore: ignored, 
    check_html: true, 
    assume_extension: ".html",
    href_ignore: [/facebook.com/]).run
end

require 'rspec/core/rake_task'
RSpec::Core::RakeTask.new(:spec => :rebuild)

task :default => [:htmlproofer]