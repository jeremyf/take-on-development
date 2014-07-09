# RSpec

## Documentation Format

## rspec-given

@TODO

## Custom matchers

### rspec-yenta

I like writing custom Rspec matchers.
Other people write custom Rspec matchers (e.g. [rspec-rails](https://github.com/rspec/rspec-rails) and [rspec-html-matchers](https://github.com/kucaahbe/rspec-html-matchers)).

A coworker of mine asked me how to find all of the matchers for one of our projects.
My answer was to create [`rspec-yenta`](https://github.com/jeremyf/rspec-yenta).

```console
$ rake -T yenta

rake yenta  # Find all of your rspec matchers and output them to STDOUT
```

Configure `rspec-yenta` for your project by following [`rspec-yenta`'s README](https://github.com/jeremyf/rspec-yenta#usage).
Then run `rake yenta`.

Below is a portion of output &mdash; albeit modified &mdash; from one of my projects.

```console
$ rake yenta

be            ./path/to/rspec-expectations/lib/rspec/matchers.rb:221
be_a          ./path/to/rspec-expectations/lib/rspec/matchers.rb:227
be_a_kind_of  ./path/to/rspec-expectations/lib/rspec/matchers.rb:253
be_a_new      ./path/to/rspec-rails/lib/rspec/rails/matchers/be_a_new.rb:73
```
