require "bundler/setup"

task :default => :sync

desc "Downloads all libraries from ajax.googleapis.com that are listed in libraries.txt"
task :sync do
  File.foreach("libraries.txt") do |url|
    download(url)
  end
end

def download(url)
  url, path = url_and_path(url)
  return unless url
  dir = File.dirname(path)
  FileUtils.mkdir_p(dir)
  if File.exists?(path)
    puts "#{path} already exists"
  else
    sh("curl '#{url}' > '#{path}'")
  end
end

def url_and_path(url)
  return if url.nil? || url.strip.empty?
  url.strip!
  path = url.gsub("http://#{HOSTNAME}/", "")
  [url, path]
end
