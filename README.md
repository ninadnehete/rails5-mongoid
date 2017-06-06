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