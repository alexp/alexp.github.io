---
  layout: post
  title: Devise + Rails 4.2.0-beta1 - fixing undefined method 'merge!' 
---

If you have just upgraded your Devise based app to Rails 4.2.0-beta1 version, you probabily encountered the following error:

<script src="https://gist.github.com/alexp/22a768903dd945f7b20f.js"></script>

To fix this now, you need to change your Gemfile to fetch branch _lm-rails-4-2_ of Devise directly from github, like so:

<pre>
gem 'devise', :git => 'https://github.com/plataformatec/devise.git', :branch => 'lm-rails-4-2'
</pre>

Please note, that for production use, you should probabily wait for new Devise release, where this bug will be merged.

More info at: <a href="https://github.com/plataformatec/devise/pull/3153">https://github.com/plataformatec/devise/pull/3153</a>
