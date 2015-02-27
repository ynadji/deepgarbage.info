# HOWTO

I envision our publishing process like so:
* independently make updates to files in `_drafts`. you can test locally by running `jekyll serve` in the root directory
* when we're done with a post `git mv` it to _posts and push
* i'll pull/build whenever we push to github or every 5 minutes or w/e

# Directory Structure

See the [structure](http://jekyllrb.com/docs/structure/) document on Jekyll's
homepage but here are the important ones:

* `_posts`: for posts
* `_data`: for _internal_ data (only used when Ruby runtime builds the site)
* `_drafts`: for drafts duh

Folders without a leading `_` are copied over verbatim so `images/faj.png` will be
at http://deepgarbage.info/images/faj.png. I made `images` and `data` since I figure
we'll use those often. Maybe let's make separate dirs per project/post/whatever?
