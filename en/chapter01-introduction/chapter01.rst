Introduction and What To Expect
===============================

Hello, and welcome to 'Salt Book'! I thought it would be best to start by
explaining how this book operates, and how we're going to progress through
learning Salt. This book is for beginner and intermediate users, we aren't
going to get into some of the very advanced or obscure topics of Salt, but
we are going to look at how you can become better at using Salt. In addition
to that, we're not going to talk about HOW to do server builds, deployments,
or general information like repository structure. This is up to you and your
organization. You picked up this book to learn Salt, and that's what we're
going to focus on. To begin with we need to get some of the basics out of the
way. If you feel comfortable with Salt, or have already been experimenting
you might want to skip these first few sections.

This book is going to be focused on helping YOU to learn Salt, what this
means is there are a lot of overly verbose examples, details on a per line
basis when needed, and a lot of small projects that you're going to be
building. If you're looking for a more terse manual, then please review the
existing Salt documentation, which while extremely thorough, isn't going to
walk you through from installation to running application like this book will.
If you're looking to build something with Salt then this is the book for you.
 

What Makes Salt Awesome
=======================

I'm sure a lot of you are currently trying to justify some sort of
configuration management to the higher ups in your organization, or maybe
you're just trying to move from another configuration management tool to Salt.
Either way, let's talk about what Salt brings to the table that makes it my
tool of choice.

* The way Salt processes jobs is lightweight, as the server the work is to be
  performed on is completing the actions. This means that your ``Salt master``
  does very little work, it ensures things are put together properly, and then
  sends them to the minion, which then does the work (more on this later).

* Salt is stupidly fast thanks to ZeroMQ, and how data is broken down. It uses
  PUB/SUB to broadcast data out.

* Salt is written in Python. If you can write Python, you can make Salt do
  what you need.

* As of writing this book Salt is completely open source. That means there's
  no corporate shennanigans to get in the way of getting things done.

* Salt uses Jinja2 (or Mako) and YAML, making it pretty easy to write even if
  you're a beginner.

* Salt has a large number of pre-written ``formulas`` which will help you get
  up and running quickly. Those are available here: 
  https://github.com/saltstack-formulas.

Salt Basics
===========

Let's start with the basics of Salt, and how it operates.

To begin with you have your ``Salt master``, this is the server from which you
execute commands. There can be multiple ``Salt masters`` depending on how your
infrastructure is configured.

All of the servers which will be accepting commands, or changing configuration
are your ``Salt minions``. These machines are just all of the boxes that are
part of your infrastructure (web servers, database servers, etc.), the
``Salt master`` itself can even be a ``Salt minion``!

The transporation method used is ZeroMQ, it's fast, efficient, and powerful.

With just the information introduced here we can get started with Salt. There
are many more facets, but those don't need to be explained until we actually
use them.


How Salt Works
==============

Salt works by compiling the data you've presented it with into a dictionary.
Once this dictionary is compiled, it creates a ``job ID`` for each server you
are executing commands on, then passes the dictionary to the 
``Salt Minion``, and then releases the process (note that the zeromq
connection continues to be established). From here the ``Salt Minion``
takes the dictionary, interprets it, and executes the commands. Once the run
is complete (whether it has succeeeded or fails) the information is sent back
to the ``Salt Master``, and the associated ``job ID`` is updated with the 
details.

That's Salt in the simplest terms, and it's really all you need to know for
right this moment. The key thing to take away is the fact that Salt does NOT
process commands on the ``Salt master``, that job is left to the
``Salt minion``. It's also important to understand that Salt does not leave
processes to the ``Salt minion`` hanging. It simply waits to hear back to
update the ``job ID``.


What you need before starting this book
=======================================

You're going to need some sort of environment to work on Salt in. Each chapter
will build on the infrastructure of the previous chapter, so you'll either
need to create local VMs, or VMs on your favorite provider. This book
currently only covers Debian and RHEL based distros, if you'd like to
experiment with others you are more than welcome to do so.
