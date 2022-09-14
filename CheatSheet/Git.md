## GIT - Commands

#### Basics:

```
git init //To create git repo
git add index.js // To add a file to repo
git add . //Add all files to repo
git commit -m “commit message” //commit
git log //to check history
git commit --amend //amend this commit to previous commit
```

#### Branch:

```
git checkout {​​​​​​​​branchName}​​​​​​​​ //move to branch
git branch -a - //show all branch
git checkout -b “newBranchName” //to create new branch
git branch -D "branchname" //to delete branch
git remote prune origin --dry-run // Delete all local branches which are not in remote.
```

#### Remote:

```
git fetch
git pull
git push
git push —force-with-lease //safely push
```

#### Advanced:

```
git cherry-pick <commit> //cherry pick a commit
git rebase master //rebase from master
git rebase -i master //interactively rebase from master
git reset --soft HEAD~1
git reset
git reset HEAD~1 //to reset latest commit
git push origin :refs/tags/v0.1.0 //delete tag
```

#### Two origin (Gitlab & github)

```
git remote add github https://github.com/user/repo.git
git push origin <branch> (GitLab)
git push github <branch> (GitHub)
git pull origin <branch> (GitLab)
git pull github <branch> (GitHub)
```

#### Clean up git history/Squash all

```
git reset $(git commit-tree HEAD^{​​​tree}​​​ -m "A new start")
```

#### Overwrite

1. Make sure your working tree is in a clean state using

```
git status

```

2. Check out the branch you want to change, e.g. some-branch

```
git checkout some-branch
```

3. Reset that branch to some other branch/commit, e.g. target-branch

```
git reset --hard target-branch
```

#### Merging commits

ways you can achieve a Git Squash

Interactive Rebase Approach

```
git checkout <branch_name_to_be_squashed>
git rebase -i HEAD~4
```

This command will open up an editor where you can just replace pick with squash in order to remove/merge them into one.
where 4 is the number of commits you want to squash into one.

Once this is done and saved, another editor pops up.
Since we’re combining so many commits, Git allows you to modify the new commit’s message based on the rest of the commits involved in the process.
Once that’s done, your commits have been successfully squashed!

#### Tutorials:

Git Tutorial for Beginners - Crash Course - (Academind) - https://www.youtube.com/watch?v=_OZVJpLHUaI

Learn the Basics of Git in Under 10 minutes - (FreeCodeCamp Blog) - https://www.freecodecamp.org/news/learn-the-basics-of-git-in-under-10-minutes-da548267cc91/#:~:text=Git%20is%20a%20version%2Dcontrol,versions%20of%20a%20project's%20files
