Build Status:
[![Build Status](https://travis-ci.org/ministryofjustice/govuk_elements_form_builder.svg)](https://travis-ci.org/ministryofjustice/govuk_elements_form_builder)

Code Climate: <a href="https://codeclimate.com/github/ministryofjustice/govuk_elements_form_builder"><img src="https://codeclimate.com/github/ministryofjustice/govuk_elements_form_builder/badges/gpa.svg" /></a> <a href="https://codeclimate.com/github/ministryofjustice/govuk_elements_form_builder/coverage"><img src="https://codeclimate.com/github/ministryofjustice/govuk_elements_form_builder/badges/coverage.svg" /></a>

# GovukElementsFormBuilder

To build GOV.UK based services you need to use the 
[govuk_frontend](https://github.com/alphagov/govuk_frontend). This can be loaded
via Webpacker.

This gem serves a form builder and other various helper methods to produces the
markup required to leverage presentation and interaction without having to
recreate the markup yourself.

## Documentation

Guidance and documentation for how to use this library can be found [here](https://govuk-elements-rails-guide.herokuapp.com/).

Any updates to the guidance should be submitted as pull requests to [this github repository](https://github.com/DFE-Digital/govuk_elements_rails_guide).

## Installation

### Step 1: Webpacker

You need to include the GovUK Frontend - this is easiest by using the NPM module via **Webpacker**.

See [Webpacker](https://github.com/rails/webpacker)

### Step 2: Add the GOV.UK Frontend

Next install the GOV.UK Frontend

```sh
yarn add govuk-frontend
```

You'll need to add this to the assets pipeline if your using Sprockets for
SCSS and Images - add the following to `config/initializers/assets.rb`

```ruby
# Add GOVUK image asset path
Rails.application.config.assets.paths << Rails.root.join("node_modules", "govuk-frontend", "assets", "images")

# Add GOVUK font asset path
Rails.application.config.assets.paths << Rails.root.join("node_modules", "govuk-frontend", "assets", "fonts")

Rails.application.config.assets.precompile += %w[
  favicon.ico
  govuk-mask-icon.svg
  govuk-apple-touch-icon-180x180.png
  govuk-apple-touch-icon-167x167.png
  govuk-apple-touch-icon-152x152.png
  govuk-apple-touch-icon.png
  govuk-opengraph-image.png
  govuk-logotype-crown.png
  govuk-crest-2x.png
]
```

And add the GOV.UK Frontend to the `app/javascript/packs/application.js`

```javascript
import { initAll } from "govuk-frontend";

initAll();
```

### Step 3: Add the form builder

Add these lines to your application's Gemfile, form builder is the last gem in list:

```ruby
gem 'govuk_frontend_form_builder', '~>2.0.0'
```

And then execute:

```sh
bundle
```

## Usage

In your application's `config/application.rb` file, configure the form builder
to be the default like this:

```rb
  class Application < Rails::Application
    # ...
    ActionView::Base.default_form_builder = GovukFrontendFormBuilder::FormBuilder
  end
```

You can see a visual guide to
[using the form builder](https://govuk-elements-rails-guide.herokuapp.com/)
here: https://govuk-elements-rails-guide.herokuapp.com/


## Versions - Which version should you used?

We encourage developers to use the latest version but understand that sometimes
it is not possible to do so. Seeing as there was quite a significant change
to the markup needed with the release of GOVUK Elements 3.0. We have decided to
create two supporting versions of the form builder for those services that use
the older GOVUK Elements and Frontend toolkit or who would like to use the
latest GOVUK assets.

Since version 1, GOVUK Elements and Frontend versions have now become a dependency
to help ensure that developers use the correct GOVUK Form builder version.

 For the time being the only differences between the two versions is the markup
  that this gem produces. We will try and keep the methods identical between versions
  but if you decide to upgrade to version 1 you should check any pages that use
  Radio buttons or Checkboxes and any js/css that rely on the markup these two
  elements use. Another thing you should check is if you rely on the
  css class name used for errors as this has also been renamed.

## Development

After checking out the repo, run `bundle install` to install dependencies.
Then, run `bundle exec rspec` to run the tests.

To install this gem onto your local machine, run `bundle exec rake install`.
To release a new version, update the version number in `version.rb`, and then
run `bundle exec rake release`, which will create a git tag for the version,
push git commits and tags, and push the `.gem` file to
[rubygems.org](https://rubygems.org).



## Contributing

Bug reports and pull requests are welcome on GitHub at
https://github.com/DFE-Digital/govuk_frontend_form_builder. This project is
intended to be a safe, welcoming space for collaboration, and contributors are
expected to adhere to the [Contributor Covenant](contributor-covenant.org)
code of conduct.


## License

The gem is available as open source under the terms of
the [MIT License](http://opensource.org/licenses/MIT).
