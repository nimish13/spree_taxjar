SpreeTaxjar
===========

Spree::Taxjar is a US sales tax extension for Spree using the Taxjar service.

Taxjar Configuration

Create an account with Taxjar (http://www.taxjar.com/) and get an api_key.

Go to Your Account >> States Setting, and create nexus for the relevant states in which you want/need to collect sales tax. (NOTE: Unless state's nexuses are explicitly created, Taxjar will return zero sales tax by default for orders shipping to those states.)

## Installation

1. Add this extension to your Gemfile with this line:
  ```ruby
  gem 'spree_taxjar', github: 'vinsol-spree-contrib/spree_taxjar', branch: '3-0-stable'
  ```

2. Install the gem using Bundler:
  ```ruby
  bundle install
  ```

3. Copy & run migrations
  ```ruby
  bundle exec rails g spree_taxjar:install
  ```

4. Restart your server

  If your server was running, restart it so that it can find the assets properly.

5. Go to admin end > Configurations > Taxjar Settings
  Add your taxjar api_key here.

## Testing

First bundle your dependencies, then run `rake`. `rake` will default to building the dummy app if it does not exist, then it will run specs. The dummy app can be regenerated by using `rake test_app`.

```shell
bundle
bundle exec rake
```

Credits
-------

[![vinsol.com: Ruby on Rails, iOS and Android developers](http://vinsol.com/vin_logo.png "Ruby on Rails, iOS and Android developers")](http://vinsol.com)

Copyright (c) 2016 [vinsol.com](http://vinsol.com "Ruby on Rails, iOS and Android developers"), released under the New MIT License

#Note

For better handling of exception raised by taxjar due to various validations add following code in your project's application_controller.rb

    rescue_from Taxjar::Error, with: :taxjar_rollback

    private
      def taxjar_rollback(e)
        flash[:error] = 'TaxJar::' + e.message
        redirect_to cart_path
      end

