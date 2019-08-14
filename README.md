## Welcomeページまで

- リポジトリをクローン
```git
git clone git@github.com:tanikento/rails6.0.0.rc1_on_docker.git
```

- 新規Railsアプリを作成
```docker
docker-compose run web rails new . --force --no-deps --database=postgresql
```

- database.yml を修正(./config/database.yml)
```yml
pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
host: <%= ENV.fetch('DATABASE_HOST') { 'localhost' } %>
port: <%= ENV.fetch('DATABASE_PORT') { 5432 } %>
username: <%= ENV.fetch('DATABASE_USER') { 'root' } %>
password: <%= ENV.fetch('DATABASE_PASSWORD') { 'root' } %>
```

- dockerイメージをビルド & up
```docker
docker-compose up -d --build
```

- DB作成
```docker
docker-compose run web rails db:create
```

- マイグレーション
```docker
docker-compose run web rails db:migrate
```


## scafold
- scafold
```ruby
rails g scafold
```

## Action Text
- ACtion Textをインストール
```ruby
rails action_text:install
```

- マイグレーション
```ruby
rails db:migrate
```


## リッチテキスト適応

- Model
```ruby
class Article < ApplicationRecord
    has_rich_text :content
end
```

- Controler
```ruby
def article_params
    params.require(:article).permit(:title, :content)
end
```

- View
```ruby
<div class="field">
    <%= form.label :content %>
    <%= form.rich_text_area :content %>
</div>
```
