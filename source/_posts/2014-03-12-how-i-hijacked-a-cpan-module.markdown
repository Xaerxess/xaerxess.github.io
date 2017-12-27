---
layout: post
title: "How I hijacked a CPAN module"
date: 2014-03-12 19:01:51 +0100
comments: true
categories: Perl CPAN
---

Today Neil Bowers ([@neilbowers](https://twitter.com/neilbowers/)) wrote a blog post titled ["What happens when you upload to CPAN?"](http://neilb.org/2014/03/11/uploading-01.html) - a sneak peek at the very last part of module releasing process (when you do `cpan-upload` and recieve these two strange emails). Although I've already released few distributions, [PAUSE](https://pause.perl.org) still seems to me as a mysterious tool with design (i.e. web interface) from previous epoch[^1], but somehow capable of managing over 29000 distributions maintained by over 11000 authors. <!-- more -->What intrigued me in Neil's article was the "hairy" part (namespace indexer), particularly a conclusion (_"the permissions check should be separate from, and earlier than, the indexing stage"_) and these three points:

 > - PAUSE checks each package in your release to see if you're allowed to release it. You must either be the owner or have co-maint (see the doc for PAUSE::Permissions). If you've flagged the package with no_index in the metadata, then the check is skipped.
 > - You are given ownership ('f' permission) for any packages that don't currently have any permission associated with them in PAUSE.
 > - The second email is sent to you, with the results of the permissions check.

What wasn't clear to me was whether PAUSE let me do an "unauthorized release" of a module which doesn't have any owner listed in `06perms.txt`. To find out, I wrote a simple script which found modules without owner (using [`PAUSE::Permissions`](https://metacpan.org/pod/PAUSE::Permissions)) and then checked which of these are existing distributions (using [`CPAN::Source`](https://metacpan.org/pod/CPAN::Source)[^2]).

As a result I had a list containing few "abandoned" distributions, from which I chose one: [`YAML::AppConfig`](https://metacpan.org/pod/release/MOCONNOR/YAML-AppConfig-0.16/lib/YAML/AppConfig.pm) - previously released in 2006, with few bugs on RT. I made two [small](https://github.com/Xaerxess/YAML-AppConfig/commit/3bd3da22af39df848eebf6db69ab2e7e200c82c9) [fixes](https://github.com/Xaerxess/YAML-AppConfig/commit/2e618883a9bfe464f547509fcfed6487b2a1cd84), bumped version to 0.17, made gzipped dist file and uploaded it to CPAN. I was expecting I'd receive two emails from PAUSE, the second informing me that distribution wasn't indexed due to insufficient permissions. To my astonishment, I actually got _"Status of this distro: OK"_ and _"Status: Successfully indexed"_, and after few hours every piece of Perl / CPAN / PAUSE ecosystem listed my release as [proper one](https://metacpan.org/pod/YAML::AppConfig). I've checked `06perms.txt` and found:

    YAML::AppConfig,MOCONNOR,c
    YAML::AppConfig,XAERXESS,f

PAUSE gave me 'f' permission, which I thought are given only to **original** distribution author. According to one of last Perl Advent Calendar articles covering [PAUSE permissions model](http://perladvent.org/2013/2013-12-08.html):

> The 'f' permission ('first come') says that I was the **first person** to upload the module.

...who **I** wasn't. At this point I closed a bug on RT, and started tweaking `YAML::AppConfig`, which, although "hijacked", I consider suitable for my [Monthly New Distribution Challenge 2014](https://questhub.io/realm/perl/quest/530a823b6e7817b05100001a).

To sum up, either my understanding of PAUSE permissions is wrong or they have some flaws (or maybe features?). If I'm wrong, please correct me.

Anyway, does module hijacking counts as a module adoption?

---

**Follow-up**

I didn't mean to disclose potential security threat, and I'm sure I'll be more careful in the future writing about similar issues. Luckily, as you can see [in the comment](/blog/2014/03/12/how-i-hijacked-a-cpan-module.html#comment-1283194094), [@rjbs](https://twitter.com/rjbs) was in the right place in the right time (i.e. [Perl QA Hackaton 2014](http://act.qa-hackathon.org/qa2014/)) and [fixed the bug](https://github.com/andk/pause/commit/d3e76f314c33570b2670b07eb7c2a93ccfcec66a) in PAUSE.

To be honest, I looked at PAUSE code after I had "hijacked" module, but setting up PAUSE is ["Very Hard™"](https://twitter.com/rjbs/status/444185178811146240). For example, I didn't have any [Apache 1.3 with mod_perl1](https://github.com/andk/pause/blob/66f72204e24957415f5d2aca3fba519661beb2d8/doc/README#L142) ready at hand, nor any spare time to compile it. Hope it'll be easier in the future.

One more thing - I took the opportunity and "adopted" `YAML::AppConfig`: fixed all bugs, made all tests pass, added changelog, modernized its metadata, and uploaded version 0.19 on CPAN. If you spot more bugs (either in PAUSE or `YAML::AppConfig`), please report them. It's open source after all.

[^1]: That said, I really like the [idea of PAUSE and MetaCPAN dashboard integration](http://neilb.org/2014/03/10/cpan-dashboard.html#comment-1279343094).
[^2]: I had to fix `CPAN::Source` first; I'll try to publish fixes for it later, because actually it's a nice tool with 100% test failed on CPAN Testers.