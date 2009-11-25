task :default => :build

desc "Build my site, dammit!"
task :build do
  require 'yaml'
  yaml = YAML.load_file('projects/data.yml')
  yaml['width'] = yaml['projects'].size * (260 + 32) + 4
  File.open('projects/data.yml', 'w') { |f| f.puts yaml.to_yaml + "---\n" }
  exec "cat projects/data.yml projects/template.mustache | mustache > projects.html"
end
