On Mac, you can run:

```ruby
brew update
brew install ruby

# If you use bash
echo 'export PATH=/usr/local/Cellar/ruby/2.4.1_1/bin:$PATH' >> ~/.bash_profile 

# If you use ZSH:
echo 'export PATH=/usr/local/Cellar/ruby/2.4.1_1/bin:$PATH' >> ~/.zprofile
```

However, I suggest using an Environment Manager for Ruby.

You have [rbenv](https://github.com/rbenv/rbenv) and [RVM](https://rvm.io/). IMO go for rbenv:

```ruby
brew install rbenv ruby-build

# bash
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile
echo 'eval "$(rbenv init -)"' >> ~/.bash_profile  

# zsh
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.zprofile
echo 'eval "$(rbenv init -)"' >> ~/.zprofile  

# list all available versions:
rbenv install -l

# install a Ruby version:
rbenv install 2.4.1

# set ruby version for a specific dir
rbenv local 2.4.1

# set ruby version globally
rbenv global 2.4.1

rbenv rehash
gem update --system
```

#### Downgrading Ruby Version
```ruby
brew install rbenv/tap/openssl@1.0

rvm install 2.2.10 -C --with-openssl-dir=`brew --prefix openssl@1.0`

ruby
export optflags="-Wno-error=implicit-function-declaration"
```