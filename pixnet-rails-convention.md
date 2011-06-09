---
title: Pixnet Rails Convention
layout: post
---

### Environments

- Ruby Enterprise Edition <http://www.rubyenterpriseedition.com/>
- Rails 3.0.7
- Mysql
- Ubuntu 11.04 (Develop), Debian 6
- Editor: vim (with [rails.vim](https://github.com/tpope/vim-rails) plugin)

### Basic Naming Conventions

- [Ruby and Rails Naming Conventions](http://itsignals.cascadia.com.au/?p=7) from [IT.Signals](http://itsignals.cascadia.com.au/)
- [Ruby / Rails Convention of Techbang](https://gist.github.com/758319) from [xdite](http://blog.xdite.net/)


### Initial Rails App

- Clone <https://github.com/manic/rails3-app-template> and create rails project

    git clone git://github.com:manic/rails3-app-template.git
    rails new your_project_name -TJ -d mysql -m rails3-app-template/rails3.rb

### Annotate

    bundle exec annotate -p before #統一放在 model 上方
