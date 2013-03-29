GSoC-2013
=========

# Google Summer of Code 2013

We are looking forward to working with students on the following
exciting projects: [AutoMan](http://www.automan-lang.org) (a language for programming with people),
[CheckCell](http://github.com/plasma-umass/DataDebug) (a "data debugging" plug-in that finds data bugs in spreadsheets), and [Doppio](http://github.com/plasma-umass/Doppio)
(a *complete* JVM in CoffeeScript).

# AutoMan

*AutoMan* is a library that allows programmers to transparently combine
human expertise with traditional computer programs. This hybrid
computing platform provides a way to solve many of the hard AI problems,
such as vision, motion planning, and natural language understanding
right now. *AutoMan* integrates human-based computation into a standard
programming language as ordinary function calls, which can be intermixed
freely with traditional functions. *AutoMan* abstracts away many of the
issues that make working with human labor challenging, such as
scheduling, payment, and quality control, letting the programmer focus
on solving the problem at hand.

*AutoMan* is currently implemented as a Scala library. Scala is a
relatively new OO/functional language which runs on top of the Java
Virtual Machine (JVM).

## Ideas

Hybrid human-computer programs are a new and exciting area of research,
and we have lots of ideas for making the system easier to use, more
accessible to non-Scala programmers, and more adaptable to the kind of
workload desired by system builders.

## Support for a Java API

*AutoMan* is implemented as a Scala library and domain-specific language
(DSL). While we feel that Scala is a great language, we understand that
many programmers may be deterred by the need to learn a new programming
language just to use our library.

We would like an intern to build a Java interface to allow non-Scala
programs to use AutoMan code. This would also allow other JVM
languages, such as Jython and JRuby to use AutoMan, extending its
applicability to many new programmers.

### Technical Challenges

*   In principle, Scala is already callable by Java code, however the
    Scala API was designed with Scala in mind, so using Java will be
    awkward, as it lacks a few features used extensively by *AutoMan*,
    such as lambdas. An interested intern will need to be creative to
    make *AutoMan* both easy and expressive on the Java platform.

### Ideal Skills

* Experience with Java and Scala.
* Experience with Mechanical Turk.
* A good eye for elegant API design.

## Support for a Web API

*AutoMan* currently requires programmers to write their applications
    as persistent server daemons. While *AutoMan* makes this relatively
    easy, it's a simple fact that interested programmers may not have
    access to an always-on machine that can operate in this fashion.
    Instead, we would like *AutoMan* to be available to clients as a web
    service. Users would then submit jobs to the *AutoMan* web service
    which are then handled asynchronously from the end-user's program.
    This frees the programmer to write programs which can then
    periodically collect completed jobs from the web service.

### Technical Challenges

* The task scheduler and crowdsourcing backend infrastructure will
    need to be split from the client interface.
* A RESTful *AutoMan* web API will need to be designed.
* Users may be wary about sharing their AWS credentials with the
    party running the *AutoMan* web service. We will need to design a
    system that either abstracts these details away or securely handles
    authorizing the web service on the client's behalf.

### Ideal Skills

* Experience with Scala.
* Experience with REST APIs.
* Experience with Mechanical Turk.

## Support for Additional Crowd-Labor Backends

*AutoMan* currently uses Mechanical Turk to recruit workers who
    perform tasks. We would like to expose some additional labor pools
    to *AutoMan* to allow the system to choose labor that may be more
    appropriate for the programmer's task. These services vary by labor
    latency, worker expertise, cost, and worker persistence.
    Additionally, some of these services attempt to do some of their own
    quality control, which may complicate interaction with *AutoMan*.

*   ODesk ([https://www.odesk.com/](https://www.odesk.com/))
*   MobileWorks ([https://www.mobileworks.com/](https://www.mobileworks.com/))
*   SamaSource ([http://samasource.org](http://samasource.org))
*   ClickWorker ([http://www.clickworker.com/en](http://www.clickworker.com/en))
*   ShortTask ([http://shorttask.com/](http://shorttask.com/))
*   CrowdFlower ([http://crowdflower.com/](http://crowdflower.com/))
*   Many, many others!

### Technical Challenges

*  Labor recruitment APIs vary widely from service to service. While
    AutoMan was designed to make it easy to abstract away differences in
    these services, we may find that our view of the world is too
    focused on the way Mechanical Turk works.
*   Our scheduler currently assumes that the programmer only wants to
    use one service at a time. We would like AutoMan to be able to
    dynamically choose the backend without requiring the user to specify
    in advance.
*   Allowing multiple backends complicates the payment model, since
    users will need credentials on all of those systems, and the
    scheduler will need to be aware of possibly different budget
    constraints for each backend. Making it easy for a programmer to
    concisely specify these details will be important from a usability
    standpoint.

### Ideal Skills

* Experience with Scala.
* Experience with REST APIs.
* Experience with Mechanical Turk. Experience with other services a BIG plus.

### More Information

*   Mechanical Turk API documentation may be found here:
   [https://developers.google.com/google-apps/spreadsheets/](http://aws.amazon.com/documentation/mturk/)
*   Documentation for the Mechanical Turk SDK, which AutoMan uses to
    communicate with MTurk may be found here:
     [http://aws.amazon.com/code/695](http://aws.amazon.com/code/695)
*   Our paper about AutoMan, published at OOPSLA 2012, may be found
    here:
    [https://web.cs.umass.edu/publication/details.php?id=2283](http://dl.acm.org/citation.cfm?id=2384663&CFID=153428)\
*  AutoMan code may be found on our GitHub page. Feel free to give it a try!
     [https://github.com/dbarowy/AutoMan](https://github.com/dbarowy/AutoMan)

# CheckCell

*Checkcell* is a tool used to find input errors in spreadsheets. The
tool functions as a plugin for Microsoft Excel, written largely in
C\#.NET.

Spreadsheet errors can have a range of consequences, from the relatively
benign, like small rounding errors, to the profound, like major losses
in financial transactions. Using a combination of program analysis and
statistical hypothesis testing, *Checkcell* flags those input values
which are likely to cause miscalculations severe enough to lead a user
to a wrong conclusion about their data.

## Support for Google Spreadsheets

We would like a GSoC intern to spend some time modifying our codebase so
that it can communicate with Google Spreadsheets.

The current implementation of our tool as a Microsoft Office plugin
means that only end-users who have Microsoft Office may benefit from our
work. We would like to expand our user base by making the tool
available via Google Spreadsheets. This also enhances our ability to
entice end-users to participate in our user studies, since then users
may then use *Checkcell* without needing to install anything.

### Technical Challenges

*   Since the current implementation communicates with Microsoft Excel
    via COM, an intern will need to build a new spreadsheet abstraction
    layer that allows the code to work both with Microsoft Office and
    Google Spreadsheets.
*   Google's spreadsheet API is implemented as a web interface. An
    intern will need to modify our code to run as persistent server
    daemon so as to communicate with the Google Spreadsheets API. This
    also means that the intern will need to create a web interface for
    using the tool with the Google backend.

### Ideal Skills

*   Experience with C\# or Java.
*   Experience with JavaScript.
*   Experience with client/server applications using REST APIs, particularly Google APIs.
*   Experience building interactive web applications.

### More Information

*   The Google Spreadsheets API may be found here: [https://developers.google.com/google-apps/spreadsheets/](https://developers.google.com/google-apps/spreadsheets/)
*   A .NET client library for Google Docs may be found here: [http://code.google.com/p/google-gdata/](http://code.google.com/p/google-gdata/)
*   A preliminary draft of our publication, which describes the *Checkcell* tool, can be found here: [https://web.cs.umass.edu/publication/details.php?id=2283](https://web.cs.umass.edu/publication/details.php?id=2283)

# Doppio

*Doppio* is a fully-featured Java Virtual Machine written in
 CoffeeScript, a dialect of JavaScript, that runs in the browser. It
 adheres closely to the Java Virtual Machine specification in order to
 have compatibility with most programs and languages that run on the
 JVM, such as Java, Kawa-Scheme, with plans to support Scala, Jython, JRuby, Clojure, and
 more!

### Ideal Skills
These skills apply to all of the ideas below.

* Experience with JavaScript (We use [CoffeeScript](http://coffeescript.org/), but it maps directly into JavaScript)
* Experience with Java

## Ideas
We have a large number of ideas, but only a few developers on the project to implement them. Below, we list the most significant ideas that have been on our wishlist. Outside of this list, there are a million different directions in which you can take your project; *Doppio* opens the door to many possibilities!

## Cloud Storage Support
*Doppio* currently reads and writes files to the browser's local storage. This mechanism allows JVM applications to access the same files when the user revisits the webpage on the same computer. With cloud storage support, *Doppio* could read and write files to the user's Google Drive, Dropbox, Box, etc. account, which would allow JVM applications to access the same files regardless of where the user is accessing it from.

We already have a notion of a "file system" in the browser. This project would entail adding support for one or more cloud vendors into this file system.

### Technical Challenges
You may need to modify our file system implementation in order to support cloud storage. You may also want to expose a Java class that can be used by Java programs to log in to cloud storage providers and "mount" them to directories in our in-browser file system.

### Ideal Skills
* Experience interacting with RESTful web services/APIs

## Swing Support
[Swing](http://en.wikipedia.org/wiki/Swing_(Java)) is the Java GUI toolkit. If a Java program has a graphical interface, it is probably implemented using Swing.

We would love for *Doppio* to support Swing programs. We envision that it would draw the graphical interface onto one or more 2D [HTML5 canvas elements](https://developer.mozilla.org/en-US/docs/HTML/Canvas).

Of course, full Swing support might take longer than a summer, so we can start with supporting simple one-window Swing applications and iterate from there.

### Technical Challenges
Swing requires you to define an implementation of core abstract classes, such as [SunGraphicsEnvironment](http://www.docjar.com/docs/api/sun/java2d/SunGraphicsEnvironment.html) and likely others.

The good news here is that these classes usually have well-defined interfaces; your job would be to fill them in so that your implementation mirrors the official implementation. Having a reference implementation makes this type of work a bit easier to manage.

### Ideal Skills
* Experience with simple 2D graphics programming
* Experience with developing interactive applications in the browser

## Frontend for a Learning Environment
Educators have expressed interest in *Doppio* as it could be used to provide students with a simple development environment that is accessible from the web browser. This frontend would remove the difficulty of setting up a development environment on school computers and the students' computers themselves, which lowers the hoops that they have to jump through to begin coding. If you think about it, who hasn't had to reinstall Eclipse mid-project?

There are a large number of directions in which you can take this project. We imagine that you could write a simple IDE that allows students to write and run projects in the browser. We can start with a simple one-file environment, and then expand it to support multiple files.

There are already great editors available (we like the free [Ace Editor](http://ace.ajax.org/#nav=about)) that support syntax highlighting and can be integrated into any webpage.

We also already have a file system that you can take advantage of for persistent storage. By using it, students would be able to resume their project if they visit the webpage again on the same browser on the same computer (and other computers if we implement cloud storage support...).

### Technical Challenges
You will need to interface with *Doppio* for compiling and running Java programs (essentially running `javac file.java`), and you would need to use our in-browser file system for reading/writing project files.

Other than that, the code for this frontend would likely be separate from *Doppio* itself, so you would be starting from a clean slate. You probably would not need to learn anything about *Doppio*'s internals, as you will just be using it as an application.

### Ideal Skills
* Experience with web design
* Experience with writing interactive applications in the web browser
* HCI experience helps, too

## Networking Support
Java applications are able to use sockets to communicate over the network. This project would entail adding networking support to Doppio by taking advantage of WebSockets. You would need to implement core networking methods in the Java Class Library in terms of WebSockets.

### Technical Challenges
For security reasons, WebSockets can only make outgoing connections meaning that you cannot receive connections from outside parties. Furthermore, WebSockets do not operate in the same manner as regular sockets; they use a different network frame format.

One way around WebSocket's limitations is to only support outgoing connections from *Doppio*, and to reimplement core Java networking class methods to be able to handle WebSocket and regular socket requests. This functionality would enable applications running on the Oracle/OpenJDK JVM to interact with *Doppio* applications.

### Ideal Skills
* Experience working with the network stack at the frame level
* Experience with debugging network applications through packet inspection

## JIT Compilation
Currently, *Doppio* interprets JVM bytecodes. It would be great if it could compile JVM methods into JavaScript for execution using Just-In-Time (JIT) compilation.

Getting full-fledged JIT support would be an insane target to meet in a summer. You would likely start with a small goal, and iterate from there.

### Technical Challenges
There are a lot of obstacles in the way of JIT compilation in *Doppio*, including:

* **Asynchronicity**: A number of JVM operations / methods are asynchronous, which means you will need to be able to pause and resume execution somehow. We have ideas for grappling with this problem that we can discuss.
* **Interacting with interpreted methods**: The JIT is going to call interpreted methods from compiled methods, and visa-versa. There are some difficulties associated with switching between these two method types.
* **Debugging Support**: You would likely need/want to build in some debug support for compiled methods into *Doppio*, such as the ability to automatically compare execution output between the bytecode interpreter and the JITed methods.

### Ideal Skills
* Experience writing compilers / interpreters
* Knowledge of asynchronous operations in JavaScript and how they work (callbacks, etc)
* Understanding of how the JVM works regarding bytecodes, its stack-based architecture, etc.
* Some degree of insanity, as JIT Compilation would be a crazy project to choose. :)
