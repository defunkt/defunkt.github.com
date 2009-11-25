task :default => :build

desc "Build my site, dammit!"
task :build => [ :projects, :contact ]

def build(page)
  yaml = YAML.load_file('projects/data.yml')
  yaml['width'] = yaml['projects'].size * (260 + 32) + 4
  File.open('projects/data.yml', 'w') { |f| f.puts yaml.to_yaml + "---\n" }
  system "cat projects/data.yml projects/template.mustache | mustache> projects.html"
end

task :projects do
  require 'yaml'
end

task :contact do
  require 'yaml'
  yaml = YAML.load_file('contact/data.yml')
  yaml['width'] = yaml['contact'].size * (260 + 32) + 4
  File.open('contact/data.yml', 'w') { |f| f.puts yaml.to_yaml + "---\n" }
  system "cat contact/data.yml contact/template.mustache | mustache > contact.html"
end
