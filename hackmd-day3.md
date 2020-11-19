---
permalink: /hackmd-day3/
---

# 2020 November CodeRefinery HackMD, day 3

## Links

- Course page: https://coderefinery.github.io/2020-11-17-online/
- Schedule: https://coderefinery.github.io/2020-11-17-online/#schedule

###### tags: `workshop`

## Icebreaker, Day 3

What operating system and what display setup do you have?


| OS       | Display setup  | +1  |
| -------- | -------------- | -- |
| Linux | 2 monitors + laptop screen | - |
| Linux | 4k TV    | - |
| Linux | laptop + 27" monitor (1440p) | +1 |
| Linux | 4K laptop | |
| Windows/MacOS | notebook screen | ? |
| Windows | laptop + extra screen | 6 |
| Windows | desktop(!) + 2 screens | 1 |
| Windows/ubuntu |laptop + extra screen  | 1 |
| MacOS | laptop + extra screen | 2 |
| MacOS | laptop + 2 extra screens | 1 |
| MacOS | laptop | 1 |
| Windows | laptop | - |


## Feedback/suggestions from yesterday

Few questions arrived after the workshop and we have (hopefully) answered all questions here: https://coderefinery.github.io/2020-11-17-online/hackmd-day2/

Any other questions that you would like to have clarified?

- when to open a repository as private and when as public? when you open as public, can part of the code that is being developed still be private to a group of collaborators? 
    - I assume this is related to when a repository is on a public website (e.g. gitlab, github etc.) Usually a private repository means the code is not made public, it contains some information that should not be shared "on the internet" or it is not yet ready to be open (e.g. work in progress). A repository can be made public once work is considered at at status where it can be made public. However be sure to clean the commits of any private information in the git history or be sure to keep that information separate if there is ever a plan to make the private repo public at some point.
    - I could think of another two reasons for private repos
        - For companies with commercial interest. e.g. there is a public version and a Googles version of Andriod
            - for this usually a companies have internal git repositories to keep them private
        - The License agreement is not ready yet 
        
    - Not sure there is such a functionality to make part of github or gitlab repository private
    - In Git either entire repo is public or entire repo is private. But what can be useful is to use two repos (one public, one private; we will today learn how) and put the unpublished stuff on the private repo, and share the master branch, which only contains published things, on the public repo, to give others the chance to base their work on the public version.
    - In companies (at least where I worked) we had two repositories: one public for public releases and one private for internal development. We populated the public from the private whenever we wanted and with only the features we wanted.
- 
---

## Git-bisect (10 minutes before we start with collaborative Git)

https://coderefinery.github.io/git-intro/10-archaeology/#exercise-git-bisect 

- As a Windows user, which tasks should one do in the Git bash vs Anaconda prompt, in general? I'm a little confused as to why he had to switch over to anconda prompt?
  - It is possible to set up your Git Bash to do everything in there but often, depending on installation, Git Bash cannot see the Python installation. If you use Python in your "daily work" and would like to get this configured, we can do that together. If you don't use Python, then what you can do is to have two terminals open (Anaconda Prompt and Git Bash) and do all the git stuff in the latter and run the very few commands which will require Python in the Anaconda one. This is how one can make Python visible in Git Bash: https://coderefinery.github.io/installation/troubleshooting/
  - there is also information here: https://docs.anaconda.com/anaconda/user-guide/faq/#installing-anaconda ("Should I add Anaconda to the Windows PATH?")
      - I do use Python in my "daily work", and just run scripts from Spyder. I currently use git from the command line. Is this something that I should configure differently then?
          - depending on what is your default "daily work" python (e.g. 2.7<-- obsolete - some systems still have that as default) and if you can change that to another python version (e.g. 3.8) without affecting your work, then the recommandation is to follow the links above.
          - we can also debug this later. also, Spyder has git integration so you may prefer to do Git directly from there. but if you like to work in the command line (I personally prefer that), then we can fix this together later.

- Git bisect clarification- you are running the code and checking manually at each step to see if it works the way you want? 
  - yes, but this can be scripted (we also provide an example). you can write a script (any language) which decides whether the code is working (by returning 0/non-0 return code) and then git bisect can also use that.

- If you have found the commit where something broke. How do you then repair that so that it ends up working again at the end in the master?
  - once we know the commit, and assuming the commit is not too huge, often just by looking at the commit we can see why something broke and it can help debugging. the recovery then could be either reverting that problematic commit, or apply a new change at the tip of the main/master branch, undoing the mistake. possibly using a "manual" commit.

- Did I miss something ? At the end of bisect, `git show` shows changes which seem to not cause any change of the actual value. It just adds and innocent comment.
  - which commit did you locate?
      - Commit 136 which just adds a comment at the end of t0. It resembles the output shown by Matus.
        - the bad commit is `git show 326f68a5585`, so the one right after. I gues maybe you stopped one step too early.
            - Ok, resolved. I understand. At the end of `git bisect` the bisect ends at the last good commit (i.e. 136) in order to check what went wrong... (This statement is wrong. Check comment below.) 
              - no it ends at the first bad commit. but just before arriving there, it shows "0 steps left" and I think it can trick the person/presenter to not do one more step. after seeing that we should have done a "git bisect good" and git bisect would have shown us the bad commit (sorry I wasn't following the video then so I am not 100% sure but I think this is what happened)
                  - I checked the work flow twice. Even after doing `git bisect good` after it shows "0 steps left", the commit is still at 136 and `git show` still shows changes with commit 135 and not 137 (which is the bad one). Can you please confirm this ? I actually discovered `git bisect` now and I think its very interesting. I just want to know exactly how to use it.
                    - checked (see below, I go until it shows me the bad one)
                        - That's correct. I was talking about `git show` at this point.
                          - Aha! I was assuming everybody does `git show 326f68a55` :-) Should we clarify the material for this? :+1:
                              - :-) Thanks for clarifying. I understand how `git bisect` works now !
                                - great! it's super valuable. not something we need every day but something I need 2x a year and then it saves me always a day or two of work.

                    - [name=staff] In my demo, the bisect stopped indeed at the first bad commit (137), but the HEAD was at the last good (136). So `git show` showed the last good commit (136).  
                       - ok, sorry, i will modify my answers above :-)
My output:  
```
~/tmp/git-bisect-exercise on dac3c42
$ git bisect good
Bisecting: 0 revisions left to test after this (roughly 0 steps)
[41af86cd42a966e4375b68bbad4af1384a0558cf] commit number 136

~/tmp/git-bisect-exercise on 41af86c
$ python get_pi.py
3.14

~/tmp/git-bisect-exercise on 41af86c
$ git bisect good
326f68a558501a6f44d7685c2c1795794bac09b5 is the first bad commit
commit 326f68a558501a6f44d7685c2c1795794bac09b5
Author: staff <staff@users.noreply.github.com>
Date:   Fri Mar 29 16:02:52 2019 +0100

    commit number 137

 get_pi.py | 8 ++++----
 1 file changed, 4 insertions(+), 4 deletions(-)
```
  
- Why do we not stop after the first git bisect good, I mean why check all the history?  
    - because we wanted to find the first commit which changed the behavior from "good" to "bad". if we had stopped at the first "good", we would have found a working version, but not the commit that broke it. knowing the commit that broke it is useful if 1) you already published the paper and want to know whether this was before or after the problem, and 2) **it can simplify debugging if you see the bad change, often it's just one line that changes the behavior**.
    - but in the example, it kept alternating, it seemed as if the issue happened multiple times in history then been reverted? Maybe I am missing something here.
        - we did not traverse the history "following the time arrow", we gave git bisect two endpoints, then we halved the history, then we halved it again, then again. so we were jumping around the problematic commit. this was to minimize the number of steps.
            - ah ok! Got it, thanks
                - A good way of getting to understand it better, is trying the exercise yourself. In every step, you'll see at which commit in history we are, as for this exercise, the commits are "named" including a sequencial number (1, 2, 3, ...)
                - indeed if we went one commit after another, we should have stopped at the first "good" (but then we would have used 136 or 364 steps (depending on which direction we'd go), whereas with _bisect_ we used only 9 steps of _checkout+test_ to find it)

---

## Collaborative distributed version control

https://coderefinery.github.io/git-collaborative/01-remotes/

- I am confused: isn't 'centralized' the opposite of 'distributed'? Git is distributed, but has a centralized approach? 
    - the distinction is that in a centralised model there is only one latest version of the git repo, whilst in a distributed model each node has a copy which might be or not the latest one that is recorded at a working/shared (central) repository (or git remote) location.
    - and here with "centralized" we meant that we all work in the same repo on GitHub/GitLab, only one remote, while using a version control system which could equally well deal with multiple remotes. Later this morning we will also work with multiple remotes.
    - Another way to put this would be, yes Git is a distributed system, at the same time it also allows to make one of the copies to act as a central point. This is normally the copy in the cloud. But it could also be on a local network or even a location on the same computer. A trick when working with a central point define is to *pull* (get what others have contributed) before you *push* (share your work)

- What about documentation and instructions? Will we look at  wiki-page or git docs? 
  - we will discuss code documentation next week (if I understood the question correctly)
  - I wanted to know about how to make a wiki page or Docs side with GitHub:) 
    - when you create a new repository, it is created with a new wiki (top of window then). however, [name=staff] recommend to not use wiki for code documentation, more about that next week. but the GitHub wiki can be useful for notes where you are not so much interested in being able to go back to a specific version of your code+documentation.
 - And the docs side provided/made possible with GitHub? Like this: https://docs.github.com/en/enterprise-server@2.22/github/setting-up-and-managing-organizations-and-teams/repository-permission-levels-for-an-organization
 
- In GitHub, there are also projects. How is that different from a repo?
    - each repo can have a project to organise work e.g. issues, Pull Request specific to a team's workflow. There are also organisation specific Projects that can organise work across multiple git repositories.
    - Projects provide more of an easier way to organise and streamline issue tracking.
    - more info at: https://docs.github.com/en/free-pro-team@latest/github/managing-your-work-on-github/about-project-boards
    - in short, it allows to arrange issues in a board according to columns and move them by mouse. this can be interesting for people who like agile development techniques and "kanban" boards.

- How do we get the SSH URL instead of the HTTP one?  I have set up my git/github for SSH and it won't push to HTTP (Authentication failed). Or is that not my problem? [name=learner]
    - you can click the green "Code" button on the GitHub repository and there select "SSH" 
    - After getting the URL as mentioned above, you need to remove the old URL and then add the new one
        - `git remote rm origin`
        - `git remote add origin <NEW URL>`
        - `git remote set-url origin <New URL>` can overwrite the existing origin url
        - always double check your remotes after the commands with `git remote -v`

- I have a problem with deleting local repositories. I always get a complaint about some file in the .git folder being write-protected. Do you know what to do?
  - on which operating system is this?
      - On Ubuntu via WSL (Windows)
  - might be that there is another software/application that has git repository open
      - Yes maybe. But I now tried to delete the repo by opening the folder in explorer (explorer.exe .) and that works.
        - interesting 
        - Does it only affect git? Maybe you have another tool always accessing the files (like OneDrive, dropbox etc)
            - Yes it is only something I have experience with git. I think it is a specific commit that gets write protected. The complaint refers to a hash inside the .git folder.
            - `rm: remove write-protected regular file 'git-test-1/.git/objects/bb/537272e146ca60fd72dfe0b87195d948fc696b'?`

- How do you "write protect" the main/master branch on GitHub?
    - go to the repository URL, click Settings -> Branches (menu on the left) -> add branch protection rule
    - more information at: https://docs.github.com/en/free-pro-team@latest/github/administering-a-repository/configuring-protected-branches


### Break: (until xx:25)


### Resuming at step 9: discuss and accept pull request

https://coderefinery.github.io/git-collaborative/02-centralized/#9-discuss-and-accept-pull-requests

- What happens in the local side, if a pull request is rejected? 
  - rejecting can mean not merging a pull request or closing a pull request. but in either way, nothing changes locally, closing the pull request/ merge request does not delete the source branch (the branch from which the pull request was sent from) and does not delete any commits.

- What happens when the merge to master happens in the local reppository, and then the developer pushes the changes to github, and then the pull-request is rejected? I imagine that the remote and local repositories will have a somehow inconsistent state, correct? What happens in the next `git fetch` or `git pull`?
  - for simplicity let's first assume the PR (pull request) was not rejected but is still open: if you merge locally and push the merge commit, also the pull request will change to "merged" and it will look like if we had merged it via web. I don't know what happens if the PR has been rejected and you push the merge anyway. Let me try this quick: This is how it looks: (link redacted) (although I closed/"rejected" it earlier, it looks like it has been merged)
  - if a PR is rejected and closed nothing will happen, if it is just rejected changes might be required, not sure changes can be pushed if a rejected is there or there os a block by github from merging it.
    - github does not block me from pushing the local merge, see discussion/example above
        - if not set, yes, that is why one needs to set protected branches so that you don't push rejected Pull requests :) 
        - also that example does not reject it, and maybe the terminology is important here but "reject" to me means changes were requested, "closed" means it is closed, changes can still be pushed to the branch associated to that Pull request, even if the branch is deleted then probably changes can still be pushed, although not ideal
        - see https://docs.github.com/en/free-pro-team@latest/github/collaborating-with-issues-and-pull-requests/reviewing-proposed-changes-in-a-pull-request vs https://docs.github.com/en/free-pro-team@latest/github/collaborating-with-issues-and-pull-requests/closing-a-pull-request 
  - probably an example will help to illustrate what you mean it is not 100% clear
    - but also I don't think the above situation happens often in practice. I would write-protect the master/main branch and then this situation "cannot" happen and all merges then have to go via pull requests.
 
- A comment: I think it would be useful to clarify that GitHub offers services on top of git E.g. the pull-request is not part of git, but of github
  - very good point. pull requests/ merge requests are built on top of git branching and merging. git itself "does not know" about pull requests or issues.
    - Neither about forks! :) They are simply clones stored in the "cloud"
      - indeed. forks are copies from one userspace/organization to another. under the hood, they are clones, not from cloud to computer but from cloud to cloud. 

- Does it exists an upper number (like max) for the storage space or number of repositories you can be a part of? 
  - there is an excellent answer on stackoverflow to this question: https://stackoverflow.com/questions/38768454/repository-size-limits-for-github-com#:~:text=Repositories%20have%20a%20hard%20size,also%20apply%20for%20large%20pushes.&text=Files%20can%20also%20be%20shared,such%20file%20is%202%20GB#answer-59479166
  - there are hard and soft limits. It is recommended to keep repositories small (1-5 GB). The push size limit is 2GB. Files are limited to 100MB in size.  
  - this is another good reason for code review: somebody else can check whether I am accidentally adding a 200 MB file to the history. technically we can remove commits from the history but organizationally this can be non-trivial.

- Does anyone know about the push/pull options for GIT with Jupyter Notebook/lab?
  - There is the nbstripout plugin which allows to remove the output of cells before you commit. It simplifies the workflow with Jupyter. You can `pip install nbstripout`, and in your `$HOME/.gitconfig` you can add:
    ```
    [filter "nbstripout"]
        clean = python3 -m nbstripout
        smudge = cat
    [diff "ipynb"]
        textconv = python3 -m nbstripout -t
    ```
  - See also https://pre-commit.com/ for a collection of many tools to quality control and validate commits. Many are useful to validate syntax, code style and prevent you from adding files or content that you shouldn't (e.g. a password).

- What is gitverse? is there any such thing as gitverse or related one? or universe ?
  - This word might be used to refer to the ecosystem of tools built around `git`. I wouldn't worry about these terms. 
  - where did this term show up?

- Can we close multiple issues with one PR. For example, "closes #N #M"?
  - "I did this and that, closes #1, closes #2, closes #13"  
  - or a multiline commit message and you can list all the closes line by line
  - note that if you forget to close issues in the commit, you can also close them in the pull request/ merge request

- How do I sync my fork with the central repo now?
    - we will demonstrate this: the short route is https://coderefinery.github.io/git-collaborative/03-distributed/#shorter-route, there is also a longer way, just above
    - important to realize that forks do not automatically update themselves, we update them via our local clones by pulling from one remote (central) and pushing to another remote (the fork)
    - also good to know that instead of using shortcuts like "origin" you can refer to the full URLs instead
    - Is it also possible to just keep my forked repo out-of-date in the long term, and instead only pull from the original repo? Or could that cause issues?
      - it is ok to keep it out of sync but I would update it before I start working on something new to make sure that the new feature branch is not based too far in the past and to avoid conflicts at the moment when I send the pull request few weeks later. I often don't even bother updating the main branch on fork since I don't work on it anyway.
          - Yes. I meant pulling master from the original repo, but pushing only my feature branch to the fork
            - Right. I think this is fine and this is how I often use it: you do the work locally anyway, and then the fork is only a "parking lot" for open pull requests.

- there were no option to create issues from forks "forked" by helper. However, a collaborator when used the main repo branch as a template and "generated" from the main repo, then issue could be created.
  - a fork will by default not carry own issues but you can enable issues on a fork (settings). but it is often less confusing to have all issues only in one place, in the central repository.
  - for the *generated* repo it worked because there the goal is different: this is often used to generate repositories where there is no aim at bringing changes back to the template and then it makes sense to track their own issues

- I created a new branch and wanted to upload that to my repo and then make a pull request, but the new branch does not appear while git in the shell says "Everything up to date" after a push. No the branch is missing.
  - check with `git status` or `git graph` whether the branch you want to push contains any new changes. But still the branch should show up on GitHub. It doesn't?
    - maybe we can look at it after via screenshare?
  - maybe `git push -u origin <name_of_branch>` 
     - it should still show up, also without `-u`
      - I tried the just now, it still does not show up.
      - before I tried 'git push origin -u branch_name'
          - let's look at it in a breakout room?
            - please let me know if this is still an issue
            - it kind of did something now, but I still don't understand.
            - I can explain here, perhaps that will be more clear.
              - OK, let's do that.
            - I managed to push the new branch and file to my repo. And then made a pull request, which was accepted. But once the PR was accepted, the file directly appeared in the upstream repo, my branch vanished. This is unexpected. Is this normal behaviour for github ?
              - the vanished branch is surprising. can you paste a link to the pull request? I will remove the link again before we publish these notes.
            - the link is: (link redacted)
              - the branch is still there, it stays on your fork until you delete the branch. the merged pull request neither removes the branch, nor does it actually modify your fork
                - my branch is still in my repo yes, but why does the pull request not conserve the branch in the upstream repo ?
                  - the branch was created in your fork, not in the upstream repo, so it never existed in the upstream repo (for full completeness this is not 100% correct but this is a technical detail of how github stores things but I think it is useful to imagine that the branch never existed there)
                    - does this mean that only the owner or a collaborator can create a branch in that repo ?
                      - right, this is correct. otherwise anybody could "vandalize" my own repos without asking me. 
                          - It would still be a pull request ...
                            - and this way I have the choice to accept what goes in 
                            - Yes but can a pull request create a branch ? That is my question.
                              - the PR does not create a branch, it originates from a branch and once merged, it creates a commit, but does not create a branch 
                                 - I see, is this mentioned in the tutorial ? I might have missed it, but if it is not there, it would be good to point this out, to avoid confusion.
                                   - thanks: https://github.com/coderefinery/git-collaborative/issues/162  
        - I have a related questions, the first issue was due to the fact that the git setup by default uses http login which never worked in the git bash, although sometimes it said "Everything up to date".
            - Is there a way tell git to setup every new repo to use ssh ?
              - I think it remembers the last choice and will default to that


## Feedback for day 3

Please write down one thing you liked and one thing we should improve.


### Good:
 - Having multiple upstreams around form the start is nice! Thanks for teaching GitHub workflow
 - The pictures describing what happens locally/remote, makes it easier to understand!
 - It was very helpful to first learn how things work conceptually, then connect it to code, and then practice with the code (and concepts!) on our own. This order is important because it helps to actually understand what you are doing while coding (in contrast to coding as fast as possible to keep up and then not really knowing what you actually did...).
 - Great exercises on collaborative workflow. They really get discussions going, and learners learn a lot from each other.

### To improve:

 - It might be nice to directly see what we are supposed to do from the tasks: like some tag for `helper`, `type-along`, `do-yourself` etc. Was always a bit confusing with "helper does A-C, you do D-E, F and G will be done in zoom"
   - good point, we need to make this clearer
- Very simple code that is expected to be known, might not be known to everyone. So things like 'step out of your directory' are total gibberish to people who don't know git bash. It would be very helpful if such simple commands (cd ..) are included in the mark down after such statements (between parentheses or something), to help out the people that have no clue. This also helps people not to get lost, get behind, or feel like total noobs. 
  - thanks! good suggestion. one slight complication is that some of these "simple" commands are sometimes different on different shells (which can increase confusion) but still we should make this clearer, perhaps offering different tabs. but it is super important that we avoid giving learners the feeling that they are "noobs" so we need to do something about this.
        - Thanks!





:::danger
If you're not editing this hackmd document, please go to view mode by clicking the eye button :eye: - you can then go back to edit mode when you want to edit.
:::

:::info
*Always ask questions at the very bottom of this document, right above this. Switch to view mode if you are only watching.*

*We are monitoring this hackMD, but we will reply every now and then so that you can focus on the speaker.*
:::