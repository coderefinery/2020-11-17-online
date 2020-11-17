---
permalink: /hackmd-day1/
---

# 2020 November CodeRefinery HackMD, day 1

## Links

- Course page: https://coderefinery.github.io/2020-11-17-online/
- Schedule: https://coderefinery.github.io/2020-11-17-online/#schedule

###### tags: `workshop`


## Icebreaker

(tentative) What’s the most important thing you’d like to learn this week?
- Reproducible research and FAIR data
- How to create and maintain scripts that to be used by many people during and after a project
- Modular software development (CMake?)
- How to better use git, learn how to do unit testing
- Better understand git
- How to manage versions when working on the same project and scripts with multiple people
- Small details and tricks unknown before about keeping a code workflow either personal or in a group
- New tricks and also learn about what others are working on
- Learn more about the tools, reproducible research, reusability, maintainability, workflow, and learning through helping
- Learn code developemnet using git and push to github, version control
- Workflow and organization for collaboration at UiO
- Being able to organize my scripts etc. in a way that is reproducible for myself and others.
- Best practices and python environments
- Fixing wrong commits/pushes as clean as possible
- Social coding and modular code development
- Basic use of GIT for developing scripts and programs as a team.
- Learn about debugging techniques and how to write sustainable documentation of code.
- Convince myself to move towards a more flexible and valuable way of working
- How to use use git effectively with a large working group
- Reproducing research workflow with `snakemake`.
- Managing a collaborative coding project on GitHub
- Understand how git works
- Learn how to master git
- Learn best practices on collaborative coding
- Improve my coding skills and learn new ways of collaborations. Version control skills.
- Make my code usable for others
- Reproducible research and collaboration
- How to best document my code
- Learn about create reproducible scrits for my work
- Undoing things
- Being able to use git better on terminal, and make good documentation
- Get inspiration about how others use these tools, and consolidate practices. There is always room for new knowledge and inspiration. Specially about project structuring and documenting tools in practice.
- While all the different topics are interesting, it is good to learn new stuff in a structured way and interact with other people (homeoffice gets boring after a bit)
- Using git for maintiaining my research code.
- Some best practice and tips and tricks when using version control!
- Three objectives: act as helper for my colleagues, practice virtual education, interact with other different people


---
## Introduction
https://github.com/coderefinery/workshop-intro/blob/master/README.md

- Do you guys want us participants to have video turned on or off on the zoom?
    - Either is ok.
    - We are neither recording nor streaming this workshop so it's fine to keep the video on.
- What tools for drawing on screen is Sabry Razick using? They look amazing
  - It's amazing. Sabry has built a plexiglass board for this, lit from the side, and promised that he will open-source his setup :-)
  - Mind blowing!
  - Long live DIY!
  - Wonderful work!


## Introduction to version control with Git
https://coderefinery.github.io/git-intro/01-motivation/

- What problems do you anticipate with this kind of version control?
   - Which would be the 'original' version?
       - I'm not sure exactly what this refers to, can you elaborate?
   - What to merge to what, and what is actually supposed to be kept in the document?
       - we will talk about branching and merging later and you will practice it!
   - What if I find a bug and want to know where/when it was introduced?
       - we will learn very cool methods to hunt bugs in git history tomorrow!

- What are the main differences between snapshot based versioning and patch based versioning ?
  - The difference is whether the tool internally stores entire snapshots or only stores differences (patches). Git actually does not store differences but entire snapshots but it does it in a very efficient way (storing them in a tree). When we ask Git to show us a difference between two versions, this difference is computed on the fly, not stored.

- What is the difference between a branch and a fork ?
    - we will learn it 
    - branches are development lines within the same repository
    - a fork is a copy of the entire repository, copying all branches
    - you use a branch when you e.g. want to add a new feature to your repository, while you typically use a fork to make a copy of an entire repository (particularly useful for external repositories with hundreds or thousands of users)

- What happens if we fork and the original project is moved out of the GitHub, e.g. moved to GitLab or moved offline?
    - for a public project: nothing happens to the fork, the fork still stays there, maybe the "forked from X" disappears
    - for a private project: if the original repository is gone, the fork is gone (at least this is how it was some time ago)

- Saving a snapshot of the entire project every time, doesn't that require a crazy amount of disk space??
    - that's indeed what you might think, but Git is very clever about what it stores - it doesn't store full copies but only the incremental changes
      - I don't think it stores incremental changes but it chops the files into chunks and stores them efficiently in a tree, so it does not store same chunks twice. For big binary files this works less well so Git may not be ideal to store e.g. videos or large binary files. For the latter, git-annex is interesting.

- What is the rectangular highlight tool that was used to highlight some portion on the screen? It looked like a semi transparent window.
  - This is a plexiglass board, lit from the side. Home-built.
      - Cool, this workshop turned more interesting and attractive! Thanks.



### Basics
https://coderefinery.github.io/git-intro/02-basics/

- I was wondering if the illustration used by Sabry was correct... You don't have to "git add" again for version v2 after you edit a file. Is that correct?
    - the figure is correct, after each edit you need to `git add` *and* `git commit`
    - we will learn why Git works this way
       - Does this mean: edited, did `git add`, but did not commit, then edited again, then we need to do `git add` again, right?
            - yes. this extra step gives you the option to undo the "edited again" if you realize this was a mistake.

- What is the “cost” of creating and maintaining a folder with git? Would it take extra memory or take up some computation capacity of my computer? Is it negligible?
  - it is negligible almost always so I recommend to always create it. The space occupied by .git will most of the time be not more than that occupied by  the code/scripts/data, since it stores snapshots compressed.

- Can you teach us how to clean up git folders and Github repositories?
  - GitHub repositories: go to "settings", scroll down to "danger zone"
  - git folders on your computer: if you remove the .git folder, then the Git repository and all its history is gone

- Sorry, but I missed the answer to this question: They are not just integers counting 1, 2, 3, 4, … (why?).
  - this would be ok for a centralized system but Git is distributed (although up to now we only use it in one place) and then different people doing different changes would not agree on who can call a version "4". there would be clashes. so instead the commits have a unique identifier. same commit identifier means: same changes, same history, same author.
  - note that named/labelled/numbered versions are still possible through "git tags".

- What's the difference between the diff and difftool? Can't seem to get it set up to vscode.
  - git diff puts the difference into "standard output" (into the terminal). this is ok for small changes but it can be a bit inconvenient to inspect changes that go over many lines and many files. for this, visual side-by-side comparisons such as git difftool can be nice where you can scroll through changes. this is convenient to compare larger changes.

 

### Breakout room until XX:35
Exercise goal: 
1. Go through the type along (what the instructor did)
2. Exercise: record changes

#### Group status (please type how you are doing)

- Group 2: finished
- Group 3: exercise completed, some moved to the optional part 
- Group 4: finished, now in optional exercise
- Group 5: Finished
- Group 6: Finished. All fine
- Group 10: working along! Participants are starting the excersise
- Group 11: proceeding ok with exercises, optional exercises now
- Group 13: finished, doing the optionals
- Group 15: finishing exercise 1 soon. all fine.
- Group 16: all finished the base exercise, some optionals
- Group 17: all going well, 4/5 working on the optional exercises
- Group 18: all fine.
- Group 19: all fine too. Exercise 1 is done


### Break until xx:45


- problems with `git add .`
  - accidentally adding files which should not be tracked by Git, example: generated files, .pyc files, compiled files
      - I'd argue that's less of a problem if you are in a source only folder, and check status before committing
         - agree. I use this when starting a project. And I agree that in combination with `git status` it can be used in a safe way. But I have also seen repositories containing generated/compiled files because the repository did not have a clear separation of sources and generated files.
        - Why is it bad to add files which have not been modified?
            - It might be a bad idea to add files that should not be tracked, either because they are big or should not be shared with others who look at your repository (e.g. on GitHub)
            - but if this is a tracked file, then there is no problem. in fact, nothing will happen to that file in this case.
  - possibly better: autocomplete with tab
  - another alternative: `git add -u`: will stage all modified files but in contrast to `git add .` it will not add files that are untracked :heavy_check_mark: 

- I have seen some groups use emoji to tag commits. Like :sparkles:  for features, :scroll:  for documentation, :ambulance: for quickfix etc. Think it's quite convenient (can't always be displayed nicely though).
  - interesting! sounds fun!



### Using the Git staging area
https://coderefinery.github.io/git-intro/04-staging-area/


- with rm command, do you completly remove the file or does it get back to its last stage?
    - I guess it won’t really remove it until you commit 
    - `git rm` removes the file from your working directory and from the git repository (but you can restore it later if needed since it's part of the history)
        - It does not seem to be true in all cases. For e.g. if one removes the ingredients.txt file and commits the change. In the next commit if the same file is added and committed, the git history of the file will begin from epoch 0. (Please correct me if I'm wrong)
            - no you're right, this happens if you create the file again from scratch. But you can **revert** the `git rm` commit, which simply does the exact opposite (i.e. creates same file again, preserving its history). We'll learn to use `git revert` soon
    - and you mean `git rm`, not `rm`, right?
        - good point, if you do `rm file.txt` and `git status` you'll see that a tracked file has been removed. If you then `git add` you'll stage the removal (so this is equivalent to `git rm`). But you can also undo the `rm` by `git checkout file.txt` (as we'll see soon in this episode)

- When is it recommended to use `git stash` (i.e. working with the philosophy of patches: `git stash pop`, `git stash push` etc...) vs `git branch`? I ask this question since I often have issues while merging multiple branches (given that I branch often.) Are there standard recommendations/best practices ? :+1: x2
  - I used to use `git stash` to hide away messy changes to do something else quickly. But I stopped doing that because I then forgot about the stash and coming back to the repository 3 weeks later `git status` looked good and I deleted my changes. So these days I always prefer to put messy code on a side branch.
      - I initially also used to use `git stash` to hide away unwanted changes. Then I actually tried to use the feature as a new concept which is useful when working on projects with multiple branches. It helps to avoid a lot of merging and promotes a modular commit philosophy I suppose. 
  - I use `git stash` sometimes if git prevents me from switching branches but where I know that it should be possible. Then I stash, change branch, then unstash. But often this is not even necessary.
  - I am using worktrees more and more, one to have my local work in progress (WIP) branch, another to actually commit/push to remote. This requires cherry-picking from one branch to the other, so it's a bit advanced - you definitely want a visual interface.
  - Would love for you to talk about in the call :+1:

- What about subfolders in a git-project?
  - A folder is similar to a file. If you add a file in a folder, that folder will appear as well. You can ignore full folders with gitignore. 

- Unstage the staged changes means? Do I remove the changes in the file manually?



### Undoing things
https://coderefinery.github.io/git-intro/05-undoing/

- is it possible to correct a commit message after the commit? (e.g., if there was a typo or something)
    - `git commit --amend` if you want to fix the last commit
    - it is possible to also change commits in the past with an interactive rebase
    - note that both above are history-changing commands which will change the commit identifier. Fine to do for work which I haven't shared, but I should be careful doing this on commits that other people already depend on.
    - basically, everything that was not pushed to a remote can be edited safely.

- Once I accidentally added an image (big file) and commited and pushed. Then everyone in the project all of a sudden had to download a big repository even if I removed the image. How can I obliterate the existance of that file? like from history, forever without a trace?
  - in this case the file stayed in the history. it is possible to rewrite history and remove commits/additions with `git filter-branch` or using interactive rebase. The difficulty in doing this is that everybody else in the project needs to be informed and they need to update their copies, otherwise your change might come back again because somebody else had it in their history and did not update their copy.
    - Thanks! and how do they update their copies? do they just pull? or need to run the same commands as me?
      - they don't have to reapply the same changes as you but a `git pull` is probably not enough since `git pull` will merge your new history with their old history. they should 1) make sure all their uncommitted changes are somewhere saved and 2) better do a fresh clone after the rewrite.
  - this is where it get's dangerous ;) Some repositories might not allow you to.
      - After this experience I learned to be very careful and use .gitignore better ;)
        - also `git status` helps and using code review (sending all changes via pull/merge requests so that somebody else can check the change before it is integrated; more about that on Thursday) 
  - github's tutorial on how to revise your history  remove unwanted files - https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/removing-sensitive-data-from-a-repository

- question: I'm trying to revert deleting a file with git rm but it doesn't seem to work
    - this should work: `git rm somefile.txt`, `git commit -m "removing file"`, `git log --oneline` (to find hash of commit), `git revert <hash>` 
    - that gave: error:
    
    ```
    Reverting is not possible because you have unmerged files.
    -hint: Fix them up in the work tree, and then use 'git add/rm <file>'
    -hint: as appropriate to mark resolution and make a commit.
    -fatal: revert failed
    ```

    - this error means that you want to undo a removal but something else happend with the file later so it cannot bring it back to the state without undoing what happened later, so it stopped. Or: something else is up. In this case we need to see `git status`.


- so... git checkout update your version against the repository, right?
    - we will cover checkout later. It is a command to switch between branches, but can also be used to restore a file to the last committed version
    - bring a path back to last committed or last staged version

- Do you know whether geospatial raster files are binary files, and thus best not use Git for their version control? (practically speaking, they are just images)
  - Basically, they're data. They do not change on a line-by-line basis. So I'd advise not to check them in, unless you have git big file support.
  - git-annex might be interesting. How large are the files? Do you have some example for these files? (with git-annex you can track metadata while storing the data itself somewhere else; see also a session on `git-annex` we did in https://researchsoftwarehour.github.io/sessions/rsh-012/)
      - I'll search for en example that I will be using

- How can I move folders from one directory to another?
  - `git mv folder1 folder2/anothername` followed by `git status` and `git commit`. With `git mv` we can move move and rename files/folders.
      - Thanks!

- And what if the folder I want to move is the repository folder?
  - then you can move the whole thing and it will still work. All the history is in the `.git` subfolder and this one fortunately uses relative paths and not absolute files so the whole repository can be moved. This by the way, is what happens when we `git clone` (tomorrow), we copy the whole thing.

- Most basic folders on my laptop (i.e. desktop, documents, etc.) are automatically already stored in OneDrive. Many project files are stored in Google Drive or other cloud services like Box. Is it a problem to initialize a git folder in a cloud folder? Does that defeat the purpose of a Git repository?
  - great question. I think it is not a problem unless you start sharing a project with other people using both onedrive/dropbox/somecloud *and* Git/GitHub. But I think it won't be a problem if I keep the onedrive for myself and share the Git repos using Git. Then also make sure to ignore (`.gitignore`) files generated by the other storage/versioning solution.

  - I have had bad experience with cloud-shared folders as development environments. The watchers sometimes do not keep up with the changes and may interfere destructively with each other
    - good point. in practice I store all the git repositories on GitHub/GitLab and not on other clouds-shared folders and use the latter only for non-git projects and document writing. 

- I have a python project with my main code in my working directory and several modules in my user directory. At the moment I only have one preject on the go so all of the module are being used by only one source code. Later I expect to use them for multiple projects. Should I have a git repository for each one of the modules, and my source code? So in this example, 4 folders with 4 git repositories for a single project?
  - just to check I understand the problem: the modules do "unrelated" things but at the moment are used in one git repository because at the moment they are only used by one project? and in future there will be more projects, possibly only using some of the 4 modules? If you have a link to the (github?) repository, it will also help.
  - This might be a use case for submodules, if I understand the setup correctly. Basically, you can link one git repository into another one, kind of like importing it. That way, the general code can be included in several repositories.
 - Sorry, I have custom made modules which are stored each in their own folder. So I initialized a git repo in each folder, so I have 4 git repos for 1 project (my main code cal these modules).
   - if you like we could look at this in a breakout room/ screenshare and give comments/recommendations 
   - answered in breakout room: one option is git submodules (to nest git repositories), another option is to create conda/PyPI packages from the dependencies and to include them into your project using `environment.yml` or `requirements.txt`.

- I don't understand what the point is of staging ("add") before intending to commit and while still working on the file
  - to record a change it would be enough to do `git commit filename` so the staging/adding indeed seems like a redundant extra step. The advantage of maybe later using the staging area is that you can "save" an improvement and still continue working on the improvement before making a commit. I use the staging area to "prepare" nice, well defined commits and to collect related changes. But it is perfectly OK not to worry about this from the start. Better too many commits than too few.
    - thanks! I wasn't asking why have two steps -- I see the point of collecting multiple revisions into a commit that has a specific purpose; the question was about incremental staging when one is not ready to commit (e.g., a change that is incomplete, untested etc.). This refers to your "working on an improvement before making a commit": why stage that at all?
      - ah OK, yes. I would stage changes that "made something better". So maybe that was indeed not a good example. I use: staging everything that was an improvement, checkout everything that made things worse. So it can makes sense to stage something incomplete if it made things better. And why staging then? Because if I mess up after the staging, I can go back to the staged version. So I can go back one step, even before having committed the change.

- after doing "git chekout ingredients.txt" ingredients.txt still appears on the list of changes to be commited on git status
  - yes. `git checkout` will undo modifications that were not staged. In other words it will bring the file back to a state as it was staged. If the file was not staged, it will bring it back to the last committed state.
      -  ok- so if I stage it then make another change, git checkout returns to the staged version?
        - yes
 

### Break until xx:33


### Exercise after the break:
https://coderefinery.github.io/git-intro/04-staging-area/#exercise-using-the-staging-area

- So just to confirm- when you use diff, it gives you the difference between what you haven't staged and it's previous commit, whereas diff --staged  gives you the difference in the file that you added. Is that correct?
    - yes, “git add —staged” shows difference between staged version and last committed version 
    - it's nicely sumamrised in this illustration: https://coderefinery.github.io/git-intro/img/staging-basics.svg

- How to remove a mistakenly committed file like API keys entirely from git history?
    - there is a discussion about this further up, but in short: either interactive rebase (`git rebase -i somehash`; the `somehash` should be a version some time before the commit you want to edit) or git filter-branch (useful to remove commits that modified a certain path). both commits are history-changing, so please see above discussion about risks when working with others who might also have to update their histories.

- git reset was supposed to revert the added modification, e.g. remove "to be staged" from the file, no ?
  - yes, `git reset` can be used to "unstage" changes 

- What does "updated 1 path"  mean?
    - where did this show up?
        - as an output of one of the command Sabry wrote towards the end of Day 1 of the workshop, when discussing about checkout

- `git reset --hard` : The commit is not visible any more, but it is not removed. You can still checkout if you know the SHA.

- Some learners were confused what the difference between `git reset` and `git checkout` are - they tried to use `git checkout` for unstaging.
    - `git reset` was used for unstaging changes. `git checkout` is a versatile tool that can be used for several things, for example to switch between branches, switch to a specific commit, or go to a specific version of a file.
    - We will learn more about `git checkout` tomorrow.

**Exercise: Using the staging area**
What was your commit message ?



### Feedback

Please write down one thing you liked and one thing we should improve

Good:
- I am very fond of the 'practical' and explanatory approach. And it is very useful to have the instructor's command-history :+1::+1:.
- useful material presented in a pedagogical way via code-along and interactive exercises (it's also very nice to see the command-history of the instructor)
- Nice to have all materials and exercises online :+1::+1::+1:
- I liked the exercises, they were concise and self-contained (and instructive)
- It's great to have small groups
- Great set up for drawing and good choice of illustrations !

To improve:
- I feel it's hard to both monitor this pad while also listening to the talk :+1::+1:
  - And then not all questions will make it into the call
- It would be good to see more of the instructor's command history. I can only see one command back! maybe the instructor's command log could be put online?
    - Command history transcript (https://docs.google.com/document/d/1VQ4lUr1hrrKQwOAYa2z0h-0xltBm1PEuQLY8VksWk7c)
    - Excellent! 
- It would be helpful with a summary of the key points before and after each lecture/module :+1:. Before so learners know what to expect/see the read thread, after to repeat/know what the most important take-home message is.
- Please, scroll webpages a little bit more slowly
- It was a bit to messy and fast for a newbeginner like me
- I dont know the audience but maybe using a console is not the easiest for beginners. But I use it. And I also use VSCode and it's git UI.
- I felt that the undoing things part was a bit fast.


### Installation issues
- I have an issue with the opendiff graphical interface, as it will not start. I am running git on MacOS. Apparently there are some issues that require the installation of XCode, which I am currently doing. I get this error: `xcode-select: error: tool 'opendiff' requires Xcode, but active developer directory '/Library/Developer/CommandLineTools' is a command line tools instance`
    - Alright, installing XCode sorted my issue, and now opendiff works.


:::info
*Always ask questions at the very bottom of this document, right above this. Switch to view mode if you are only watching.*

*We are monitoring this hackMD, but we will reply every now and then so that you can focus on the speaker.*
:::
