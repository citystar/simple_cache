# What's Simple Cache?
Simple Cache is a library which caches the model objects and their associations. Any transaction onto the model objects will refresh the cache.

# Usage
Add this gem only!

## Install
Add this line to the Gemfile:

```
gem 'ar-simple-cache', github: 'begaborn/simple_cache'
```
Currently, SimpleCache supports Rails 4.2 or later. 


```
bundle install
```

# How it works 
Let's say there are two models as the following:
```ruby:user.rb
class User < ApplicationRecord
  has_many :players
end
``` 
```ruby:player.rb
class Player < ApplicationRecord
end
``` 

At first, the `players` objects, which are the `user` object's `has_many` associations, will be retrieved from the database when firstly being used like the following sample snippet. After that, the `players` objects will be stored into the cache server(Memcached) automatically.

From the second run, `players` will be retrieved from the cache server instead of the database.
```
User.take.players
```


<img width="643" alt="screen shot 2018-11-12 at 8 01 53 pm" src="https://user-images.githubusercontent.com/12689917/48343478-d4e44980-e6b5-11e8-90ad-b75e3356c9c9.png">


# Notes
1. If any option below is specified for `has_many` or `has_one`, the model objects will not be cached.
```
:class_name, :foreign_key, :dependent, :counter_cache, :auto_save, :extend
```

2. Only `has_one` and `has_many` are supported currently.

## Contributing
Bug reports and pull requests are welcome on GitHub at https://github.com/begaborn/simple_cache. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.

## License
The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).
