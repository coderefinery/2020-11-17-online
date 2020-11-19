---
permalink: /hackmd-day2/
---

# 2020 November CodeRefinery HackMD, day 2

## Links

- Course page: https://coderefinery.github.io/2020-11-17-online/
- Schedule: https://coderefinery.github.io/2020-11-17-online/#schedule

###### tags: `workshop`


## Icebreaker

(tentative) Name the most important thing you learned yesterday

- I found the whole "Undoing things" section very useful since this has been a bit of a knowledge gap for me. :thumbsup:
- I liked that we focused on everything related to the local copy only, without immediately introducing the push/pull concepts.
- Some commands were explained very well, e.g. git checkout and git add -u.
- Staging area was explained well
- Splitting of chuncks with `git commit -p` :+1:
- The use of the staging area as a moving-box
- The `--staged` flag to `git diff`.  :+1:
- The basics of staging and committing, well explained, and hands-on practice.
- Really enjoyed some of the commiting options e.g. `git commit -p`. Also the difference between `checkout` and `reset`
- the 'undoing things' section was super interesting and useful
- The structure of local state, repository, staging area etc. within the logical structure of git
- Motivation for using version control, and why the staging area is useful
- Not been able to attend Day 1 but from the materials I learned about the commands `git commit -p` and `git diff --staged`. Excellent pedagogically organized material
- Nice octopus example!


## Feedback/suggestions from yesterday

- comment on yesterday's page "Undoing things"  (I thought this went by a bit fast by the way): (1) In "Exercise: Modify a previous commit" step 3, it says "add to the previous commit with git commit --amend". It is implied that the new changes must have been previously staged with git add, which is obvious to an experienced user but not to a newbie. I would add this instruction (i.e., to use git add before the new git commit). (2) In "Test your understanding" at the end, there are two questions on HEAD and HEAD^ which I do not recall being mentioned at all yesterday. I don't think we've discussed HEAD at all (or even master, but I guess master is today's topic)
  - thanks for both comments, we will adjust (1). for (2), `HEAD` was mentioned briefly at the end (the casette tape analogy) but indeed this question perhaps arrives too early. I am noting these good points as issues so that we follow up: https://github.com/coderefinery/git-intro/issues/267 and https://github.com/coderefinery/git-intro/issues/268

---

## Branching and merging
https://coderefinery.github.io/git-intro/06-branches/

- Regarding the octopus example: What if glasses and hat are incompatible? E.g., they both need "forehead space"? How do we then join/merge glasses and hat?
    - We will talk about that [later today](https://coderefinery.github.io/git-intro/08-conflicts/)
- I'm still a little confused about the parent concept. Will we be coming back to it?
    - the previous commits on connected branches are parents to following (next) commits.....
    - parents to immediately following commits, ancestors to all following commits on continuous branches 
    - each commit has at least one parent commit, except the first commit (the initial commit).
    - some commits have two parent commits: these are **merge commits**.
- git bash has a nice display showing the name of the branch. I have found it very handy. +1
  - nice! it has this on by default? or did you have to install something on top?
      - default in Git Bash on Win
      - confirm, no additional actions for git bash
- Can we create parallel branches to master, i.e. not as a branch from it? +1
  - you mean a branch which does not start from master but starts from "nowhere"?
    - yeah, starts from "root".
      - you can create `--orphan` branches, where the first commit of the branch has no parent: `git branch --orphan somename`
          - Will it be possible to merge it then?
          - A concrete unfortunate example (Don't try this at home:) ): Somebody copied a repo (without .git folder), did changes, created a new git repo. Is there any trick to be able to merge that "orphan" repo to the origin?
             - It is possible to merge orphan branches by providing `--allow-unrelated-histories` option (https://git-scm.com/docs/git-merge#Documentation/git-merge.txt---allow-unrelated-histories)

- Can we have the list of pre-requisites for the current execise written somewhere e.g start with a clean history, create branch etc.
  - good suggestion, we need to not assume that participants still have the repository from yesterday, noting this: https://github.com/coderefinery/git-intro/issues/269
  - `mkdir recipe`
  - ` cd recipe`
  - `git init`
  - now create two files: ingredients.txt and instructions.txt from https://coderefinery.github.io/git-intro/02-basics/#type-along-tracking-a-guacamole-recipe-with-git
  - `git add` both files, then `git commit`

- Can you please quickly re-explain the head concept again? 
  - `HEAD` is our current position, in analogy of the recorder head for those who remember casette tapes. when we switch branches with `git checkout somebranch` or `git switch somebranch`, then `HEAD` moves over to that place.
  - `HEAD` typically points to a branch (and a branch is like a sticky note pointing to a commit hash). But `HEAD` can also point directly to a commit hash and in the latter case we have a "detached HEAD" state.


What to do 

1. define git graph (https://coderefinery.github.io/git-intro/06-branches/#a-useful-alias)
2. Then create a branch called experiment https://coderefinery.github.io/git-intro/06-branches/#creating-and-working-with-branches


Solution of the above ex:

1. go to the directory you have been using yesterday (the guacamole recipe)
2. define the graph alias: `git config --global alias.graph "log --all --graph --decorate --oneline"`
3. make sure your directory is clean/ commits: `git status`
4. create a new branch called experiment from master: `git branch experiment master`
5. switch to the experiment branch: `git checkout experiment`
6. view your branches: `git branch`

---


## Excercise: (until xx:55)
https://coderefinery.github.io/git-intro/06-branches/#exercise-create-and-commit-to-branches

- **Stop before merging**
- At the end you want to have 3 branches
- Also make sure `git graph` alias is defined and works
- Your `git graph` should produce a graph similar to the picture in this exercise

- I don't understand why HEAD would point to `experiment` after committing changes to `less-salt`?
    - I think they did not write all the commands in the exercise to get to that point
    - Are you referring to the picture in the material?
        - Yes!
          - good point, I see how it can be confusing. We need to adapt that picture: https://github.com/coderefinery/git-intro/issues/270. I think at some point we have changed the exercise without adapting the picture.
            - Good suggestion! This has confused learners in previous workshops as well.

- is it possible to visualise an entire tree with the gitk command? I only see the branch that is active at the moment (with all comments, but without other branches even when on master)
    - The `git graph` alias should show the whole tree. If the tree is big you can scroll it with arrow keys, `q` returns to your command line. 
    - I got it how to use `git graph`, but gitk allows to visualize longer trees in a GUI so I was wondering if there is patch to visalize it with all branches and not only the current one. git graph is awesome, but having a GUI is also good sometimes

- On the figure just below the octopus, the labels of commits are c1, .., m1, d1, etc, where 'm' refers to merge. In the figures below, 'm' refers to master. It might be a bit confusing. 
  - good point, thanks for that. noting this so we change/clarify it: https://github.com/coderefinery/git-intro/issues/271
  - ;-)


## Break until xx:07/


## Merging branches https://coderefinery.github.io/git-intro/06-branches/#merging-branches

- In larger projects with a lot of files, does it take some time for Git to update the working directory when I, for instance, switch between branches with a lot of differences?
  - This is basically "instantaneous", I have never noticed a lag when switching branches. The operation corresponds to extracting compressed files from .git and putting them into your working directory. But this is implemented very efficiently.

- Can we create a new branch from a previous or any commit hash (e.g `git branch new-branch 2e70ce4`)?
    - yes! we'll look at use cases of this in the archeology episode "Inspecting history"

- how do we know that deleting a branch is safe?
  - Git will not let me delete a branch with `git branch -d` or `git branch --delete` if the commits have not been merged to another branch.
  - But you can force Git to delete it anyway with `git branch -D`
  - Reminder that branches are like sticky notes, when we delete branches, we do not delete commits. But in order to find commits, it's good if they are part of some branch. 


Merging branches on your own until: XX:22 

- how does one "cut away" a branch / create a new repository for a given branch that keep the history of that branch? Maybe one could `git remote...` and `push` and then delete the branch?
  - I would create a repository on GitHub/GitLab (later we will see how) and then push only that one branch to the new repository: `git remote add origin someurl; git push origin thatonebranch`. Then you have a new repo and only that branch in there with all commits on that branch. And after that, indeed you can delete the branch on that original repository.
    - Thx. Just wondering if there was an alternative solution.
      - Assuming your original repo is somewhere on GitLab/GitHub, you could also import it into a new repo, in the new repo you delete all branches except one, in the original repo you delete that one branch.
      - If you do everything manually by command line, you have to set up both a remote of the repository (the GitHub/GitLab repo), and set/create upstream branches for your local ones. So you could well add a second remote, set the remote of your `cutaway-feature-branch` to `master` of the remote. Then you can clone the new repo anew and delete the cutaway branch in the original repo. This can get messy, since we're used to have only one remote, and remote branches to be named exactly as they are locally.
        - on a laptop you could also `cp -r` the repository folder to a new folder and you delete the branch in one and delete all other branches in the other.

- what if somebody changed only the first word of the line and somebody else changed only the last word of the line, is it still a conflict?
  - yes, Git looks at line modifications, not at "words"
  - this also means that if you want to put your manuscripts or a document in Git, it's good if the lines are not too long to minimize the risk of conflicts. You can configure your text editor to wrap long lines. 

- Are the file formats for which `diff` does not work, in the context of merging commits? Will it just check the checksum and report a conflict if the files are different? Or are there some useful tools for non-text files?
    - with non-text files git will not be able to compare versions and merge them, so if you get such a conflict you will need to select which version you want to keep (the one on current branch or the one on the branch you're merging)
    - in this case if the two modifications have a different checksum, it is a conflict

- Why there was no conflict on the first merge with like-cilantro to master ? It was also targeting a change in a line with cilantro. However, only the second merge raised a conflict
  - because that line was not modified on `like-cilantro` and `master` in two different ways before that merge. only after we have merged `like-cilantro` we have a modification of that line on `master` and the second merge will conflict. Please let me know if this explanation was not helpful enough and we expand.
  - **follow-up:** I still don't get it: The line has also been changed in master, just not in the directly previous commit but some time earlier. Does git only look at changes in the directly previous commit on the file to be merged? Or does it look at timestamps to give one version precedence? Why would it overwise choose the `like-cilantro` version over the `master` version? 
     - The first merge did not conflict because the earlier change was an ancestor of the later change. In this case it assumes that the later change was intentional and there is a clear ordering of changes. The second merge conflicts because the change on `less-salt` and `experiment` are topologically not ordered but happened "in parallel". In this case Git does not take the later change in terms of time stamp but it compares whether they are related in terms of "ancestry". Please do not hesitate to raise this issue if it is not clear or not well explained.

- I managed to make 2 consecutive merges on a same line without having a conflict. Does it depend on the position of the HEAD?
    - it could be that you did not merge both branches into the master branch, because it *should* conflict if you modified same line in two different branches

- I have the opposite question from above: Why was there a conflict after the first merge? The result of the merge was a 1/2 cilantro (applying dislike-cilantro over master) and master had now a revised content, master is now 1/2. What's the problem with just merging in like-cilantro and revise master to 2? I mean, dislike-cilantro is gone now (merged into master). It's clear that two branches applied conflicting edits. The question is, why is this still relevant after one of the branches has been merged into master? What's wrong with this desciption?
    - Thinking about the answer to the above some more myself it seems that the answer is something like: master and like-cilantro have conflicting edits because master inherited the dislike-cilantro edits, so it is not just edited to a new state but carries along the edits from the merged branch that brought it to that state. Does this make sense? If yes, I have answered my own question :-)  If not, please help!


## Conflict resolution: https://coderefinery.github.io/git-intro/08-conflicts/

Create two branches as the instructor showed 

- i.e. all the steps under https://coderefinery.github.io/git-intro/08-conflicts/#type-along-create-a-conflict
- change to master (as described in above link) and merge the first branch, that should go smooth
- try to merge the second branch and you will face a conflict, resolve it manually as described
- Ask for help if you need it on the chat or here 


- When I try to resolve the conflict I get:
  ```
  error: Merging is not possible because you have unmerged files.hint: Fix them up in the work tree, and then use 'git add/rm <file>'hint: as appropriate to mark resolution and make a commit.
  fatal: Exiting because of an unresolved conflict.
  ```
     - if you have resolved the conflict, you need to tell Git that the conflict is resolved by `git add somefiles`. In other words we signal conflict resolution by staging the change. From the error I guess the staging did not happen?
          - Had to commit after resolving and adding.

- In the nice optional exercise moving commits to another branch: when we make a mistake and commit to the wrong branch, and we do `git reset --hard` don't we lose the changes introduced in the commit?
  - assuming we have created the new branch before doing the `reset`: `git reset --hard` moves the branch to a commit in the past. But the commits are still there and they are now reachable via the newly created branch.
  - However, if I accidentally did a `git reset --hard somehash` before "saving" the commits to a new branch, I will have a hard time finding these commits again. In fact they have not been deleted and I can recover them with the help of `git reflog` which keeps a log of all commits you have visited, for some time.
  - Please let me know if I misunderstood the question :-)
  - That is it thanks!

- After 'git diff', which is the command to solve the conflict?
    - you need to go into the file and edit it manually (remove conflict resolution markers and choose what version you want), and then stage the file: `git add`. You can then type `git commit` and you will have a pre-filled commit message
    - by staging the file you are telling Git that you're done solving the conflict - Git won't mind if you accidentally left resolution markers in the file!
    -Done! Thanks
    Once I solved the conflict, can I delete the unnecessary branches?
      - yes, once branches have been merged, they can safely be deleted

- Can you increase font size in left terminal?
  - thanks for pointing it out


## Sharing repositories online
https://coderefinery.github.io/git-intro/09-remotes/

- please emphasize that the name of the remote repository should be the same or am I wrong?
  - yes, it matches the lesson material better if you use the same name

- How to update desktop github? Is made automatically?
  - you have created a repository on your computer using github desktop and want to put it on github? or the reverse: you want to clone a repository from github using github desktop? 
  - Clone the repository in the desktop: (already know how to do this, thanks!)
    - great! I was looking for a screenshot but nice you solved it.

- It is very annoying that GitHub defaults to `main` instead of `master` for the name of the master branch. It is possible to change it in the personal settings of your account in the "Repositories" tab, and restore the default to master for new repositories.
  - Indeed this adds a bit of confusion to our material that locally Git defaults to `master` but now GitHub defaults to `main`.

- perhaps running `git remote -v` initially would be good idea before adding the remote link
  - yes indeed

- I get this error: `fatal: remote origin already exists.`
  - in this case you tried to do `git remote add ...` with a remote already defined. You can remove the remote with `git remote rm origin` and then try again and it will work. `origin` is a placeholder and we will explain tomorrow what this really means. :ok_hand:

- I get no authentication prompt at all. 
  - with using https protocol?
      - Different person here, but I also didn't have to put in a pw or username. Using https on windows. I have used github in the past and have serveral repos set up, never needed a pw but I followed the set up instructions just like on screen.

- for me, the "Git Credential Manager" pops up 
  - probably this is macOS? this is fine, hopefully it works then also this way
  - no, it was Windows. But yeah, it worked fine.

- Are there steps to follow somewhere? I was not able to follow along because I had a remote issue
    - yes the steps are documented here: https://coderefinery.github.io/git-intro/09-remotes/ 

- I get an error saying that the push would publish a private email address. How can I resolve this wihtout making my email Public? 
  - the way I solve it is that I defined my local git email address to be `myusername@users.noreply.github.com` (replace `myusername` with your github username). This way, nobody can write you to that address but GitHub will still be able to count your contributions.
      - yes, I did that. But I still had to turn off the *"Block command line pushes that expose my email"* option on GitHub. But I guess this is no problem now since I use the github-noreply email address.
  - this warning/error shows up if you have configured your local git to use a different email address than on github. although github will make sure the email addresses cannot be easily harvested through their web frontent, public repositories can always be cloned and inspected with `git log` so if you don't want your email address to become visible at any point for nobody, you can use the above answer.
    - this worked for me: `git config --global user.email=gitusername@users.noreply.github.com` (replace "gitusername")

- I've wrote the origin path for sabryr his repository and now I can not changed it?! bHow to remove this connecction and the connect to my own repository at GitHub? 
  - First: `git remote -v`
  - Then: `git remote rm origin` (this removes the "origin" placeholder)
  - Then try again: `git remote -v`
  - Now you can add your own remote as suggested by github: `git remote add origin ...`
  - (we will clarify all these in more detail tomorrow where we focus on how to work with remote repositories and with other people)

- I get this error when trying to push the repository: 
  ```
  git@github.com: Permission denied (publickey).
  fatal: Could not read from remote repository.
  ```
  What is most likely wrong?
  - SSH access is probably not set up. See https://docs.github.com/en/free-pro-team@latest/github/using-git/which-remote-url-should-i-use#cloning-with-ssh-urls
  - The ssh key was not added via ssh-add. Adding the key solved the issue.

- While merging, **Git** can only handle *"obvious"* conflicts in individual lines, right? I guess if there is a function `func` in `master` that is used in branch `a` but altered in branch `b`, these three branches can be merged without conflict but it will cause erroneous behavior, won't it? Because the usage of `func` in branch `a` differs from its implementation in branch `b` (and hence in the merged `master` branch).
    - Correct. Git doesn't know wheter it's merging source code or song lyrics. Logical conflicts can be easily introduced into code without merge conflicts. If separate tasks involve common code, communication between developers is needed.


## Break until xx:15


## Inspecting history

https://coderefinery.github.io/git-intro/10-archaeology/

- is main the same branch as master? I´m not able to find master anymore... :(
  - yes somewhere we have renamed `master` to `main` with `git branch -M main`. We have done that because recenly GitHub started calling the default branch "main". This setting can be changed. It's also good to see that there is nothing really special about "master" or "main", they are just names and can be renamed.
    - thanks

- Where does `git log -S` look? Only in the commit Messages?
    - no, only in the code changes 
    - so this can be useful if you want to find out where/when something got added or removed and you don't see it from "normal" `git log` or `git log --oneline`
    - typical use case: "there used to be that variable X. when did I change that?"
        - thanks for this example **+1**

- He just mentioned that he was using Git bash, I'm using the command line in windows. Is there a benefit of using Git bash?
    - mostly depends on your preference I guess, but Gitbash is probably somewhat easier for Git and has unix commands

        - What is the benefit of unix commands?
          - When you have to work on a unix system for some reason (like web server administration, supercomputing etc), you will need the unix commands.
          - For a good introduction to unix shell commands and scripts, see this [Carpentry lesson](https://swcarpentry.github.io/shell-novice/)
          - working on the command line can feel a bit like traveling to the 70ies but after a while it may feel more efficient, especially when processing many files and chaining commands and scripting/automating them :+1:x2
              - I'd still always use some visual tool in addition, since `git graph` for example will become huge pretty large. Love VisualStudio code with a linux shell.
                - totally agree. I normally inspect the git history graphs directly on github/gitlab

- <span style="color:#aaaaaa"> This is just a fangirl comment: I use networkX in my work it's pretty cool ;)</span> 👍🏽
    - <span style="color:#aaaaaa"> What is networkX?</span>
    - <span style="color:#aaaaaa"> It's a library for working with graphs, the speaker is one of the developers. I was curious because the git example is with the networkX repo haha</span>

- note: `git checkout -b new_branch master` is just a shorthand to `git branch new_branch master` and `git checkout new_branch`. So nothing really new, but I believe we have not seen it before

- Can we use annotate and log even when branches have been merged?
    - yes, `git annotate` is extremely useful

- Just realized in breakout room that Grep isn't working well with Windows. Is this is universal problem with windows? What is the workaround? 
    - Do you also have a problem with **git grep**? Are you using the default Git Bash? (maybe a pager problem?)
        - Using the command line. Not sure what you mean by the above question around **git grep**, how do I check that? Also what is a  pager?
           - was the problem that `git grep` gave no output at all?
               - When I type that, I get "fatal: no pattern given"
                 - ah, but try `git grep somepattern` (where somepattern is the text you search for) 
                     - ```C:\Users\XXXX\recipe\recipe-branching\rvest>git grep 'No links matched that expression'
                        fatal: ambiguous argument 'links': unknown revision or path not in the working tree.
                        Use '--' to separate paths from revisions, like this:
                        'git <command> [<revision>...] -- [<file>...]'
                        ```
                          - try with double quotes? error looks like that git thinks "links" is a file.

                            ```R/session.R:      stop("No links matched that expression", call. = FALSE)```
                            - this looks good! this is not an error, this is the line we were looking for. so the problem was the single quotes?
                             - Ahh so does that mean that on the windows command line we must always use double quotes?
                                - this is new to me but we will adapt the material to not fall into this trap in future: https://github.com/coderefinery/git-intro/issues/275
                                  -Thanks!       
         
## Exercise until xx:55

- https://coderefinery.github.io/git-intro/10-archaeology/#exercise-basic-archaeology-commands
- optional exercise for those who finish the above: try the "git bisect" exercise right after the above
- With `git bisect`, what should we do if at a given commit we don't know if it is good or bad? Is there a way to tell git "I don't know, give me the next/previous commit" ?
  - It's kind of hard to find something if you don't know what you are lookign for. Guess you'll have to decide whether you want to find an earlier commit (mark as good) or after (mask as bad).
    - Yes, but this strategy chooses in which direction you go. Sometimes, a given commit doesn't compil for another reason, but the previous and next ones compile. It would be nice to be able to say "this commit is broken, give me a neighbor instead."
      - ah yes, see also below answer
  - in which situation don't we know? one situation I have been in is that the code does not even compile in a version and I cannot tell whether the bug existed there, in this case you can `git bisect skip` that version.
  - If you return 125, git will skip that commit. You can return that if for example the code does not build. (Didn't try it, but found as answer earlier)
  - Excellent, thanks! 
  - I found the issue by using git bisect manually, but it is tedious ... Then I tried the script provided, but I could not get it to work, git bisect complains that : "somehash was both good and bad" presumably because there is an issue with the exit code, when I run the python script it only prints an empty line ... Any ideas what I can try here ?
    - I just tried the example and it worked for me so I suspect that we have used it differently. I have saved the script as `test.py` and after defining the search endpoints, I ran: `git bisect run python test.py` and it located the bad commit. I suggest we look at it together via screenshare?


## Feedback

Please give us feedback for today: one thing that you enjoyed, one thing we should change/improve:

Good:
- It was nice that Matus showed how some of the command-line options (log, annotate) could also be seen on github
- I forgot to say yesterday, that showing some of the command history at the top of the terminal was very nice by Sabry
- Showing the clock with the break end-time on the shared screen in the break was a great idea, keep doing that!
- Nice demonstration of some very useful git tools.
- bisect is amazing. looking forward to try it
- I had done a workshop on Git and version control before, but this one has really helped me understand how powerful Git really is. Just need to figure out how to use it for my own work.
- exploring history
- IMHO you explained the whole branching/merging issue very nicely. I think I understood it now!

To improve:
- Just one note, the second instructor did not have the console history recorded in a doc so it was hard to follow sometime
    - Thank you for noticing this. We try to ensure that command history is available.
- I think it's a lot better to type-along than just watch :+1:x2
    - that of course must go a bit slower then but it saves the *"now for two minutes do what I have just shown"*
    - Thanks for the comment. We aim for group exercises and type-alongs and check and adjust our lesson timing to allow more those.
- I agree with the above, in general I prefer: group exercise > type-along > just watching.
- Same for me. I much prefer to type along, and then do the group exercises and discuss in the breakout room. I had some difficulties in the first part of today's lecture, since I had some issues with my files not showing up in the correct branches. As such, I had to delete my repo and restart, which caused me to lag behind and not follow the lecture properly.
  - we need a better starting point for day 2, I have created github issues for that  
- It's sad we can't really discuss advanced concept - totally understandable, since not everyone is at the same level. Maybe splitting into more/less advanced teams before the workshop starts would allow for that?
  - thanks for comment. indeed we would love to also give more advanced concepts but it is a difficult balance but maybe different room distribution could work. but we will over the next workshop days revisit some of the concepts and go more in-depth.

- ensure some time to discuss the interesting discussion questions on the webpage of the course programme :+1:. I'm wondering about many of them. e.g. "Discuss how Git handles conflicts compared to the Google Drive" 

- how can we report typos and/or other things related to the course material webpage.
    - thanks for asking! you can report typos and any problems as "issues" in the underlying github repositories. For git-intro it's here: https://github.com/coderefinery/git-intro
    - you can create an issue by clicking "Issues" next to "Code" at the top, and then "New Issue"
    - You can find the underlying github repos by clicking the "fork me on GitHub" banner in the top right corner of the lessons
        - did as a pull request in the end https://github.com/coderefinery/git-intro/pull/276

- (no feedback, but question regarding this morning and important for tomorrow i think): can you explain the most important differences between a public or private repository? Is it possible to have a public repository, but keep some working material still private for a collaborative working group? Thanks!
    - As long as you don't ever create repository in GitHub (or similar service) and don't `git push` everything is only your local computer.
    - If you want to collaborate via GitHub (or similar) you can choose whether you create a public or private repository for your collaboration. We have so far seen public ones. For private repositories you usually have to pay for (but not always).
    - Public repositories anyone can see and clone and fork to use as they want, restricted by the license defined in the repository. Repository owner controls who can push or merge to the repository.
    - Private repositories can't be seen or cloned or forked (or pushed) anyone but collaborators having the access.
    - You can set up your own local git repository (gitlab, gitea) for your working group.
    - It is possible to spilt your sources in two repositories, one of which is pushed to some private repo and the other one pushed to a public repo. Or you could push all repositories to a private service and set the public ones to be automatically mirrored to a public repo. Setting up the mirroring of a repository might depend on the collaboration service/platform or requires a little bit tweaking.


:::info
*Always ask questions at the very bottom of this document, right above this. Switch to view mode if you are only watching.*

*We are monitoring this hackMD, but we will reply every now and then so that you can focus on the speaker.*
:::
