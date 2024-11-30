# frozen_string_literal: true

source "https://rubygems.org"

gem "jekyll", "~> 4.3"
gem "webrick", "~> 1.9" # Necessário para rodar o Jekyll localmente
gem "nokogiri"          # Usado para parsing XML/HTML (certifique-se de que é necessário)

# Plugins personalizados
gem "jekyll-last-modified-at", git: "https://github.com/maximevaillancourt/jekyll-last-modified-at", branch: "add-support-for-files-in-git-submodules"
gem "jekyll-note-link"

# Plugins para o GitHub Pages
group :jekyll_plugins do
  gem "github-pages"
end
