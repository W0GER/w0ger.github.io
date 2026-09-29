source "https://rubygems.org"

# The site is built by .github/workflows/deploy.yml, not the GitHub Pages
# builder, so the github-pages meta-gem isn't needed. Its version pins held
# back security fixes (e.g. rubyzip via jekyll-remote-theme 0.4.3).
gem "jekyll", "~> 3.10"
gem "kramdown-parser-gfm"
gem "minimal-mistakes-jekyll"
gem "webrick", "~> 1.9"
gem "uri", ">= 0.13.2"
# CVE fix: path traversal in rubyzip < 3.4.0 (Dependabot alert #41)
gem "rubyzip", ">= 3.4"

group :jekyll_plugins do
  gem "jekyll-remote-theme", "~> 0.6"
  gem "jekyll-github-metadata"
  gem "jekyll-paginate"
  gem "jekyll-sitemap"
  gem "jekyll-gist"
  gem "jekyll-feed"
  gem "jemoji"
  gem "jekyll-include-cache"
end
