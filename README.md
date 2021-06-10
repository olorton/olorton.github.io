# Oliver Lorton's blog

## Dev setup

Check that you have the homebrew version of Ruby:

    $ which ruby
    /usr/local/opt/ruby/bin/ruby

And that you have version 3 or later:

    ruby -v
    ruby 3.0.0p0 (2020-12-25 revision 95aff21468) [x86_64-darwin18]

Install Jekyll and bundler gems:

    gem install jekyll bundler && bundle install

Run local Jekyll server with live reload:

    bundle exec jekyll serve --livereload
