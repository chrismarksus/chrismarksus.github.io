
---
layout: post
title:"Separate your rake tasks"
tags: ruby rake

This was a little trick that I found online when I was looking for information on unit testing rake tasks. The programmer broke up the tasks into different files so they could be loaded and tested apart from the rest of the tasks. I have started to do this and I find it has some benefits on it's own.

<!--more-->

To start with you need to create a folder structure that keeps the tasks and support code organized. Below is a sample of how I have organized some projects. The **rakefile** is stored at the top level and you add all of the rake tasks in the ```lib/tasks/``` folder. I give each task and extension of *filename.rake*. This is not an approved extension but it makes it easy to load and organize. The ```modules/``` and ```classes/```` folders are where you store the support code that is common to the tasks.

```
rakeFile
lib/
   |-> classes/
   |-> modules/
   |-> tasks/
            |-> clean.rake
            |-> deploy.rake
```

All you have to do at this point is add the line below to the rakefile at the top level to load all of the tasks. I find it easier to pull this at the top of the file.

```ruby
    Dir.glob('lib/tasks/*.rake').each { |r| load r}
```

I also have not seen any value in a separate rake file for the default so I just keep it in the *rakefile* as well. 

```ruby
    desc "Assign default, see deploy"
    task :default => :deploy do
    end
```

Even if you don't unit test your ruby tasks you will find that this helps in managing and editing *rakefiles*.
