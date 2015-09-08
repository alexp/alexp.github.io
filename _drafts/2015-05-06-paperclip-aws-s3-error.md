---
  layout: post
  title: uninitialized constant Paperclip::Storage::S3::AWS
---

When trying to set up the Paperclip gem with Amazon S3 storage I encountered the following error:

<script src="https://gist.github.com/alexp/28db7db35c58741aabfa.js"></script>

Reverting the <code>aws-sdk</code> gem to version < 2.0 fixed it for me:

In Gemfile: <br/>

<code>gem 'aws-sdk', '< 2.0'</code>

As Trevor Rore from Amazon writes:

<blockquote>
NameError: uninitialized constant AWS
<br/>
If you receive this error, you likely have a dependency on aws-sdk and have updated so that you now have version 2 installed. Version 2 uses a different module name, so it does not define AWS.
</blockquote>

Read more <a href="http://ruby.awsblog.com/post/TxFKSK2QJE6RPZ/Upcoming-Stable-Release-of-AWS-SDK-for-Ruby-Version-2">here</a>.
