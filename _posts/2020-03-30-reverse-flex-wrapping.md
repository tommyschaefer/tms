---
layout: post
title: "Reverse Flex Wrapping"
link: https://labs.teecom.com/2020/03/30/reverse-flex-wrapping.html
originally_posted_on: TEECOMlabs blog
---

While working on a side project last week, I ran into a pretty ugly visual bug
with long content.

![](/images/reverse-flex-wrap/before-design.png)

After brainstorming a bit, I decided that wrapping the `Discussed IRL` badge
across lines might look okay. Then the question was, should it wrap upwards or
downwards?

![](/images/reverse-flex-wrap/mockup.png)

Based on my really rough mockup, I decided that the badge should wrap upward.
I struggled to find the best way of implementing this until I learned that
[`flex-wrap`](https://www.w3schools.com/cssref/css3_pr_flex-wrap.asp) has a
`wrap-reverse` option.

![](/images/reverse-flex-wrap/wrapping.png)

Perfect! After applying this to my existing code, I was pretty happy with the
result!

![](/images/reverse-flex-wrap/after-design.png)
