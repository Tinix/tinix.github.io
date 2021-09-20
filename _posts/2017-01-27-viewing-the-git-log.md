---
layout: post
title:  "Viewing the Git log"
date:   2017-01-27 11:52:19 -0300
categories: git
comments: true
---

This list isn't complete, but the commands shown here are the handful that I use on a day-to-day basis. They should all work in a recent version of git on Linux or macOS (I don't have access to a Windows computer anymore, but if you know something I don't, please leave a comment and I'll amend this article).

- **`git log`**: On its own, `git log` displays a list of commits and their commit messages in reverse chronological order (most recent commits at the top).
- **`git log --reverse`**: Display the output in reverse, so the earliest commits appear at the top of the output.
- **`git log --oneline`**: Passing `--oneline` results in a terse, two-column list of commit titles and SHA identifiers.
- **`git log -p`**: Passing the `-p` flag adds a full patch, or diff, to each commit--the code you added and removed.
- **`git log -p <filename>`**: Passing a file name restricts log output to changes to that file (for example, `git log -p app/models/user.rb`). You can remove the `-p` flag if you don't care about the code changes in each commit, or use `--oneline` instead to get a quick list. I find that I'm almost always interested in the actual code changes, though. If there's a chance that git could confuse the filename for a branch name, include `--` to disambiguate (`git log -p -- app/models/user.rb`).
- **`git log -p -S <query>`**: Use the `-S` flag (also known as the *git pickaxe*) along with a search term to restrict log output to code changes matching the search (for example, `git log -p -S password`). Again, this will work without `-p`, or with `--oneline`, but this is how I typically use it.
- **`git log -p --grep <query>`**: The `--grep` flag searches only the commit messages for the provided query. Wrap the query in quotes if it contains spaces. (You and your team are hopefully [writing useful commit messages](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)!)
- **`git log <commit1>..<commit2>`**: Restrict output to only the differences between two specific commits by passing them with a `..` (and no spaces) between them. This works with SHA identifiers (`git log 660bfa2..922b5d2`) as well as branch names (`git log rails-4.1..rails-4.2`). Leave either side blank to imply the current branch (`git log rails-4.2..`). Use with `-p`, `-S`, and `--grep` as outlined above to filter the results further.
- **`git log --stat`**: Add a brief list of the files that were altered in each commit, with a count of lines that were added or removed. As you may have guessed by now, `--stat` can be used alongside the other flags listed here to narrow results.
- **`git log --no-merges`**: Omit merge commits from the log output (use `--merges` to show *only* merge commits). I don't use these as often.

As I mentioned, this is just a list of the tools I use most often to look at the git log. If you want to learn more, Atlassian's article on [advanced git logging](https://www.atlassian.com/git/tutorials/git-log) is a great next step.
