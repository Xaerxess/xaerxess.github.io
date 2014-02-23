---
layout: post
title: "New module on CPAN - Task::BeLike::XAERXESS"
date: 2014-01-31 22:38:02 +0100
comments: true
categories: Perl CPAN
---

[Perlbrew](https://metacpan.org/pod/perlbrew) is a great module. I use it on every machine - it lets me install modern Perl versions on systems which ship with ancient a.k.a. good-old perls like 5.8 or even those from previous millennium. But there comes a problem - every perlbrewed perl has a separate environment and it lacks all CPAN goodies you installed and used earlier. Plus, if you have few machines and / or like to experiment with various operating systems (like me), you have to install modules you use again and again.

To address this issue I've released [`Task::BeLike::XAERXESS`](https://metacpan.org/release/Task-BeLike-XAERXESS). It's a [`Task`](Task) module which has a simple purpose - it installs a module bundle *I* frequently use. What's more, because I uploaded it to [CPAN](http://www.cpan.org/), *you* can use install, try or modify it (the [module source code is on GitHub](https://github.com/Xaerxess/Task-BeLike-XAERXESS)).

<!-- more -->

I don't expect that anyone besides me will ever install and use `Task::BeLike::XAERXESS`, but there was another reason I made this module: do a module release with [`Dist::Milla`](https://metacpan.org/pod/Dist::Milla). Let me cite:

> `Milla` is a `Dist::Zilla` profile. It is a collection of `Dist::Zilla` plugin bundle, minting profile and a command line wrapper. It is designed around the "Convention over Configuration" philosophy (Opinionated), and by default doesn't rewrite module files nor requires you to change your workflow at all (Unobtrusive).

I wanted to compare `milla` with pure `dzil` because I used latter once (to release my first module - [`Time::Duration::pl`](https://metacpan.org/pod/Time::Duration::pl)) and last few days there was [quite much buzz](http://blogs.perl.org/users/brian_d_foy/2012/08/should-my-perl-release-process-be-yours.html) about `Dist::Zilla` being [suitable module releasing tool](http://www.dagolden.com/index.php/2275/distzilla-haters-stop-your-whining/). I'll write all my observations later in separate post, in just one sentence - `milla` is great: powerful like `dzil` but much simpler, it has everything _I_ need to release a Perl module.
