---
layout: post
title: "[RAILS] PG::Error: ERROR: relation does not exist"
categories:
- blog
---

I recently decided to try and migrate one of my rails apps to [Heroku](http://heroku.com). It was my first Heroku app, and I'm learning a lot in the process. One of the first gotchas I ran into was that I needed to convert my app to use postgres since that's what Heroku seems to work best with and has the most documentation around.

I figured I would try and get this working locally before messing around with getting it to work on the Heroku server. First I had to modify my local config/database.yml file to connect to the postgres server. (*Hint: Heroku will overwrite this file so your local copy doesn't matter over on the Heroku server*)

    development:
      adapter: postgresql
      encoding: unicode
      database: pg_tcj
      username: postgres
      pool: 5
      host: localhost

<!--more-->

Next I wanted to load my database schema into the new postgres database, something I've done a thousand times with other database connectors:

    rake db:schema:load

To my surprise, I got the following error:

    PG::Error: ERROR:  relation "pages" does not exist
    LINE 4:              WHERE a.attrelid = '"pages"'::regclass
                                            ^
    :             SELECT a.attname, format_type(a.atttypid, a.atttypmod), d.adsrc, a.attnotnull
                  FROM pg_attribute a LEFT JOIN pg_attrdef d
                    ON a.attrelid = d.adrelid AND a.attnum = d.adnum
                 WHERE a.attrelid = '"pages"'::regclass
                   AND a.attnum > 0 AND NOT a.attisdropped
                 ORDER BY a.attnum

I spent more time than I'd like to admin trying to figure out what was going on. In my web searches I consistently found the same two suggestions:

1. Simply run `rake db:migrate:reset` (or similar). Obviously this didn't work since I was getting the error while trying to run `rake db:migrate` or `rake db:schema:load`!

2. The other suggestion was that something in the rails environment was trying to use a model before it was created. ActiveAdmin is a gem that came up frequently. This is was probably the more likely scenario for my code.

Armed with that knowledge I tried to figure out what could possibly be trying to use my `pages` model before it was created. One line in the stack trace I got from `rake db:schema:load --trace` stuck out to me:

    /home/eric/dev/rails/tcj/config/routes.rb:56:in `block in <top (required)>'
    /home/eric/.rvm/gems/ruby-1.9.3-p194/gems/actionpack-3.2.1/lib/action_dispatch/routing/route_set.rb:272:in `instance_exec'
    /home/eric/.rvm/gems/ruby-1.9.3-p194/gems/actionpack-3.2.1/lib/action_dispatch/routing/route_set.rb:272:in `eval_block'
    /home/eric/.rvm/gems/ruby-1.9.3-p194/gems/actionpack-3.2.1/lib/action_dispatch/routing/route_set.rb:249:in `draw'

Ah ha! Routes is a pretty good suspect for something that runs early in the rails loading process. In my routes.rb file, I have the following:

    Page.all.reject{|x| x.slug.blank? }.each do |page|
      match page.slug => 'pages#show', :id => page.id
    end

Bingo! In my application, which is a sort of pseudo CMS, I'm setting up routes for custom slugs on the pages that are added. Here I was trying to reference the *page* model before it was ever created.

**Simply commenting out the three lines above temporarily solved the problem**.

Hopefully this saves someone some time someday!