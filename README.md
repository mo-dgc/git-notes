# Multi-identity Github Notes

I use github all day long for work and other personal projects.  Like everyone else, I set the global settings for my ```user.name``` and ```user.email```.  However, this means that for work projects, alerts would goto my default global stuff which is my personal email.  That's not very useful for me.  

Here's how I use multiple identities with github on a per repo basis.

# Cloning a repo

Cloning a repo is just the same as anything else.  Remember if working on a community project to fork it first so you can easily create pull requests for the project.

I'm using this repo for these notes.

```
~/dev$ git clone https://github.com/mo-dgc/git-notes.git
Cloning into 'git-notes'...
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
```

I then set my ```user.name``` and ```user.email``` that I want associated with this repo/project.

```
~/dev/git-notes$ git config user.name "Mo"
~/dev/git-notes$ git config user.email "grower.mo@gmail.com"
```

That's not it though.  If you look at your remote URLs, you'll see there's no user associated, so git will attempt to use what is set in your global git configuration:


```
~/dev/git-notes$ git remote -v
origin	https://github.com/mo-dgc/git-notes.git (fetch)
origin	https://github.com/mo-dgc/git-notes.git (push)
```

Now we need to modify these - you'll need ot know your username for github (not your email address - this is also the same one used in the url for your repo's if you don't know what it is).  You'll insert that username into the URL so Github knows which user to use.

```
~/dev/git-notes$ git remote set-url origin https://mo-dgc@github.com/mo-dgc/git-notes.git
~/dev/git-notes$ git remote set-url --push origin https://mo-dgc@github.com/mo-dgc/git-notes.git
```

Now you can show them again, and you should see your userid being used:
```
~/dev/git-notes$ git remote -v
origin	https://mo-dgc@github.com/mo-dgc/git-notes.git (fetch)
origin	https://mo-dgc@github.com/mo-dgc/git-notes.git (push)
```

Now when you push to the repo everything will use the correct identity:

```
~/dev/git-notes$ git commit -m "Updating notes"
[master 285e294] Updating notes
 1 file changed, 52 insertions(+), 2 deletions(-)
 rewrite README.md (100%)
~/dev/git-notes$ git push
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 1.08 KiB | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/mo-dgc/git-notes.git
   9e00675..285e294  master -> master
```

Which will show on Github as:

(example-commit.jpg)
