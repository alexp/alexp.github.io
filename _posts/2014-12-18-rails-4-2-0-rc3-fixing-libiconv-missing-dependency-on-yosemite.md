---
  layout: post
  title: Rails 4.2.0.rc3 - Fixing libiconv missing dependency on OS X Yosemite (10.10.1)
---

OK, so today I tried to install the newest <a href=“http://weblog.rubyonrails.org/2014/12/13/Rails-4-2-0-rc3-has-been-released/”>release candidate</a> of Rails - the <strong>4.2.0.rc3</strong> and *again*, I got the missing libiconv dependency error while installing nokogiri, version 1.6.5.

<code>
ERROR:  Error installing nokogiri:
     ERROR: Failed to build gem native extension.

    /Users/aps/.rvm/rubies/ruby-2.1.5/bin/ruby -r ./siteconf20141218-1242-b4o2ja.rb extconf.rb
checking if the C compiler accepts ... yes
checking if the C compiler accepts -Wno-error=unused-command-line-argument-hard-error-in-future... no
Building nokogiri using packaged libraries.
checking for iconv... no
-----
libiconv is missing.  Please locate mkmf.log to investigate how it is failing.
-----
*** extconf.rb failed ***
Could not create Makefile due to some reason, probably lack of necessary
libraries and/or headers.  Check the mkmf.log file for more details.  You may
need configuration options.

Provided configuration options:
     --with-opt-dir
     --without-opt-dir
     --with-opt-include
     --without-opt-include=${opt-dir}/include
     --with-opt-lib
     --without-opt-lib=${opt-dir}/lib
     --with-make-prog
     --without-make-prog
     --srcdir=.
     --curdir
     --ruby=/Users/aps/.rvm/rubies/ruby-2.1.5/bin/ruby
     --help
     --clean
     --use-system-libraries
     --enable-static
     --disable-static
     --with-zlib-dir
     --without-zlib-dir
     --with-zlib-include
     --without-zlib-include=${zlib-dir}/include
     --with-zlib-lib
     --without-zlib-lib=${zlib-dir}/lib
     --enable-cross-build
     --disable-cross-build

extconf failed, exit code 1
Gem files will remain installed in /Users/aps/.rvm/gems/ruby-2.1.5/gems/nokogiri-1.6.5 for inspection.
Results logged to /Users/aps/.rvm/gems/ruby-2.1.5/extensions/x86_64-darwin-14/2.1.0-static/nokogiri-1.6.5/gem_make.out
</code>

I headed back to official <a href=“http://www.nokogiri.org/”>Nokogiri website</a> and reviewed their <a href=“http://www.nokogiri.org/tutorials/installing_nokogiri.html”>installation guidelines</a>, which basically say that on OS X it should work out of the box, unless you encounter the <code>libiconv</code> issues ;).

But still, they claim that the following should do the trick:

<code>
brew unlink gcc-4.2 # you might not need this step
gem uninstall nokogiri
xcode-select --install
gem install nokogiri
</code>

Unfortunately that did not work for me, so I started investigating. I tried the solution from my <a href=“http://blog.sailsoftware.co/2014/09/05/upgrading-rails-to-4-2-0-beta1-on-mavericks.html”>previous blog post</a>, which fixed the problem by passing the additional parameter for non-standard iconv installations (
gem install nokogiri --with-iconv-include=/usr/local/Cellar/libiconv/1.14/include --with-iconv-lib=/usr/local/Cellar/libiconv/1.14/lib
)

But really, I wanted to get it working cleanly this time, without the custom steps and/or hacks involved. Of course I tried to pass the —with-iconv-include parameters in and that didn’t do the trick either.

So what’s the deal here? With up-to-date Xcode developer tools installed, iconv actually installed at /usr/bin/iconv and still failing to install by pointing to the brew version of libiconv, I tried to <strong>unlink the libiconv</strong> at brew and finally got it working as expected!

So please find the actual steps I took, below:

# install the latest ruby 2.1.5
% rvm install ruby-2.1.5

% brew unlink libiconv                                                                                                                                                                                                                                                               
Unlinking /usr/local/Cellar/libiconv/1.14... 125 symlinks removed

% gem install nokogiri # you can skip it and and go directly to installing rails of course

% gem install rails —version 4.2.0.rc3

% rails -v
Rails 4.2.0.rc3

Nice and clean now, rockin' on a bleeding edge of Rails again :)
