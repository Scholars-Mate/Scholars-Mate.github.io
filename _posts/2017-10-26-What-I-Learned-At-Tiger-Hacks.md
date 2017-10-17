---
layout: post
title: What I Learned At Tiger Hacks
date: 2017-10-26
---

I had a lot of fun at Mizzou's Tiger Hacks hackathon a few weeks ago. One of the
great things about hackathons is that it is a great place to learn. It's
actually a lot of fun to jump into technologies you haven't used before, and
especially fun to learn more about technologies you were already familiar with.
Here are some of the things I learned at Tiger Hacks:

## Don't be afraid to `git commit`
Previously, I thought that all my commits should be perfect, and something that
I could push upstream with no modifications. This meant that I wouldn't actually
commit all that often. When I needed to switch branches, but had unsaved work, I
would use `git stash`. This could get confusing quickly if you have a lot of
branches. This all changed when one of my group members introduced me to
interactive rebasing. With `git rebase -i`, you can rewrite history. You can use
it to reorder commits, squash multiple commits down to a single, logical commit,
or simply delete commits. This is incredibly useful because you can make your
commit history as messy as you'd like to in your own branch. All you have to do
is rebase to get a nice set commits that you can push upstream.

## Use branches in `git` extensively
As I alluded to earlier, a messy commit history is perfectly fine in your own
branch. The problem with rewriting history is that if anyone else is using the
branch, it will be very confusing to figure out what happened when they have
suddenly diverged from master. This is where branches come in. If you have your
own branch, you can do whatever you want in it. In addition, it's great idea to
make a new branch for the different components you are working on. Branches are
cheap to make. It's best to just leave your master branch alone and in sync with
upstream and do all your work in separate branches. If you want your branch to
reflect the latest master, all you need to do is rebase.

## Bootstrap is pretty cool
I had never done web development in any capacity before Tiger Hacks. I knew of
HTML, CSS, and JavaScript, but I had never really made anything of my own using
those technologies. Tiger Hacks was my first introduction to doing much of
anything on the web. We used Bootstrap in our project, and I was tasked with
helping set up the front end of our project. Bootstrap proved very easy to use,
even to a beginner like me, and I was able to get the site looking the way we
wanted it to. I actually used Bootstrap to help make this site after Tiger
Hacks.

## I'm glad I use Linux
Out of the four group members we had, only one was using Windows. The rest of us
were Linux users. This made setting up our test environments trivially easy.
Unfortunately, our other group member was not so lucky. After trying to get his
environment set up on Windows for a while, he gave up and used a virtual
machine. This proved to be easier, but with annoyances of its own. I don't want
to come off as a Linux fanboy, but in this case, using Linux had its advantages
and I was happy for it.

Unfortunately, we weren't able to finish our project for Tiger Hacks, but
despite this, I had a lot of fun and learned quite a bit. In the end, isn't
that what hackathons are all about?
