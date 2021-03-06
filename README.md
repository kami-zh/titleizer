# Titleizer

[![Build Status](https://travis-ci.org/kami30k/titleizer.svg)](https://travis-ci.org/kami30k/titleizer)
[![Gem Version](https://badge.fury.io/rb/titleizer.svg)](http://badge.fury.io/rb/titleizer)

Titleizer sets page title to Rails application using I18n.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'titleizer'
```

And then execute:

```
$ bundle
```

## Usage

### Basic usage

#### 1. Add to locales

Add page titles to your `config/locales/*.yml`:

```yaml
en:
  title:
    application: My Blog
    description: This is my blog.
    posts:
      index: All posts
      show: "%{subject}"
      new: New post
      edit: Edit post
```

#### 2. Modify title tag

Modify title tag in `app/views/layouts/application.html.erb`:

```erb
<!DOCTYPE html>
<html>
  <head>
    <title><%= title(yield :title) %></title>
        :
  </head>
```

You should restart your application after changing locales file.
Then you will see the page title as you set.

### Optional usage

#### Title with variable

If you want to set page title using variable, you can set `@title_params` in your action:

```ruby
class PostsController < ApplicationController
  def show
    @post = Post.find(params[:id])

    @title_params = { subject: @post.subject }
  end
end
```

When `@post.subject` is "My first post", `posts#show` title is as follows:

```erb
<!DOCTYPE html>
<html>
  <head>
    <title>My first post | My Blog</title>
        :
  </head>
```

#### Override title

If you want to override page title, you can set preferred title on view file.
This feature is useful in some case, such as rendering error page.

For example, if you set view file as follows, the page title become `404 Not Found | My Blog` even if you set title in locales.

```erb
<% provide :title, '404 Not Found' %>
```

## Contributing

1. Fork it ( https://github.com/kami30k/titleizer/fork )
2. Create your feature branch (git checkout -b my-new-feature)
3. Commit your changes (git commit -am 'Add some feature')
4. Push to the branch (git push origin my-new-feature)
5. Create a new Pull Request
