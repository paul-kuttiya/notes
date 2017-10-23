## Rspec 101  
* ensure gem `bundler` is installed  

* create file `Gemfile`  
```ruby
source 'http://rubygems.org'
ruby '2.2.7'

gem 'rspec'
```
~> run `bundle install`  

* run command `bundle exec rspec --init`  
~> will generate `.rspec` and `spec_helper.rb`  
```text
// .rspec
--color
--require spec_helper
```

* Create test file in `spec/testname_spec.rb`  
~> `require_relative '../filename'`  

### Rspec basic  
* describe something for testing  
~> can be `class`  

* use `context` to group similar test behavior  

* use `it` to specify what to test for  

* use `let` block to pre-defined reusable variable for the same `context`  

* use `before` block to pre-defined reusable behavior which will run for all `it` in the same context 
