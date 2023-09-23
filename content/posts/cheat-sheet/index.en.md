---
weight: 1
title: "Cheatsheet"
date: 2020-03-06T21:29:01+08:00
lastmod: 2020-03-06T21:29:01+08:00
draft: false
author: "Sharad"
authorLink: "https://sharadsingh.net"
description: "Cheatsheet"
# resources:
#  - name: "port-mapping"
#    src: "port-mapping.png"
# - name: "featured-image-preview"
#   src: "featured-image-preview.webp"

tags: ["git commands", "dotnet CLI","git cheatsheet"]
categories: ["Cheatsheet"]

lightgallery: true

toc:
  auto: false
---
### DOT NET CLI

``` dotnet --list-runtimes ```

#### List all availabel commands
```dotnet new list api```

```dotnet new webapi -n YourApiName
```

Create a new .sln file
``` dotnet new sln ```
Create a new .sln file in a subfolder

```
dotnet new sln -o MySolution
```

#### Create a new project

```
dotnet new [TEMPLATE]
dotnet new web
```

Create a new project in a subfolder

```
dotnet new [TEMPLATE] -o [NAME]
dotnet new web -o Backend
dotnet new mvc -o MyApp
dotnet new console -o MyApp
dotnet new classlib -o MyLib
dotnet new mstest -o MyLib.Test
dotnet new nunit -o MyLib.Test
```

##### Add Git ignore file

``` dotnet new gitignore ```

##### Add Project for specific dotnet version

``` dotnet new console -f net7.0 --name "TestUI" ```

##### Add Project to sln file

``` dotnet sln vscode-handson.sln add TestUI/TestUI.csproj ```

#### Manage project dependency

**Add a reference to another project**

``` dotnet add reference [PROJECT_PATH]
 dotnet add reference ../MyLib/MyLib.csproj ```

**Remove a project reference**

``` dotnet remove reference [PROJECT_PATH] 
 dotnet remove reference ../MyLib/MyLib.csproj ```
List all project references
```dotnet list reference```
Add a Nuget package
```dotnet add package [PACKAGE] 
 dotnet add NewtonSoft.Json```
Remove a Nuget package
```dotnet remove package [PACKAGE]```
 dotnet remove NewtonSoft.Json 
List all project references
```dotnet list package```

#### Test
Run the tests
`dotnet test`
Run the tests and create test report
`dotnet test --logger "trx;LogFileName=results.trx"`
List all tests without running them
`dotnet test -t`
Run specific tests
`dotnet test --filter "[FILTER]"`
`dotnet test --filter Unit`
`dotnet test --filter "TestCategory=Database"`
`dotnet test --filter "TestCategory!=Slow"`
`dotnet test --filter "Unit&(TestCategory=Cat1)"`

#### BUILD
Build the project or solution in the current folder
`dotnet build`
Build the Release configuration
`dotnet build -c Release`
Build the project or solution
`dotnet build [PROJECT/SOLUTION]`

#### RUN
Run an application
`dotnet run`

#### Watch
Watch an application
`dotnet watch`



#### Publish
Publish the project or solution from the current folder
dotnet publish
Publish specific project or solution
dotnet publish [FOLDER]
dotnet publish MyApp
Build a self-contained executable for Windows
dotnet publish -c Release -r win-x64 -f netcoreapp2.2
Build a self-contained executable for Linux
dotnet publish -c Release -r linux-x64 -f netcoreapp2.2
#### NUGET
Create a nuget package
dotnet pack
Publish a nuget package
dotnet nuget push

#### GLOBAL TOOLS
Install a global tool
dotnet tool install -g [TOOLNAME]
Uninstall a global tool
dotnet tool uninstall -g [TOOLNAME]
List all globally installed tools
dotnet tool list -g


### Git Cheat sheet reference


[ it Cheat sheet reference](https://education.github.com/git-cheat-sheet-education.pdf)
 



### SETUP
Configuring user information used across all local repositories

git config --global user.name “[firstname lastname]”
set a name that is identifiable for credit when review version history
git config --global user.email “[valid-email]”
set an email address that will be associated with each history marker
git config --global color.ui auto
set automatic command line coloring for Git for easy reviewing



#### SETUP & INIT
Configuring user information, initializing and cloning repositories
git init
initialize an existing directory as a Git repository
git clone [url]
retrieve an entire repository from a hosted location via URL

#### STAGE & SNAPSHOT
Working with snapshots and the Git staging area
git status
show modified files in working directory, staged for your next commit
git add [file]
add a file as it looks now to your next commit (stage)
git reset [file]
unstage a file while retaining the changes in working directory
git diff
diff of what is changed but not staged
git diff --staged
diff of what is staged but not yet commited
git commit -m “[descriptive message]”
commit your staged content as a new commit snapshot

#### BRANCH & MERGE
Isolating work in branches, changing context, and integrating changes
git branch
list your branches. a * will appear next to the currently active branch
git branch [branch-name]
create a new branch at the current commit
git checkout
switch to another branch and check it out into your working directory
git merge [branch]
merge the specified branch’s history into the current one
git log
show all commits in the current branch’s history


#### INSPECT & COMPARE
Examining logs, diffs and object information
git log
show the commit history for the currently active branch
git log branchB..branchA
show the commits on branchA that are not on branchB
git log --follow [file]
show the commits that changed file, even across renames
git diff branchB...branchA
show the diff of what is in branchA that is not in branchB
git show [SHA]
show any object in Git in human-readable format


#### SHARE & UPDATE
Retrieving updates from another repository and updating local repos
git remote add [alias] [url]
add a git URL as an alias
git fetch [alias]
fetch down all the branches from that Git remote
git merge [alias]/[branch]
merge a remote branch into your current branch to bring it up to date
git push [alias] [branch]
Transmit local branch commits to the remote repository branch
git pull
fetch and merge any commits from the tracking remote branch

#### TRACKING PATH CHANGES
Versioning file removes and path changes
git rm [file]
delete the file from project and stage the removal for commit
git mv [existing-path] [new-path]
change an existing file path and stage the move
git log --stat -M
show all commit logs with indication of any paths that moved


#### REWRITE HISTORY
Rewriting branches, updating commits and clearing history
git rebase [branch]
apply any commits of current branch ahead of specified one
git reset --hard [commit]
clear staging area, rewrite working tree from specified commit

#### TEMPORARY COMMITS
Temporarily store modified, tracked files in order to change branches
git stash
Save modified and staged changes
git stash list
list stack-order of stashed file changes
git stash pop
write working from top of stash stack
git stash drop
discard the changes from top of stash stack


#### IGNORING PATTERNS
Preventing unintentional staging or commiting of files
git config --global core.excludesfile [file]
system wide ignore patern for all local repositories
