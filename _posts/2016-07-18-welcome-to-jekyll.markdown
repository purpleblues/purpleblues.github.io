---
layout: post
title:  "Welcome to Jekyll!"
date:   2016-07-18 18:47:49 +0900
---

You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:




```c

//write mxFrame number to master journal

Pager *pPager;   /* Pager associated with pBt */

sqlite3BtreeEnter(pBt);
pPager = sqlite3BtreePager(pBt);
if( pagerUseWal(pPager) ){
    char mxFrame[12];
    sprintf(mxFrame, "%u", pPager->pWal->hdr.mxFrame);
    rc = sqlite3OsWrite(pMaster, mxFrame, sqlite3Strlen30(mxFrame)+1, offset);
    offset += sqlite3Strlen30(mxFrame)+1;
}
// rc = sqlite3PagerExclusiveLock(pPager);
sqlite3BtreeLeave(pBt);
//end

```

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
