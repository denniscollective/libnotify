require 'rake'
require 'rake/rdoctask'
require 'rubygems'

begin
  require 'jeweler'
  Jeweler::Tasks.new do |gem|
    gem.name = "libnotify"
    gem.summary = 'Ruby bindings for libnotify using FFI'
    gem.email = "peter-libnotify@suschlik.de"
    gem.homepage = "http://github.com/splattael/libnotify"
    gem.authors = ["Peter Suschlik"]

    gem.has_rdoc = true
    gem.extra_rdoc_files = [ "README.rdoc" ]

    gem.add_dependency "ffi", ">= 0.6.2"

    gem.add_development_dependency "riot", "= 0.11.2"
    gem.add_development_dependency "riot_notifier"
    gem.add_development_dependency "yard"

    gem.test_files = Dir.glob('test/test_*.rb')
  end
  Jeweler::GemcutterTasks.new
rescue LoadError
  puts "Jeweler (or a dependency) not available. Install it with: gem install jeweler"
end

# Test
require 'rake/testtask'
desc 'Default: run unit tests.'
task :default => :test
task :test => :check_dependencies

Rake::TestTask.new(:test) do |test|
  test.test_files = FileList.new('test/test_*.rb')
  test.libs << 'test'
  test.verbose = true
end

# Yard
begin
  require 'yard'
  YARD::Rake::YardocTask.new
rescue LoadError
  task :yardoc do
    abort "YARD is not available. In order to run yardoc, you must: sudo gem install yard"
  end
end

desc "Alias for `rake yard`"
task :doc => :yard

# Misc
desc "Tag files for vim"
task :ctags do
  dirs = $LOAD_PATH.select {|path| File.directory?(path) }
  system "ctags -R #{dirs.join(" ")}"
end

desc "Find whitespace at line ends"
task :eol do
  system "grep -nrE ' +$' *"
end

desc "Display TODOs"
task :todo do
  `grep -Inr TODO lib test`.each do |line|
    line.scan(/^(.*?:.*?):\s*#\s*TODO\s*(.*)$/) do |(file, todo)|
      puts "* #{todo} (#{file})"
    end
  end
end
