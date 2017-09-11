require 'html-proofer'

Encoding.default_external = Encoding::UTF_8
Encoding.default_internal = Encoding::UTF_8

options = { 
	:check_html => true,
	:assume_extension => true, 
	:allow_hash_href => true,
	:url_ignore => [/localhost/,
	/https\:\/\/www.linkedin.com\/company\/eclipse-foundation/]
}

task :default => ["test"]

desc "cleans the output directory"
task :clean do
  sh "bundle exec jekyll clean"
end

desc "build site"
task :build => [:clean] do
  sh "bundle exec jekyll build"
end
 
desc "serve site"
task :serve => [:clean] do
  sh "bundle exec jekyll serve"
end

desc "serve incremental"
task :incremental => [:clean] do
  sh "bundle exec jekyll serve --incremental"
end

desc "test production build"
task :test => ["build"] do
  HTMLProofer.check_directory("./_site", options).run
end
