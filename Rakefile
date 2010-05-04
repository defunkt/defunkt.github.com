task :default => :build

desc "Build my site, dammit!"
task :build => [ :index, :contact, :talks, :about ]

def build(page)
  require 'yaml'
  yaml = YAML.load_file("pages/#{page}.yml")
  yaml["width"] = yaml[page.to_s].size * ((yaml['block-width'] || 260) + 32) + 4
  File.open("pages/#{page}.yml", "w") { |f| f.puts yaml.to_yaml + "---\n" }
  system "cat pages/#{page}.{yml,mustache} | mustache > #{page}.html"
end

task :index do
  require 'yaml'
  require 'rdiscount'
  data = YAML.dump('yield' => Markdown.new(File.read('index.md')).to_html)

  File.open('data.yml', 'w') do |f|
    f.puts data
    f.puts "---"
  end

  exec "cat data.yml index.mustache | mustache > index.html"
end

task :about do
  build :about
end

task :talks do
  build :talks
end

task :contact do
  build :contact
end

desc "Publish the site."
task :publish => :build do
  system "git commit -a -m publish"
  exec "git push origin master"
end

desc "Kick it!"
task :kicker do
  exec "kicker --no-growl -e rake css/defunkt.css pages index.md"
end
