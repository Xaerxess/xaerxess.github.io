---
layout: post
title: "New module on CPAN - Task::BeLike::XAERXESS"
date: 2014-01-31 22:38:02 +0100
comments: true
categories: Perl CPAN
---

[`Perlbrew`](https://metacpan.org/pod/perlbrew) is a great module. I use it on every machine - it lets me install modern Perl versions on systems which ship with ancient a.k.a. good-old Perls like 5.8, 5.6 or even those from previous millennium. But there comes a problem - every perlbrewed Perl has a separate environment and it lacks all CPAN goodies you installed and used earlier on default system Perl. Plus, if you have few machines and / or like to experiment with various operating systems (like me) you have to install modules you use again and again.

To address this issue I've released [`Task::BeLike::XAERXESS`](https://metacpan.org/release/Task-BeLike-XAERXESS). It's a [`Task`](Task) module which has a simple purpose - installs a module bundle *I* frequently use. What's more, because I uploaded it to CPAN, *you* can use install, try or modify it (the [module source code is on GitHub](https://github.com/Xaerxess/Task-BeLike-XAERXESS)). 

I don't expect anyone besides me will ever install Task::BeLike::XAERXESS but there was another reason I made this module: [`Dist::Milla`](https://metacpan.org/pod/Dist::Milla). Let me cite:

> `Milla` is a `Dist::Zilla` profile. It is a collection of `Dist::Zilla` plugin bundle, minting profile and a command line wrapper. It is designed around the "Convention over Configuration" philosophy (Opinionated), and by default doesn't rewrite module files nor requires you to change your workflow at all (Unobtrusive).

I wanted to make and release a CPAN distribution with `milla` to compare it with pure `dzil` (I'll write my observations later in separate post). In just one sentence - `milla` is great: powerful like `dzil` but much simpler.
