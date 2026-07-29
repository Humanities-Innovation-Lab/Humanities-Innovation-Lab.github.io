source "https://rubygems.org"

gem "jekyll", "~> 4.4.1"
# Needed to run `jekyll serve` on Ruby 3+ (webrick left Ruby's core library).
gem "webrick", "~> 1.8"

group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.17"
  gem "jekyll-seo-tag", "~> 2.8"
  gem "jekyll-sitemap", "~> 1.4"
end

# Windows and JRuby do not ship zoneinfo files.
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

# Speeds up directory watching on Windows.
gem "wdm", "~> 0.1", :platforms => [:mingw, :x64_mingw, :mswin]
