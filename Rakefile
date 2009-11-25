task :default => :build

desc "Build my site, dammit!"
task :build => [ :projects, :contact ]

def build(page)
  yaml = YAML.load_file("pages/#{page}.yml")
  yaml["width"] = yaml[page.to_s].size * ((yaml['block-width'] || 260) + 32) + 4
  File.open("pages/#{page}.yml", "w") { |f| f.puts yaml.to_yaml + "---\n" }
  system "cat pages/#{page}.{yml,mustache} | mustache > #{page}.html"
end

task :projects do
  build :projects
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
  exec "kicker -e rake defunkt.css pages"
end
