
## ruby, jekyll, bundle
[1]
```bash
sudo apt-get install ruby-full build-essential zlib1g-dev

# append to ~/.bashrc or ~/.zshrc
# Install Ruby Gems to ~/gems
export GEM_HOME="$HOME/gems"
export PATH="$HOME/gems/bin:$PATH"

source ~/.bashrc

gem install jekyll bundler
```

use `bundle exec jekyll` to draft/post/serve/...

## jekyll-plugin

## zsh, oh-my-zsh, powerlevl10k
```bash
sudo apt install zsh

sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

powerlevel10k-plugins


## ref
[1] [install-jekyll](https://jekyllrb.com/docs/installation/ubuntu/)