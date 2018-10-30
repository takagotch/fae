### fae
---
https://github.com/wearefine/fae

```sh
gem 'fae-rails'
rails g fae:install

gem install rails -v '~> 5.0.0'
gem 'fae-rails'
rails g fae:install
rails g fae:scaffold ArticleCategory name:string position:integer
rails g fae: scaffold Article title:string slug:string introduction:text body:text date:date hero_image:image pdf:file article_category:references
rails g fae:page AboutUs hero_image:image headline:string body:text
rails db:migrate


```

```ruby
validates :title, presence: true
validates :slug, Fae.validation_helpers.slug

Judge.configure do
  expose Article, :slug
end

# app/models/concerns/fae/navigation_concern.rb
def structure
  [
    item('News', subitems: [
      item('Articles', path: admin_articles_path),
      item('Article Categories', path: admin_article_categories_path)
    ]),
    item('Pages', subitems: [
      item('About Us', path: fae.edit_content_block_path('about_us'))
    ])
  ]
end


```

```
main.content
  = fae_input f, title
  = fae_input f, :slug
  = fae_input f, :introduction
  = fae_input f, :body
  = fae_input f, :date
  = fae_association f, :article_category
  = fae_image_form f, :hero_image
  = fae_file_form f, :pdf
  
= fae_input f, :title, input_class: 'slugger'

= fae_input f, :body, markdown: true

fae_datepicker f, :date


```



