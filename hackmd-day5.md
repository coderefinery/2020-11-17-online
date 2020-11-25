---
permalink: /hackmd-day5/
---

# 2020 November CodeRefinery HackMD, day 5

## Links

- Course page: https://coderefinery.github.io/2020-11-17-online/
- Schedule: https://coderefinery.github.io/2020-11-17-online/#schedule

###### tags: `workshop`


## Icebreaker

Are you using Jupyter notebooks? (please vote y for yes and n for no)

- yyyyyyyyyyyyyyyy
- nnnnnnnnnnnnnnnnnnnnnnnnnnn


Are you using `nbdime` to diff and merge notebooks?

- y
- nnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnn


Are you using https://mybinder.org/?

- yyy
- nnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnn


Are you using R Markdown and/or R Studio?

- yyyyyyyyyyyyyyyy
- nnnnnnnnnnnnnnnnnnnnnnnn


## Feedback/suggestions from yesterday


## Jupyter and Jupyter Lab

- Which are the restrictions from puslishers in putting the results of our published research on a jupyter notebook and then on github?
    - I think it should be encouraged by publishers not restricted. Please share if you have experience +1
    - Different publishers might have different policies, but I think anyone is free to reproduce results in a paper, which means you are free to reproduce your own results. With reproduce I mean recreating them from the scripts/workflow in the jupyter notebook. If you just include the images/other results from the paper, then it should be fine as long as you give references.

- what is the difference between jupyter lab and jupyter notebook?
    - JupyterLab is a newer interface to Jupyter notebooks, which looks more like an IDE (integrated development environment)
    - jupyterlab is more customisable and modular and is generally recommended nowadays

- I am very very used to using the jupyter notebook, do I really HAVE to switch to lab?
    - No
    - just to avoid misunderstanding, JupyterLab is a tool for editing Jupyter notebooks, but the interface is different than the old jupyter-notebook interface

- Is there a way of mixing different programming languages in the same notebook?
    - Yes, see [answer below](#multiple-languages-notebook).

### Excercise, until XX:40

https://coderefinery.github.io/jupyter/03-basic-workflow/#exercisedemonstration-calculating-pi-using-monte-carlo-methods


Goals:
- create this notebook
- run all cells from top to bottom
- optional: try later modifying some cells and running them not in the right order

*(Notes continuing)*

- For me it doesn't make a difference whether I use `%matplotlib inline` or omit it, the result is the same anyhow. Is it supposed to be like that? :P 
  - this at least used to be necessary in the past. I am unsure whether it is maybe not necessary anymore.

- Can you add citations (like with a LaTex-formatation and bib) in a notebook? 
  - LaTeX yes but about bibtex: I don't know the answer. Somebody else knows?

- What happens when several people tries to open the same notebook? 
  - in this case we all modify our own copy. later when wrapping up the session I will mention tools that allow to work in the same notebook at the same time and save changes.

- How do you import a function from another notebook?
    - to answer my own question, this here worked nicely https://stackoverflow.com/questions/62689173/importing-function-from-existing-jupyter-notebook-to-a-new-notebook

- In the notebook I saw "shut down" option. When is it useful? 
    - It will shut down all "kernels" (e.g Python) and then the notbook webserver. When you start the notbook you start a webservice, i.e. an entry point that you can point your browser. When you shutdown this webserver will be shutdown and the port used relised.

<a name="multiple-languages-notebook"></a>
- Can one mix several languages (e.g. Python and Fortran) in the same notebook?
    - yes, there are "magic commands" that allow you to create a code cell in a specific language, e.g. write in first line of a cell `%%R` for R or `%%bash` for bash. One can install extensions for other languages, even compiled languages
    - and create own extensions/magic commands, see here for C++ example: https://coderefinery.github.io/jupyter/05-examples/#defining-your-own-custom-magic-command

- Did we already say how to share this (I mean the notebook) and I missed it, or is that coming up?
    - it's coming. will be discussed here: https://github.com/coderefinery/jupyter/issues/83

- Perhaps we should elaborate launching a new notebook instructions
  - we should add some screenshots: https://github.com/coderefinery/jupyter/issues/83

- I am not able to launch jupyter-lab from GitBash but when using Anaconda Prompt it works. How could I launch it from GitBash?
   - I think the problem is that perhaps the whole Anacoda installation is not visible from Git Bash. You can either adapt paths according to https://coderefinery.github.io/installation/troubleshooting/. But I would probably launch it from Anaconda Prompt and then you can also use the terminal that comes with JupyterLab.

- Which tool does Radovan use in the terminal to get proposal of commands (like auto-fill)? Looks decent!
    - `fish` is a linux shell with this tab completion https://fishshell.com/
    - `ctrl-r` will loop over previously used commands

- How can we reload this notebook later? through the shell I suppose, as a parameter to jupyter-lab ?
    - Give the name (full path if it is located somewhere else) of the notebook as argument
    - e.g. jupyter-lab  test.ipynb
    - Better way I guess is (the way I like) is
        - jupyter-notebook --notebook-dir DIR-WITH-NOTEBOOKS
        - Then select the notebook to load 

- nbdime seems to be already installed for me (Windows). Maybe it was part of Anaconda?
  - probably yes. it's great that it's already available

- will it install everything again or only the new things not present in the system? 
  - a bit unsure what is meant by "it"
  - `pip install -r requirements.txt` will only install whatever new packages are needed

- is there any logfile in the system for all the errors shown on the screen?
    - you mean the errors that you see in the terminal where jupyter-lab server is running? I don't think there's a logfile

- are there any security issues related to all these extensions 
  - I am not aware of incidents but I recommend to install extensions that are official and used by many

- What is the tool to time the breaks? It is really nice! 
  - it seems it's vclock.com

- When you open jupyter from the anaconda promt it gets stacked. If want to use the terminal again,you have to open a new one? [+1]
    - you could also launch jupyter from the Anaconda Navigator, so your promt stays clear (I cannot test if this is the case for jupyter lab, can someone confirm?)
        - Seems to shut down properly if you close all the Jupyter browser windows before doing ctrl-c. Using the launcher works, but it is harder to find the correct working directory as the change directory tool in Jupyter isn't very good (can't go up from the directory where Jupyter was opened!).

- How do you open the ndime sidebar on jupyter?   The pip install reported nbdime is already avaialable and I restarted jupyter-lab but I don't see the git icon
    - you might need to run `nbdime extensions --enable`, see https://nbdime.readthedocs.io/en/latest/extensions.html

- Can I add a new notebook to the gitrepo from the binder server? 
  - same/identical question answered further down



### Break until xx:07

After the break: https://coderefinery.github.io/jupyter/06-sharing/



### Exercise until xx:30


- room 13: I got an error from *Binder*: 

	```
        Waiting for build to start...
        Failed to connect to event stream
	```

   - sometimes it can get stuck, in this case close the tab and revisit the link via the Binder badge

- room xx: we would have needed a few more min



- How well does jupyter work with the Matlab kernel, any experiences? And how would the sharing work, if at all (since Matlab requires you to have a license and so on)
    - haven't tried it myself, just read a blog post explaining it and it seems to work fine. You can share the notebook on github but others might find it difficult to reproduce if they don't have a matlab license
  - as to the sharing via Binder: this really works well for open-source dependencies and can be a bit of a problem



- comment: the exercise time in the Overview here is wrong https://coderefinery.github.io/jupyter/06-sharing/, says 0 min but it's 20 below
    - thanks, so it seems. fixed.
    - yes sorry :-) I changed the exercises but forgot to adapt the timings

- Can I add a new file to the gitrepo from the binder server? 
  - you can add new files but once the Binder times out, all changes will be lost. so if you want to save changes, you need to do that via git/github and reopen a new binder.

- I get an error message: `Could not resolve ref for gh:XXXXXX/jupyter-exercise/HEAD. Double check your URL. GitHub recently changed default branches from "master" to "main".`
  - Update: changed from private repo to public - works now:)
    - good point, I forgot to say that for Binder the repo needs to be public 

- any insights on benefits and disadvantages on "JupyterLab supports sharing and collaborative editing of notebooks via Google Drive" compared to using binder
  - binder is non-profit/open and if you place the notebook on Zenodo, you can be reasonably sure that this will work in 5 years. we don't know whether the big companies change their services/terms in future.

- I understand that I have to add the matplotlib in the requirements. But how can I know it is really version 3.1.0? For simple stuff like this, wouldn't matplotlib be enough? I expect other versions working too. 
  - it would still work now but if you don't put a version, it might stop working in future once matplotlib changes. once you share a notebook for publication, it can be good to "freeze" the version. see also reproducibility lesson. Either `pip freeze` or you can `print(matplotlib.__version__)` in your notebook to find out which version you are using right now.
  - an example of this problem is here:  https://coderefinery.github.io/jupyter/06-sharing/#optional-exercise-what-happens-without-requirementstxt this notebook actually does not work anymore without some extra work because the authors did not record dependencies in `requirements.txt`






## Documentation

https://coderefinery.github.io/documentation/

### Excercise until XX:03

https://coderefinery.github.io/documentation/04-sphinx/#exercise-1-generate-the-basic-documentation-template

You can continue to Ex. 2 if you have time

- Questions about exercise 1 (part 2): got the error:

    ```
    Exception occurred:
          File "C:\Anaconda3\lib\shutil.py", line 104, in copyfile
            raise SameFileError("{!r} and {!r} are the same file".format(src, dst))
    ```

    - This was solved by deleting the _build folder and rerunning sphinx.


### Break until XX:13


- There was a question about organising big documentation into folders. It's a good option indeed, example is here: https://docs.galaxyproject.org/en/master/ | https://github.com/galaxyproject/galaxy/tree/dev/doc/source 


### Excercise until XX:32

https://coderefinery.github.io/documentation/05-rtd/#exercise-deploy-sphinx-documentation-to-read-the-docs

- room xx: ok. could use a bit more time though

- ReadTheDocs seems stuck on "Your documentation is building" for several minutes now
    - OK it worked eventually, I can see the docs now. But it really took a long time.

- It's also stuck on building for me, plus the "Error: Duplicated build" +1
  - Same here.
  - Seems to work now on 4th try...
  - Try pushing a new commit to the repo, and see if the docs build automatically (i.e. don't push any "build" buttons)

- When the build is done I get this error message: 

    ```
		SORRY                              
            **This page does**
             **not exist yet**    
    ```

    - is the page still not building? Sometimes it can take some time


### Break until XX:45

### Exercise

https://coderefinery.github.io/documentation/06-gh-pages/#exercise 

Until 12:00

#### Room status:
*CR editor's note: the room status preserved because it describes points to improve*

- room xx: Did not finish. Spent most time discussing/explaining confusion surrounding the connection between pages, sphinx, rst, html, ...
- room xx: We all get stuck on the first page after clicking "Choose a theme".  The exercise instructions don't work for any of us, we can get a project page via project settings on github but not from the linked pages.github
- room xx: OK, needed to clarify that repositories must be public
- room xx: did not manage, the undetailed instructions on https://pages.github.com/ were unsufficent. Took too long before I found the more detailed guide linked at the very bottom. It must've changed since last workshop? Then it wasn't so difficult.

*(Notes continuing)*

- How can I sign up for this event: https://nordic-rse.org/events/2020-online-get-together/? 
    - Thank you for pointing out, you can join from https://indico.neic.no/event/146/ "registration" at the second bottom. It seems the registration link disappeared for some reason.

- My github pages website doesn't update when I commit a change to the code or change theme.

- Our research group at Linkoping University is looking for a person that can arrange a workshop/lectur about code testing(unittest etc). If anyone want to please write.

- when writing a large documentation, are we supposed to leave all the rst files for the different subsections, or can we divide into subdirectories according to their hierarchy? Right now it seems to me that the hierarchy is only explicit in the index.rst file. Can we have rst files containing intermediate hierarchies (e.g. one rst file per "chapter", but each of them in turn links to different rst files for each section of the chapter). Or is the index.rst file the only place to specify how our documentation is organized?
    - The rst files can be distributed across several folders and subfolders. There is only one `index.rst` but it you can have table of contents also in other rst files and thus you can nest table of contents. In other words the entire table of contents does not have to be defined in `index.rst`.


## Feedback

*CR editor's note: Feedback was restructured little to facilitate its further use.*

One thing you liked:

- Interesting nbdime and binder
- Thanks <Documentation lesson instructor> for sharing a vertical screen! And thanks for the breaks and managing to go through the whole material with all exercises despite of limited time and without rushing, respect!
- Very good session; pacing and clarity was generally on point. Good summary by <Jupyter lesson instructor> before/after the lecture.
- Great quick-intro to Jupyter (Lab)! Worked fine all the way from using Jupyter the first time to launching it on MyBinder. And very nice with the need to use git in the middle.
- Very useful material, both jupyter and readthedocs
- It is amazing how much useful information there is in the coderefinery sites for these workshops/lessons. We can always go back and check out tools we did not have time to cover during the workshop, redo exercises, re-read explanations, follow links etc.  Very grateful for all this!


One thing to improve:

- A bit rushed and not enough time in breakout room to discuss (if there is no time to interact, it seems to me that there isn't too much point in having breakout rooms!)

- There was a bit of confusion on the [last exercise](https://coderefinery.github.io/documentation/06-gh-pages/#exercise): 
    - the exercise doesn't really explain what the starting point is, and
    - only instructs to "make changes to the repo". Learners who started from a blank repo (as opposed to the documentation built in the [previous exercise](https://coderefinery.github.io/documentation/05-rtd/#exercise-deploy-sphinx-documentation-to-read-the-docs)) did not understand why nothing appeared on pages or how to make the changes visible. 
    - Most of the breakout-room time went into explaining what was supposed to be done, and the purpose of/relation between pages, readthedocs, sphinx, rst, html. 
    - A suggestion would be to perhaps specify the starting point of the exercise, and also to change "Make a change to the repository after the webpage has been deployed for the first time" to something more specific (e.g. change the `.rst`-files and build the documentation).

- A pity that the ReadTheDocs build didn't work smoothly. In my case there were errors, which ReadTheDocs showed only long time after launching the build, so impossible to fix before the workshop day was over. But worked in the end! (this might not be so actionable feedback, other than maybe adding a warning about double-checking the ReadTheDocs parameters and immediately redoing (Admin tab?) if not showing valid build output)


- One thing that did not work so well for me and my group today was the jupyter part.  The presentation went a bit too fast in the sense that the presenter was not aware of the point of view of someone who has not used a particular interface before. There are a few compounding problems here in my opinion: 
    - First, not explaining exactly what is supposed to happen at each step. Running a shell command with --no-browser makes things complicated and leaves us wondering how to get to the right place (in my opinion this was probably unnecessary at this stage). 
    - Second, not waiting for the audience to "digest" each step. If someone is even slightly uncertain and may be looking around for stuff, it is very easy to get lost, and if the presenter is two steps ahead then the flow is broken and *everything* is missed until a correction can be made. 
    - Third, the most trivial things can benefit from being explicit. If it is one's first time on an interface, we don't know where the terminal is, or where anything else is. There are top menus, sidebars, notebook-specific menus, options all over the place.  It is useful to say exactly what you are clicking, take a breath, then click on the right option while again saying what you are clicking on. 
    - As a more general comment that applies to some extent to other modules, it seems to me that sometimes we get into a "how-to" mode that focuses on sequences of actions (commands/clicks) where it is easy to get lost with respect to the conceptual operations (what we are trying to achieve and how each step moves us toward that objective). 
        - The git introduction is where this did *not* happen: very nice diagrams explaining the point of the whole setup, and frequent reminders of how the operations were serving that overarching purpose. 
        - As rather poorer examples, yesterday's use of binder got me completely lost because I had no idea what we were doing and why. I think now that the point was to be able to see snakemake and instead of running it locally we took to binder due to some people having installation problems (is that right?). I personally did not have problems with snakemake (following the fine instructions to install minimal on windows) so it took a while to dawn on me. So then instead of trying to focus on what snakemake is for (note: I am not a newbie, I used to work with Make a lot a couple of decades ago) we are wrestling with binder and conda; it must have been a total blank for beginners. 
            - In general, there should be only ONE major conceptual objective at a time, and it should be clear to the participants all the time (after three commands it can be forgotten, it must be connected to the actions all the time). 
            - Okay, I am saying a lot of "should", I would just like to clarify that this is just my impression and personal opinion, I am not lecturing anyone here, I am *very* grateful for this opportunity and I just hope the comments are helpful!  
    - So today's first part was for me also less well anchored to a conceptual foundation. I have no previous experience with jupyter (have been hearing about it for years but never tried) so it took me a while to realize that this is not a tool for collaboration (at least not directly). I imagined the notebook was some sort of online collaborative coding. Of course that is not the workshop's fault, it's mine, but it should have become clearer what we are trying to achieve at each step, and why. Maybe a diagram of the overall workflow at the beginning could have helped: here is a tool for coding on the cloud, here is how that connects with git, here is how people can work together -- and then each component becomes a lesson and goes along with the exercise. Almost all of this is already there, but it seems to me that the glue that holds it together is sometimes missing, and from the participant's perspective, trying to figure out and provide that glue online oneself while also trying to follow unfamiliar steps over unfamiliar environments/interfaces is sure to overwhelm someone who has no anchoring points. At least that's my opinion.

    - *CR editor's note: Thank you for taking time to write this feedback! I tried to structure it little to facilitate its use.*

 
- I think I see now what's wrong with the last exercise (how to make a web page, on https://coderefinery.github.io/documentation/06-gh-pages/). 
    - The first instruction reads "Follow https://pages.github.com/" and is the first item on an unnumbered list, but I think it should read "Follow the instructions on https://pages.github.com/" and be one level above the following list. 
    - Also, the first two following items ("Select “Project site”" and "Select “Choose a theme”") concern the pages.github.com whereas the remaining items (starting with "Click “Select theme”") concern the project settings, but there is no separator or other indicator to this distinction. 
    - This was confusing but one of us figured it out quickly -- the rest of us, including myself, were trying to blindly follow the instructions instead of reading the page. Not a bit deal, but easy to fix so that people won't stumble next time.

