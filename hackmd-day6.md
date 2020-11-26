---
permalink: /hackmd-day6/
---

# 2020 November CodeRefinery HackMD, day 6

## Links

- Course page: https://coderefinery.github.io/2020-11-17-online/
- Schedule: https://coderefinery.github.io/2020-11-17-online/#schedule

###### tags: `workshop`


## Icebreaker

Do you use continuous integration (or any form of automated testing) for your work? If so, to which degree?

- Jenkins, nightly and PR blocking
- Travis CI, nightly and PR blocking
- Travis and GitHub Actions, also GitLab CI, and some Appveyor (every push and merge request)
- GitLab CI
- GitLab CI
- GitLab
- Github Actions, Gitlab CI - but also used Jenkins and Travis; used for most of the tests automated and release builds (e.g. Docker and executables)
- None +8
- Jenkins
- Travis CI and GitHub actions (but I haven't implemented any of those myself except githooks)
- no idea what it is +2
- no but curious
- me neither


How is this online workshop format working for you? What are the differences against following our materials individually?

- The workshop forces me to consolidate time and concentrate, this would not be practically achievable just with the online materials because there are so many other obligations and distractions. +1 But it is great that the materials are available online because there is no time to digest much during the workshop, it is very densely packed with information and time flies (this is not a criticism! it's great to see so many things). So when we decide to take up some of the tools or try some of the new workflows we can go back and follow in more detail.  Truly amazing job, thank you all! +1+2+3
- Having expert helpers available online is also of great help during the exercises, because one can get stuck even with a lot of experience, when a tool or method is new
- Half day is great +8
    - allows to do other regular work stuff in the afternoon +1+1+1
    - allows to recapitulate course content that I could not digest in the morning +1
    - but I would welcome 30min more, and at least one 15min break + one 10min break daily
    - it would be really hard for some of us that are not located in European region to follow a full day class due to the time difference. +1
- I would have never done it by myself alone, just reading the material, mostly for time and concentration reasons +1
- I've enjoyed a lot. Like the format. For teaching duties I had to skip parts of the seminar but I can always go back to the materials and do the exercise on my own (did last night). The materials are good enought for one to catch up. Thanks for putting all together!
- I think you really got the point of distance learning, exploiting all the advantages +1

### Feedback / suggestions from yesterday


## Automated testing

- do we better include a test at the end of (within) a function/module that we are developing or right after using the function/module?
    - In projects I've been involved (general application development) the tests are written in their own file/module and in their own `<myproject>/src/tests` folder. 
    - My personal preference is to write tests close to the functions that are tested, then if I change the function, I don't have to go to another file. Also I often use tests as documentation. But the more standard way seems to be to collect tests into own folder.

- In a test-driven development, if the test goes first, isn't it a source for hard-coding? Namely when the person designs a function/code to pass a test but maybe the function itself will lose some generality.
    - good point! indeed in TDD the function is written to its specifications, specified in the test. but at least then the specifications are clearly documented. then later one may need to adapt these when generalizing. it's also always a tricky balance of not making things too general vs. making things reusable.

- Will you show us an example of non-trivial testing? Just as an example? I am not used to testing. Python is good 
    -  For less trivial tests we have a later episode: https://coderefinery.github.io/testing/test-design/ which also contains solutions. Unfortunately only in Python but we are working on R examples. Ideally we would like to have examples for a couple of languages. If you use testing in R or matlab or another language, you can help us with pull requests :-) :eyes:

- Just want to point out that the function to convert kelvin to celsius (in Concepts under defensive programming) is incorrect. It is supposed to be -273.15 and not plus. :)
    - looking ... ah yes :-) funny mistake. thanks! https://github.com/coderefinery/testing/issues/105 - beautiful demonstration that sometimes one can start from wrong specifications and arrive at wrong code with all tests happy.


### Exercise until XX:50

https://coderefinery.github.io/testing/pytest/#exercise-pytest

"Pre-commit hook" exercise is optional (otherwise it's left as "homework").

- I got stuck in point 7: Doesn´t recognice "." (for windows)" **'.' is not recognized as an internal or external command, operable program or batch file.**"
    - Were you on Anaconda prompt ? 
        - yes
        - It is already solved, thanks!
    - Can you please share how you fixed it
        - Just removing "./" 

- (...) now, in point 9, I committed it without problem but it should crash... I committed it in GitBash because I dont know how to commit in Anaconda. I could commit it but now pre-commit.bat doesn't run, which is what is spected

- Is 'pre-commit' a hard-coded file name in order to work as a git hook?
   - yes. the file name associates the contained script with one of a set of predefined hook names
   - you can have a look in `.git/hooks` and there are samples for other files with well defined names that relate to certain events and then you can script what should happen at these events.

- Can hooks be made part of the shared repo, or are they always local?
   - from git version 2.9 you can configure the path to the hooks. This allows them to be shared across a team of developers.
   - alternatively you could use fx. github actions

- Is there any test function for perl?
    - One example I found : https://perldoc.perl.org/Test

- in the pre-commit exercise, after testing and committing the correct file, I end up with a `__pycache__/` folder. What is it?
   - this is generated by Python and a good way out would be to add `__pycache__/` to `.gitignore` to make sure this is ignored by Git.

- FYI, the pre-commit test works on Windows+git bash
   - oh! nice!


### Break until xx:08

After break we will do this next exercise:

### Exercise until xx:40

https://coderefinery.github.io/testing/gh-actions/#exercise-a-full-cycle-collaborative-workflow

Note that the repository that we create should be **public**.



## Modular code development

Starting questions:

1. What does “modular code development” mean for you?

    - Develop code in 'batches', that can be tested independently, and also fixed independently.
    - Splitting problems into smaller parts that are "attacked" separately.
    - Having an abstraction of your system, knowing what your data looks like and then creating modules to process and display such data for several stakeholders
    - Break code into self-contained components as much as possible, develop and test individually, make parts re-usable in various combinations (not necessarily foreseen in advance)
    - Don't know what it means.+1

2. What best practices can you recommend to arrive at well structured, modular code in your favourite programming language?

    - Try to sketch or explain the structure within the documentation so that others know / understand the modules and how they connect to each other
    - Use pure functions +1
    - Know your system/program/information/project. Apply architecture patterns and software patterns and organize your data model.
    - ...
    - Design the structure to functionally independent components, use object-oriented programming as much as possible 
    - Think about input and output for each function (if the function takes too many inputs and the output is unclear that might be a hint that it's not modular enough...)
    - Start by designing the API. Ensure that the API is reusable/abstract, meaning that it (the functionality it encapsulates) can be used for general cases. Make your actual use case a particular one that can be addressed with the functionality accessible from the API.
    - Discuss with others!

3. What do you know now about programming that you wish somebody told you earlier?

    - There is never enough documentation!
        - In my opinion there is, sometimes, e.g. when it is incorrect, outdated, or too verbose/distractive of the main point. Good code/naming also can substitute (some sort of) comments. Also a good desing can save documentation. The point is that yes, documentation is essential, but there are cases when it is better to not to document (as those stated above) and concentrate on a good coding style/structure.
    - Strong typing helps a lot for debugging
    - Testing and documentation!
    - That it's more fun to programme together with other!
    - I now know how bad of a programmer I am, someone should've told me that long ago!  
    - It's not I wasn't told, it's that I didn't take the time to internalize good habits
    - Follow Unix Philosophy : one tool does one thing well. Avoid too many optional features
    - Thinking about data structures is necessary for a clean code architecture and also for performance
    - It's something collaborative! To work together with others improves your code a lot
    - Properly choosing names of variables, functions, classes, etc. is even more important than the documentation. It some cases, it can even substitute for it (e.g. when you "don't have time to create documentation/comment code"). It is crucial for others to understand what you are doing (e.g. finding bugs).
    - It is not because it is newer that it is better
    - It is not because it is old that it is bad ;-)

- For which type of data do you NOT recommend to use pandas? 
    - multi-dimensional data?
        - Agree. For this there is the excellent Xarray package.
    - gridded data

- How to enable the always visible command history at the top part of the instructor's terminal?
    - The instructor is using the fish shell and oh-my-fish extensions: https://github.com/oh-my-fish/oh-my-fish (i think)

- what does the `f` in front of the string do?
    - string formatting it was introduced in Python 3 in order to format strings
    - it allows you to embed the result of expressions in slots
    - [f-strings](https://realpython.com/python-f-strings/). Very handy stuff in Python.

- If you write your own custom fuctions, which you import into the main algorithm to run, how would you write tests for that? For example, I may make changes to a custom module and commit it, but I can't check it worked until I run it from the main code. Or should you write a test which can be run without any input data so it can be run on its own?
   - Clarrificaiton- Which file do you test in?  
   - You can write the test in the same module where you have the actual function, or in a separate test file which imports the module. When you run pytest it will find all functions that start with `test_` (usually for functions) or `Test` (usually for classes) and run them


- In the for loop "for num_measurements", would it be good practice to take that list out? So set the list of number of measurements you want at the to and then run that list? 
   - I was thinking more of pure code. I usually set my lists at the top and then iterate through a preset list. I'm just wondering if that would be poor practice?
 
   - yes this literal inclusion is very impractical for longer lists. Declaring it in a parental scope is good practice
      - I wasn't sure because the example of setting individual variables at the top was considered bad practice, but lists are ok?
         - bad practice is with regard to breaking references upon moving your function. If you create a parent scope to include both (fx. with a class) it is a nice example of pure, modular code
            - interesting ok. I was putting a series of individual variables at the top of my code, or make it easier to change for scientific testing- so I knew that those three variables were the ones I wanted to play around with. If they are in the functions, I would have to scroll around my script to find the things I wanted to vary. So I'm just figuring out if I am approaching it incorrectly.
              - it might be more pure to limit variables to the scope they are used in. Thus you will move them together with your functions. But if you declared a class with property fields (tweakable variables) and methods (the functions) you could do both. With the added benefit of having portable code 
                  - Thank you, I'll look into that!


### Break until XX:20
  
### Suggestions for making the code more modular
  
- write a loop over [25, 100, 500] for the plotting
- define a function 
- read it as an argument from command line
- The labels must be inside de loop. Otherwise, the labels are written only in the first plot.
- add error handling in its own function
- To grab the data, you can just use pd.read_csv with an object containing the URL. That way, it always grabs the 'latest' version. For example: `url = 'yourlink.csv'`, and then do `pd.read_csv(url, header=0)`. `header=0` keeps header names. And then you can even add stuff like `parse_dates=['date']`, if you're working with dates. It keeps the date format.
    - yeah, that's very cool!
    - as long as the file is not too big to download every time...
        - of course.
- create a class to allow your variables / property fields to be on top 
- Stupid question: How do you open .py in shell?
    - Probably call `python yourscript.py`. Not sure though.
    - if you mean "open in an editor", you need to use something like nano, emacs, vim (`vim myScript.py`) to open inside the terminal. But you can also use a graphical editor 
        - :+1:
- You should also put your loop inside a function (`main` for instance), and call ths function with ``if __name__ == '__main__': main()`` , otherwise you can't really reuse your python script as a module.
   - thanks for the suggestion!
- When would you suggest to move all those functions into a class? +1
    - that's a matter of taste! some people try to avoid classes and only write functions and package them in modules. Others might write a class from the start
- What to do when the functions are complicated and difficult to test (even on dummy data) ?
    - try to break up the functions into smaller parts! not always possible, but a good first approach. Then you can write integration tests which test larger parts of the code
- if we don't write the if name == __main__ line, then will main run automatically when imported?
   - yes, this is a "trick" in python to toggle whether something should be run when imported or when run as the script directly.
- how to verify if the input file exist?
    - in python you can use `os.path.exists(somepath)`
- You should assert that the list is not [] to avoid ZeroDivisionError
   - indeed, good idea. one can also check that input values have the right type with type annotations and mypy
- Don't we need to import test_compute_statistics from the statistics.py as well?
    - no, because test_compute_statistics is not used in example.py. It's in statistics.py because that's where compute_statistics() is defined
- What are good ways to pass many arguments to a function (e. g. 20) ? With a dict?



## Workshop Feedback

positives:
 - A lot of useful information. I had no idea of how extensive version control/collaboration tools are.
 - I really liked the automated testing exercises, both were very foolproof and complete.
 - The coordinated team work
 - Excellent demo of modular code refactoring (incl. the use of git inbetween). Very nice to follow despite the speed, because the example code was very simple yet not a silly toy code, but instead a simple case of realistic data analysis: this (kind of) code should be used much more in education ✌🏽

improvable:
 - publish a list of changes to the lessons so previous participants might consider to rejoin
 - I feel we did not make use of the breakout rooms well, was mostly just silence with the helper being heard typing. Since we're such small groups anyway, I'd love to have more discussions, even about "what's your project, so which solution might be best for you?". Else it feels very disconnected, since you're completely quiet for 3h.


## Twitter
 - https://twitter.com/famfigueiredo

