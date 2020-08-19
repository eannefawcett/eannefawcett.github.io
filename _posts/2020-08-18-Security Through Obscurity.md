---
layout: post
title:  "Security Through Obscurity for Blogging with Jekyll"
date:   2020-08-18 20:27:37
categories: non-technical, security
paginator: Security Through Obscurity
---

The question of security of data and models comes up frequently in the world of data science. The way that people talk about security can verge on superstition.

<img src='../images/security_advice.png' alt='https://xkcd.com/1820/'>


Today, I'm here to talk about one method to secure blog posts called "Security Through Obscurity". The general idea is you don't know what you know. For instance, let's say that you have a blog on a little trafficked website, but that is under the online handle that you use for everything, and you want to secure certain posts more than other to protect certain types of intellectual property.

Some things to consider in this scenario are that websites tend to follow a predefined url structure for each webpage under the main one, and that it is likely predictable. In fact for this website the code to generate the urls is:




```
/:year/:month/:day/:title/
```




This is found in the .yml file for this website. This is relatively predictable, but I don't follow a posting schedule presently. This adds a random element to the year, month, and day part of the url. The title is made up by me as the title of the blog post. If you wanted to add another layer of protection to protect this url, you could add a randomizer element, like so:




```
/:year/:month/:day/:title/:randomizer
```



This randomizer could be a string of text and numbers that is a random length. For instance, I just used [random.org][link1] to generate 'MYXprOFQeELrgrViadeM'. If there were a part of my website that I wanted to personally approve people to view, I could add this randomizer in the header of the post while writing. The header for this post is:

layout: post
title:  "Security Through Obscurity"
date:   2020-08-18 20:27:37
categories: non-technical, security
paginator: Security Through Obscurity

To add the randomizer, I would modify the header to look like this:

layout: post
title:  "Security Through Obscurity"
date:   2020-08-18 20:27:37
categories: non-technical, security
paginator: Security Through Obscurity
radomizer: MYXprOFQeELrgrViadeM

Additionally, the randomizer would need to be added the file name after the title.

When linking to the "secure" post throughout the site, I would leave off the randomizer, and have the 404 page say to contact if the user thinks they should have access to the page. If the user should, like a potential employer trying to see an abstract, then I would send them the randomizer with instructions to append the randomizer to the end of the url to view the page.

And those are the steps I would take to increase security through obscurity for certain posts while blogging.

[link1]: https://www.random.org/
