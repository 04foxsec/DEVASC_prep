# Software Development and Design

Programin is much more than just creating an some code and run it. Each and every software even the smallest one has some of the following steps while created.

1. Planning (requirement analysis): Identifying the use case that the software suposed to solve. 
2. Defining: analysing functional specification and defining what the software should do.
3. Desiging: turn the software specifications into a design specification.
4. Building: Vreating the software based on the specification. (If the previous stages are completed successfully, this stage is often considered the easy part.)
5. Testing: Testing application behaviour. Bug and defect search. Application works as expected?
6. Deployment: Software is put into production. After final acceptance this stage becomes the maintanance.

ISO/IEC 12207 is the international standard for software lifecycle processes, and there are numerous organizations around the globe that use it for certification of their software development efforts.

Most popular SDLC models:

- **Waterfall**
- **Lean**
- **Agile**
- Iterative model
- Spiral model
- V model
- Big Bang model
- Prototyping models

---
## Waterfall
Started back in the '50 when IT and softwares just started to kick in and a few people knew how to program. The constructing business process (in which every step along the way was dependent on the completion of the previous step in the process.) gave the idea to the Waterfall model and became the most populat SDLC approach.

**Waterfall is a serial** approach to software development that is divided into phases:

- Requirements/analysis: Software features and functionality needs are cataloged and assessed to determine the necessary capabilities of the software.
- Design: Software architecture is defined
- Coding: Coding the software based on the design
- Testing: The completed code is tested for quality and customer acceptance
- Maintenance: Bug fixes and patches are applied.

Pro: 
- Easy to understand
- Step-by-approach

Contra:
- Serial nature of the model
- Does not handle change very well
- No achievement(working code) till the end of the process
- Quality (because of the limited time for a development cycle usually the testing is the one that suffers)

## Lean
Toyota production system aka TPS

- **Elimination of waste:** If something doesn't add value to the final product, get rid of it. There is no room for wasted work.
- **Just-in-time:** Don't build something until the customer is ready to buy it. Excess inventory wastes resources.
- **Continuous improvement (Kizan):** Always improve your processes with lessons learned and communication.

Lean led to Agile software development

## Agile
Agile is an application of Lean principles to software development.

The following 12 principles are the core of the Agile Manifesto:

- Customer satisfaction is provided through early and continuous delivery of valuable software.
- Changing requirements, even in late development, are welcome.
- Working software is delivered frequently (in weeks rather than months).
- The process depends on close, daily cooperation between business stakeholders and developers.
- Projects are built around motivated individuals, who should be trusted.
- Face-to-face conversation is the best form of communication (co-location).
- Working software is the principal measure of progress.
- Sustainable development requires being able to maintain a constant pace.
- Continuous attention is paid to technical excellence and good design.
- Simplicity is the art of maximizing the amount of work not done is essential.
- The best architectures, requirements, and designs emerge from self-organizing teams.
- A team regularly reflects on how to become more effective and adjusts accordingly.

With Agile the timeframes are smaller (can be 2 weeks)(sprints) and encompasses all the elements of the process. The aim is to ship a feature or capability  within 2 weeks. So with Agile when you are half way through the project you have workin code (with less functionality, but working)

## Common desing patterns
You don't want to reinvent the wheel each time you need a rolling thing to make something move. In software engineering, many common design paradigms have already been created, and you can reuse them in your software project. These design patterns make you faster and provide tried-and-true solutions that have been tested and refined. 
- Model-View-Controller (MVC) 
- Observer patterns

### Model-View-Controller (MVC) Pattern

Separation of concern (SoC) is decoupling and application's interdependencies and functions from its other parts. Leyered model (data access, business logic, and presentation)
- flexibility
- easier coding and maitanance
- give structure to the application

- Model: (db) The model is responsible for retrieving and manipulating data. It is often tied to some type of database but could be data from a simple file. It conducts all data operations, such as select, insert, update, and delete operations. The model receives instructions from the controller.
- View: (web) The view is what the end users see on the devices they are using to interact with the program. It could be a web page or text from the command line. The power of the view is that it can be tailored to any device and any representation without changing any of the business logic of the model. The view communicates with the controller by sending data or receiving output from the model through the controller. The view's primary function is to render data.
- Controller: (app) The controller is the intermediary between what the user sees and the backend logic that manipulates the data. The role of the controller is to receive requests from the user via the view and pass those requests on to the model and its underlying data store.

### Observer Pattern

The Observer pattern was created to address the problem of sharing information between one object to many other objects. This type of pattern describes a very useful behavior for distributed systems that need to share configuration information or details on changes as they happen. The Observer pattern is actually very simple and consists of only two logical components

- Subject: The subject refers to the object state being observed in other words, the data that is to be synchronized. The subject has a registration process that allows other components of an application or even remote systems to subscribe to the process. Once registered, a subscriber is sent an update notification whenever there is a change in the subject's data so that the remote systems can synchronize.
- Observer: The observer is the component that registers with the subject to allow the subject to be aware of the observer and how to communicate to it. The only function of the observer is to synchronize its data with the subject when called. The key thing to understand about the observer is that it does not use a polling process, which can be very inefficient with a larger number of observers registered to a subject. Updates are push only.


## Linux Bash

BASH (Bourne again shell)is a shell, and a shell is simply a layer between a user and the internal workings of an operating system. compatible with other shells like Z, ash, ss. BASH is not only a shell for command processing using standard Linux operating system commands. It can also read and interpret scripts for automation. Bash supports piping,variables, evaluation of conditions, and iteration. 

Commands:
- man (manuals)
- sudo (temporarily upgrade your privileges by prepending the sudo command before you execute a command)
- cat (displays the contents of a file to the screen)
- more (gives you a prompt to continue one page at a time)
- cd (directory navigation) .. (up one directory) / (move to root of the file system) /home/abcd (change dir to an exact too) abcd (change to abcd dir)
- ls (list dir content ) -a (all, list everything. hidden files too) -l (list details. owner, group, privileges) -
- mkdir (directory creation)
- pwd (printing out current work directory)
- cp (copy files)
- mv (move, rename files)
- rm (delete file)
- touch ( create a file and/or change the timestamps on a file's access without opening it)

## Enviromental variables

Environment variables are available in all operating systems and are typically set when you open your terminal from a configuration file associated with your login. You set these variables with similar syntax to how you set them when programming. BASH environment variables contain information about the current session.

- env - list all the environmental variables
- keywords with the = sign tied to values. ```PATH=/directory```
- ```echo $PATH``` prints the PATH variable
- append a variable ```export PATH=$PATH:/Home/bob/mama``` (append because of $PATH is on the right side of the = too)
- to make a variable permanent: ```echo "export PATH=$PATH:/Home/bob/mama" >> .bashrc``` .bashrc containss the session profile
- ```source``` command can be used to reload the variables from the hidden configuration file .bashrc: ```$ source ~/.bashrc```
- ```.``` is also an alias for the source command and used like this```$ . ~/.bashrc```

## Software Version Control (SVC)
Software version control (SVC) typically involves a database that stores current and historical versions of source code to allow multiple people or teams to work on it at the same time. Instead of using inefficient techniques such as file locking, a version control system handles concurrent check-ins, allowing two programmers to commit code at the same time. Another aspect of a version control system is the ability to branch and merge code built independently. By creating a branch, you effectively create a separate work stream that has its own history and does not impact the main **trunk**of the code base. Once the code is written and any conflicts are resolved, the code from the branch can be merged back into the main trunk.

### Git
Git is free and open source. In 2005, Linus Torvalds (the father of Linux) created Git as an alternative to the SCM system BitKeeper. Git was created to be fast and scalable, with a distributed workflow that could support the huge number of contributors to the Linux kernel. **Note** GitHub is not Git. GitHub is a cloud-based social networking platform for programmers.

#### Understanding Git

Git is a distributed version control system built with scalability in mind. It uses a multi-tree structure, and if you look closely at the design, you see that it looks a lot like a file system. (Linus Torvalds is an operating system creator after all.) Git keeps track of three main structures, or trees (see Figure 2-8):

- **Local workspace:** This is where you store source code files, binaries, images, documentation, and whatever else you need.
- **Staging area:** This is an intermediary storage area for items to be synchronized (changes and new items).
- **Head, or local repository:** This is where you store all committed items.

Another very important concept with Git is the file lifecycle. Each file that you add to your working directory has a status attributed to it. This status determines how Git handles the file. Figure 2-9 shows the Git file status lifecycle, which includes the following statuses:

- Untracked: When you first create a file in a directory that Git is managing, it is given an untracked status. Git sees this file but does not perform any type of version control operations on it. For all intents and purposes, the file is invisible to the rest of the world. If you want Git to start tracking a file, you have to explicitly tell it to do so with the **git add** command; once you do this, the status of the file changes to tracked.
- Unmodified: A tracked file in Git is included as part of the repository, and changes are watched. This status means Git is watching for any file changes that are made, but it doesn't see any yet.
- Modified: Whenever you add some code or make a change to the file, Git changes the status of the file to modified. Modified status is where Git sees that you are working on the file but you are not finished. You have to tell Git that you are ready to add a changed (modified) file to the index or staging area by issuing the **git add** command again.
- Staged: Once a changed file is added to the index, Git needs to be able to bundle up your changes and update the local repository. This process is called staging and is accomplished through **git commit**. At this point, your file status is moved back to the tracked status, and it stays there until you make changes to the file in the future and kick off the whole process once again.

If at any point you want to see the status of a file from your repository, you can use the extremely useful command **git status** to learn the status of each file in your local directory.


|Command|syntax|Note|From|To|
|---|---|---|---|---|
|git init|```git init (repo name)```|Initializing a local repository|-|-|
|git clone|```git clone (remote) (local)```|Initializing a repository by downalod a remote location|Remote repo|Local|
|git status|```git status```|checks the reporsitory status|-|-|
|git add|```git add (file) or (. or -A(all file))```|add file to stage|Unstaged|Stage|
|git rm|```git rm (-r "recursive") (-f "force") (folder/file.py)```| remove file from stage|Stage|-|
|git mv|```git mv (-f) (source) (destination)```|rename or move file|-|-|
|git commit|```git commit (-a "add and commit") (-m "your commit message")```|move it from the index or staging area to the local copy of the repository| Stage| Local Repo|
|git remote add|```git remote add (name) (url)```| remote repository creation|-|-|
|git remote -v|```git remote -v```| remote repository listing|-|-|
|git remote rm|```git remote rm (name) ```| remote repository deletion|-|-|
|git push|```git push (remotename) (branchname)```|sync your local repository to the remote repository|Local Repo| Remote Repo|
|git pull|```git pull```|fetches the latest version of the remote master repository and merges it into the local repository|Remote repo| Local Repo|
|git log|```git log```| shows commits with a hash for the repository|-|-|
|git branch|```git branch (-d "delete") <branchname> [commit]```| create new branch |-|-|
|git checkout|```git checkout [-b] (branchname or commit)```| change branch|-|-|
|git merge|```git merge (branchtomerge)```| merge branch into master branch|branch|current branch|
|git diff|```git diff ``` |highlights the differences between your working directory and the index|-|-|
|git diff --cached| ```git diff --cached```|This command shows any changes between the index and your last commit.|-|-|
|git diff HEAD|```git diff HEAD```|shows the differences between your most recent commit and your current working directory.|-|-|
