#gems
**annotate[注解]**
```
gem 'annotate', '~> 2.7', '>= 2.7.1'
$ rails g annotate:install
```
**seedbank[seed分表]**
```
gem 'seedbank', '~> 0.4.0'
创建文件：db/seeds/development/modles.seeds.rb
puts "添加字段"
Member.create(:name => "马飞虎", :telphone => "14797478668", :age => "25")
或
Member.create(name： "马飞虎", telphone： "14797478668", age： "25")
执行命令：
rails db:send
```
**slim-rails[视图简化]** 
```
gem 'slim-rails', '~> 3.1', '>= 3.1.1'
```
**rails-i18n[中英文转化]**
```
gem 'rails-i18n', '~> 5.0', '>= 5.0.1'
config/application.rb
    config.i18n.load_path += Dir[Rails.root.join('config',  'locales', '**', '*.{rb,yml}')]
    config.i18n.available_locales = ['zh-CN', :en]
    config.i18n.default_locale = 'zh-CN'
创建文件config/locals/zh-CN.yml
zh-CN:
  activerecord:
    models:
      member:  "成员"
    attributes:
      member:
        name: 名字
        telphone: 手机号码
        age: 年龄
```
**livereload[自动刷新页面]**
```
gem 'rack-livereload', '~> 0.3.16'   and    'gem 'guard-livereload', '~> 2.5', '>= 2.5.2'
  初始化： guard init livereload
  config/environments/development.rb
  添加：
  config.middleware.insert_after ActionDispatch::Static, Rack::LiveReload
  bundle exec guard
```
**foreman[多服务器启动]**
```
gem 'foreman', '~> 0.82.0'
  在根目录创建Procfile文件
  web: bundle exec rails s
  $ foreman start
```
**pry-rails[错误调试]**
```
gem 'pry-rails', '~> 0.3.4'
bingding.pry
```
**pry-remote[多服务开启调试与foreman共用]**
```
gem 'pry-remote', '~> 0.1.8'
binding.remote_pry
根据提示：新开页面操作
```
**semantic-ui-sass[css 及js 框架]**
```
application.css.scss
修改文件：application.css为application.css.scss
添加：
  @import "semantic-ui";
application.js
  //= require semantic-ui
```
**rspec-rails[基本测试]**
```
gem 'rspec-rails', '~> 3.5'
rails generate rspec:install

重要操作

文件: spec/rails_helper.rb

去掉注释(23行): ...spec/support/**/*.rb..

第一个测试

生成模型

rails g model book name author price 

spec/models/book_spec.rb

require 'rails_helper'

RSpec.describe Book, type: :model do
  it "数据正确可以通过测试" do

    book = Book.new(
          name: 'xx',
          author: 'yy',
          price: 123
    )

    expect(book).to be_valid

  end
end

运行测试

bundle exec rspec
```
**Rspec[基本测试]**
```
安装

group :development, :test do
  gem 'rspec-rails', '~> 3.5'
end
guard-rspec(测试自动)
安装
group :development, :test do
  gem 'guard-rspec', '~> 4.7'
end

bundle exec guard init rspec

bundle exec guard
```


**shoulda-matchers[简化测试]**
```
安装

group :development, :test do
  gem 'shoulda-matchers', '~> 3.1'
end

新增文件 spec/support/shoulda_matchers.rb

# https://github.com/thoughtbot/shoulda-matchers#getting-started
RSpec.configure do |config|
  Shoulda::Matchers.configure do |config|
    config.integrate do |with|
      # test framework
      with.test_framework :rspec
      # libraries
      with.library :rails
    end
  end
end

结果显示格式(.rspec)
```





**fuubar[简化测试页面]**
```
--format documentation
gem 'fuubar', '~> 2.2'
.rspec
  --format Fuubar
```
