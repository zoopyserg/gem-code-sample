# KeywordReplacer [![Build Status](https://app.travis-ci.com/DmytroHavryshGoTo/keyword_replacer.svg?branch=main)](https://app.travis-ci.com/DmytroHavryshGoTo/keyword_replacer)

This gem allows you to replace specified keywords with the links in the text.

## Problem description
Let's assume that there is a text(rich text or regular string) and you want to add links to specific words(links to store, faq, forum, etc.).

It'd be annoying to edit text each time when for example link is changed or you need another keyword. It's more convenient to have a list of keywords that should be replaced with a link. That is exactly what this gem does.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'keyword_replacer'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install keyword_replacer

## Usage

```ruby
class Post < ActiveRecord::Base
  replaces_links method_name: :transformed_text, source: :text, custom_class: 'custom',
                 max_matches: -> { 10 },
                 keywords: -> { ['keyword_1'] },
                 keywords_with_links: -> { { 'keyword_1' => 'https://google.com' } }
end
```

## Useful info
### Architecture of implemetation
There is a super handy pattern called `Module builder`
It has the following advantages:
- modules are just like any other objects—they can be created on the fly
- assigned to variables
- dynamically modified, as well as passed to or returned from methods

Example:

```ruby
  class SomeModule < Module
    def initialize(method_names)
      method_names.each do |name|
        define_method(name) do
          puts "#It's #{name} method"
        end
      end
    end
  end

  class Post
    include SomeModule.new(%i[foo bar])
  end
```

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/DmytroHavryshGoTo/keyword_replacer. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.

## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).

## Code of Conduct

Everyone interacting in the KeywordReplacer project’s codebases, issue trackers, chat rooms and mailing lists is expected to follow the [code of conduct](https://github.com/[USERNAME]/keyword_replacer/blob/master/CODE_OF_CONDUCT.md).
