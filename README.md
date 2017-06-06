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
  * `--skip-bundle`: We will be running `bundle install` after tweaking the gemfile
  * `--skip-active-record`: Active record is for sql based databases, however we will be using the mongodb database.
  * `--skip-test` and `--skip-system-test`: We will have using rspec and cucumber for out tests.

## Source Control with Git
The following steps are to set up a git repository for source control. Skip this section if you are building a throw-away app for education. Of course, if you have an aversion to git, there are other version control options such as [Mercurial](https://www.mercurial-scm.org/) and [Subversion](http://subversion.apache.org/).
*`$ git init .`
* `$ git add .`
* `$ git commit -m 'Initial commit'`
* Create a remote repository. There are several options.
	* On GitHub. Here are [instructions](https://help.github.com/articles/create-a-repo/) if you need help. The README file is optional.
	* Follow steps [8 and 9](https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/) to push your local repository to GitHub.
	**OR** you could use [BitBucket](https://bitbucket.org/) or one of the [many other](https://www.git-tower.com/blog/git-hosting-services-compared/) git hosting options


### Mongodb
* If Mongodb is not yet installed, follow the [installation guide](https://docs.mongodb.com/manual/administration/install-community/) to install it.
* Add the [mongoid gem](https://docs.mongodb.com/mongoid/master/tutorials/mongoid-installation/) to the Gemfile `gem 'mongoid', '~> 6.1.0'`
* Generate the configuration file `$ rails g mongoid:config`

