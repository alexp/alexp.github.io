---
  layout: post
  title: Installing rails 4.2 prerelease on OSX 10.9.2 (Mavericks) 
---

Now that rails 4.2 has been released you should definitely consider starting your new projects with edge rails 4.2.0-beta1 version.

In this short post I’ll describe the steps needed to start baking your *new* apps in the newest edge rails version.

And since I’ve been quite negligent in keeping my own system up-to-date, I’ll also take this opportunity and describe the process of upgrading to match the current versions of ruby, ruby gems and rails.

Please note that I am using OSX 10.9.2 Mavericks so your setup might be slightly different.

First of all, there is a bug in rubygems >2.2.2 that prevents you from installing rails 4.2, so make sure, you have ruby gems v. 2.2.2 on our dev machine. 

The error I was getting was:

<pre>
  ERROR:  While executing gem ... (Gem::DependencyError)    Unresolved dependency found during sorting - activesupport (>= 4.0) (requested by sprockets-rails-3.0.0.beta1)
  This bug was reported here:  https://github.com/rails/rails/issues/16609 - keep watching for a fix and update your ruby gems after the fix will have been issued.
</pre>

So this does the job:
<pre>
  gem update --system 2.2.2
</pre>

When developing in Rails, a good strategy to keep your setup in order is to use RVM to manage different versions of Ruby. 
You can learn more about RVM <a href="http://rvm.io/">here</a>. 
Keep in mind though, that there are <a href="http://stackoverflow.com/questions/9659236/what-are-the-alternatives-to-ruby-version-manager-rvm">alternatives</a>

Anyway, to install current stable Ruby version:

Ugrade to the most stable RVM version:

<pre>
  % rvm get stable
</pre>

Then run:

<pre>
  % rvm install 2.1.2
</pre>

After successful ruby installation you can check out your ruby versions by running:
<pre>
  $rvm list                                                                                                                                                                                                                                                                           
</pre>
<pre>
  rvm rubies

  ruby-1.9.3-p125 [ x86_64 ]
  * ruby-2.0.0-p247 [ x86_64 ]
  => ruby-2.1.2 [ x86_64 ]

  # => - current
  # =* - current && default
  #  * - default
</pre>

Finally, to create a new gemset dedicated for your edge rails versions, run:

<pre>
  % rvm use ruby-2.1.2@rails4.2 —create
</pre>

To install Rails prerelease:

<pre>
  % gem install rails —pre
</pre>

Confirm your new rails version:

<pre>
  % rails -v                                                                                                                                                                                                                                                                          
  Rails 4.2.0.beta1
</pre>

During Rails install, I had to tell nokogiri where to find the libiconv dependency.

<pre>
  gem install nokogiri -- --with-iconv-include=/usr/local/Cellar/libiconv/1.14/include --with-iconv-lib=/usr/local/Cellar/libiconv/1.14/lib
</pre>

After rerunning 

<pre>
  % gem install rails —pre
</pre>

.. Rails 4.2.0-beta1 installed correctly. 

Verify your gem list:

<pre>
  % gem list
</pre>

<pre>
  *** LOCAL GEMS ***

  actionmailer (4.2.0.beta1)
  actionpack (4.2.0.beta1)
  actionview (4.2.0.beta1)
  activejob (4.2.0.beta1)
  activemodel (4.2.0.beta1)
  activerecord (4.2.0.beta1)
  activesupport (4.2.0.beta1)
  arel (6.0.0.beta1)
  bigdecimal (1.2.4)
  builder (3.2.2)
  bundler (1.6.2)
  bundler-unload (1.0.2)
  erubis (2.7.0)
  executable-hooks (1.3.2)
  gem-wrappers (1.2.4)
  globalid (0.2.3)
  hike (1.2.3)
  i18n (0.7.0.beta1)
  io-console (0.4.2)
  json (1.8.1)
  mail (2.6.1)
  mime-types (2.3)
  mini_portile (0.6.0)
  minitest (5.4.1, 4.7.5)
  multi_json (1.10.1)
  nokogiri (1.6.3.1)
  psych (2.0.5)
  rack (1.6.0.beta)
  rack-test (0.6.2)
  rails (4.2.0.beta1)
  rails-deprecated_sanitizer (1.0.2)
  rails-dom-testing (1.0.2)
  railties (4.2.0.beta1)
  rake (10.1.0)
  rdoc (4.1.0)
  rubygems-bundler (1.4.4)
  rvm (1.11.3.9)
  sprockets (2.12.1)
  sprockets-rails (3.0.0.beta1)
  test-unit (2.1.2.0)
  thor (0.19.1)
  thread_safe (0.3.4)
  tilt (1.4.1)
  tzinfo (1.2.2)
</pre>
