# README

## Overview
This project seeks to build a rails 5 app with the following specifications:
* mongoid gem for mongodb database
* devise and OmniAuth gems for user authentication and management


## Thanks

Success does not occur in a vacuum. Special thanks to the following individuals and tutorials that helped launch this project.

* **Tutorials**
	* [rails3-mongoid-devise](https://github.com/RailsApps/rails3-mongoid-devise) by
		* [The RailsApps team](https://github.com/RailsApps) [Daniel Kehoe](https://github.com/DanielKehoe) and [Taylor Mock](https://github.com/tmock12)
	* [rails-4-bootstrap-devise-cancan-omniauth](https://github.com/alex-klepa/rails4-bootstrap-devise-cancan-omniauth) by 
		* [Alex Klepa](https://github.com/alex-klepa)
* **Mentors**
	* [Ken Mazaika](https://github.com/kenmazaika)
	* [Conrad Taylor](https://github.com/conradwt)
	* [The Firehose Project](https://www.thefirehoseproject.com)

## Setup

### Intitialize new project

* Install rails 5: `gem install rails`
* Generate new rails app

```
$ rails new rails5-mongoid --skip-bundle --skip-active-record --skip-test --skip-system-test
```

**Explanation:**
  * The `$` will be used in this tutorial for the command prompt and is not to be typed.
  * `rails5-mongoid` is the name that I chose to call the app. You may specify a different name.
  * `--skip-bundle` We will be running `bundle install` after tweaking the gemfile
  * `--skip-active-record` Active record is for sql based databases, however we will be using the mongodb database.
  * `--skip-test` and `--skip-system-test`: We will have using rspec and cucumber for out tests.

### Source Control with Git
The following steps are to set up a git repository for source control. Skip this section if you are building a throw-away app for education. Of course, if you have an aversion to git, there are other version control options such as [Mercurial](https://www.mercurial-scm.org/) and [Subversion](http://subversion.apache.org/).
*`$ git init .`
* `$ git add .`
* `$ git commit -m 'Initial commit'`
* Create a remote repository. There are several options.
	* On GitHub. Here are [instructions](https://help.github.com/articles/create-a-repo/) if you need help. The README file is optional.
	* Follow steps [8 and 9](https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/) to push your local repository to GitHub.
	* **OR** you could use [BitBucket](https://bitbucket.org/) or one of the [many other](https://www.git-tower.com/blog/git-hosting-services-compared/) git hosting options

### Mongodb
* If Mongodb is not yet installed, follow the [installation guide](https://docs.mongodb.com/manual/administration/install-community/) to install it.
* Add the [mongoid gem](https://docs.mongodb.com/mongoid/master/tutorials/mongoid-installation/) to the Gemfile `gem 'mongoid', '~> 6.2.0'`
	* `$ bundle install`
	* Generate the configuration file `$ rails g mongoid:config`

### Add gems for testing
We will be using [Test Driven Developement](https://www.agilealliance.org/glossary/tdd/) in this app.

* Add and adjust the `Gemfile` to include the following gems.
	* [rspec-rails](https://rubygems.org/gems/rspec-rails) `gem 'rspec-rails', '~> 3.6'`
	* [capybara](https://rubygems.org/gems/capybara) `gem 'capybara', '~> 2.14'`
	* [database_cleaner](https://rubygems.org/gems/database_cleaner) `gem 'database_cleaner', '~> 1.6', '>= 1.6.1'`
	* [mongoid-rspec](https://github.com/mongoid-rspec/mongoid-rspec)`gem 'mongoid-rspec', git: 'https://github.com/mongoid-rspec/mongoid-rspec.git'`
		* Note at the time of writing the git master branch has been updated to include support for mongoid 6. However, the official release of 3.0.0 only supports through mongoid 5.
	* [cucumber-rails](https://rubygems.org/gems/cucumber-rails) `gem 'cucumber-rails', '~> 1.5'`
	* [factory_girl_rails](https://rubygems.org/gems/factory_girl_rails) `gem 'factory_girl_rails', '~> 4.8'`
	* [email_spec](https://rubygems.org/gems/email_spec/versions/2.1.0)`gem 'email_spec', '~> 2.1'`

The above gems will need to be grouped as follows in the Gemfile.

```
group :development, :test do
  # Call 'byebug' anywhere in the code to stop execution and get a debugger console
  gem 'byebug', platforms: [:mri, :mingw, :x64_mingw]
  gem 'rspec-rails', '~> 3.6'
  gem 'factory_girl_rails', '~> 4.8'
  gem 'cucumber-rails', '~> 1.5', :require => false
  gem 'database_cleaner', '~> 1.6', '>= 1.6.1'
end

group :test do
  gem 'capybara', '~> 2.14'
  gem 'mongoid-rspec', git: 'https://github.com/mongoid-rspec/mongoid-rspec.git'
  gem 'email_spec', '~> 2.1'
end
```
Run `$ bundle install` to install the new gems. Next we will configure these gems.

#### Rspec [Configuration](https://github.com/rspec/rspec-rails)
* `https://github.com/rspec/rspec-rails`
  * This generates several the necessary files to run rspec tests
* Add the following line to the top of the `.rspec` file
  * `--color`
  * This adds color output for when rspec is run from the terminal. We will be setting up Travis CI to run the tests automatically, however the --color option is
  nice for local debugging of tests which are run from the command line via `bundle exec rspec`.

#### FactoryGirl [Configuration](https://github.com/thoughtbot/factory_girl_rails)
* Add the file `/spec/factories.rb` with the following code.
  ```
  FactoryGirl.define do
    # factories will go here
  end
  ```

#### Cucumber [Configuration](https://cucumber.io/docs/reference/rails)
* Run the installation code `rails generate cucumber:install`
* Cucumber tests can be run from the command line with either of the following commands, however, we will be setting up Travis CI to run the tests automatically
  * `bundle exec cucumber`
  * `rake cucumber`

#### database_cleaner [Configuration](https://github.com/DatabaseCleaner/database_cleaner)
* This [Step by step guide](http://www.virtuouscode.com/2012/08/31/configuring-database_cleaner-with-rails-rspec-capybara-and-selenium/) is most helpful.
* Create a file called `spec/support/database_cleaner.rb` and add the following code

```ruby
RSpec.configure do |config|
  
  config.use_transactional_fixtures = false
 
  config.before(:suite) do
    DatabaseCleaner.clean_with(:truncation)
  end
 
  config.before(:each) do
    DatabaseCleaner.strategy = :transaction
  end
 
  config.before(:each, :js => true) do
    DatabaseCleaner.strategy = :truncation
  end
 
  config.before(:each) do
    DatabaseCleaner.start
  end
 
  config.after(:each) do
    DatabaseCleaner.clean
  end
end
```


