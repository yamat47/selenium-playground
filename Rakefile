require 'debug'
require 'selenium-webdriver'
require 'webdrivers'

desc 'Run browser automation using selenium.'
task :selenium do
  offices = []

  driver = Selenium::WebDriver.for :chrome

  driver.get 'https://www.j-lis.go.jp/spd/code-address/jititai-code.html'

  # それぞれの都道府県のページへのリンク。
  driver.find_elements(tag_name: 'table.listtbl tr a').take(47).map do |link|
    link.attribute('href')
  end.each do |href|
    driver.get(href)

    prefecture_name = driver.find_element(tag_name: 'h1').text.delete_suffix('内市町村')
    driver.find_elements(tag_name: 'table tr:not(:first-child)').each do |tr|
      offices << "#{prefecture_name}#{tr.find_elements(tag_name: 'td')[4].text}"
    end
  end

  driver.quit

  puts offices
end

task default: :selenium
