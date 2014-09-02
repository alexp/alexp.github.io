---
  layout: post
  title: Devise + Rails 4.2.0-beta1 - fixing undefined method 'mege!' 
---

If you have just upgraded your Devise based app to Rails 4.2.0-beta1 version, you probabily encountered the following error:

<code>
/Users/aps/.rvm/gems/ruby-2.0.0-p247/gems/devise-3.3.0/lib/devise/rails/routes.rb:457:in `ensure in with_devise_exclusive_scope': undefined method `merge!' for #<ActionDispatch::Routing::Mapper::Scope:0x007fb0d52ccf08> (NoMethodError)
  from /Users/aps/.rvm/gems/ruby-2.0.0-p247/gems/devise-3.3.0/lib/devise/rails/routes.rb:457:in `with_devise_exclusive_scope'
  from /Users/aps/.rvm/gems/ruby-2.0.0-p247/gems/devise-3.3.0/lib/devise/rails/routes.rb:248:in `block (2 levels) in devise_for'
  from /Users/aps/.rvm/gems/ruby-2.0.0-p247/gems/devise-3.3.0/lib/devise/rails/routes.rb:351:in `block in devise_scope'
  from /Users/aps/.rvm/gems/ruby-2.0.0-p247/gems/actionpack-4.2.0.beta1/lib/action_dispatch/routing/mapper.rb:932:in `block in constraints'
  from /Users/aps/.rvm/gems/ruby-2.0.0-p247/gems/actionpack-4.2.0.beta1/lib/action_dispatch/routing/mapper.rb:808:in `scope'
  from /Users/aps/.rvm/gems/ruby-2.0.0-p247/gems/actionpack-4.2.0.beta1/lib/action_dispatch/routing/mapper.rb:932:in `constraints'
  from /Users/aps/.rvm/gems/ruby-2.0.0-p247/gems/devise-3.3.0/lib/devise/rails/routes.rb:350:in `devise_scope'
  from /Users/aps/.rvm/gems/ruby-2.0.0-p247/gems/devise-3.3.0/lib/devise/rails/routes.rb:247:in `block in devise_for'
  from /Users/aps/.rvm/gems/ruby-2.0.0-p247/gems/devise-3.3.0/lib/devise/rails/routes.rb:223:in `each'
  from /Users/aps/.rvm/gems/ruby-2.0.0-p247/gems/devise-3.3.0/lib/devise/rails/routes.rb:223:in `devise_for'
  from /Users/aps/Dev/sideprojects/blogi/webapp/app/config/routes.rb:2:in `block in <top (required)>'
  from /Users/aps/.rvm/gems/ruby-2.0.0-p247/gems/actionpack-4.2.0.beta1/lib/action_dispatch/routing/route_set.rb:377:in `instance_exec'
  from /Users/aps/.rvm/gems/ruby-2.0.0-p247/gems/actionpack-4.2.0.beta1/lib/action_dispatch/routing/route_set.rb:377:in `eval_block'
  from /Users/aps/.rvm/gems/ruby-2.0.0-p247/gems/actionpack-4.2.0.beta1/lib/action_dispatch/routing/route_set.rb:355:in `draw'
  from /Users/aps/Dev/sideprojects/blogi/webapp/app/config/routes.rb:1:in `<top (required)>'
</code>

To fix this now, you need to change your Gemfile to fetch branch _lm-rails-4-2_ of Devise directly from github, like so:

<code>
gem 'devise', :git => 'https://github.com/plataformatec/devise.git', :branch => 'lm-rails-4-2'
</code>

Please note, that for production use, you should probabily wait for new Devise release, where this bug will be merged.

More info: https://github.com/plataformatec/devise/pull/3153
