# PA8-Crispr-GUI

## Learning Objectives

The goal of this assignment is to use basic JavaFX to create
a GUI output representation of the PA6-Crispr program.

Another important goal is to improve the code clarity and
decomposition from the PA6 programming assignment.

## The Assignment

In this assignment, you will build on the PA6-Crispr implementation
to visually represent your ecosystem simulation.

For PA8, you will be graphically representing each animal in 
the output as well as handling a `delay` command from the input file that 
represents how long to wait between the execution of commands. 
In the video example files in the publicTestcases folder, 
each animal (i.e., each character from the PA6 output) is represented 
by a uniquely colored tile on a canvas.

Please open and watch 'PublicTestCases/Ecosystem.mp4' to see an example GUI 
output for the input file 'PublicTestCases/Ecosystem.in'.

You should also be looking at the PA6-Crispr writeup to refresh your memory on 
how it works: https://github.com/Spr19CS210/PA-Drill-Section-Writeups/tree/master/PA6-Crispr

## Delay parameter

The input file format for this assignment is exactly the same as that of PA6-Crispr, 
except that you will now have to handle a delay parameter.
The delay will be specified on the third line of the input file 
right under the 'cols' parameter. An example input is shown below:

```
rows: 6
cols: 6
delay: 3.0

CREATE (0,0) lion left
CREATE (2,2) warbler 3
CREATE (5,5) giraffe right
MOVE 
```

The number after 'delay:' is a **double** that represents the time to wait 
before each command executed. In the video example (PublicTestCases/Ecosystem.mp4),
this delay was set to **.5**, therefore, each command was executed after waiting a half second.

## PA6 Requirement Changes

Your code from PA6 should behave according to the PA6 writeup except in the following ways:

* When animals reproduce the baby should be assigned a gender randomly
* Baby mammals created from a reproduce command should be assigned a direction randomly
* Baby insects created from a reproduce command should be assigned a clockwise boolean randomly

The above changes will lead to a more interesting simulation.

Additionally, you have the option to implement the EAT command, and track whether animals are alive
or not depending on if they have eaten, if they have been eaten, or if they have been alive for too
many turns. Details for these implementations are below under the 'Extra Credit' section.

## Steps for completing this assignment

 1. See a tutorial on how to install the JavaFX plugin in Eclipse at
    https://docs.google.com/document/d/1L5t-rKRHQ3jCCd4cyeCdo21D9zBcV3p0U0cqOjG2d2U/edit?usp=sharing
    The tutorial is also posted on the CS 210 resources webpage 
    https://piazza.com/arizona/spring2019/csc210/resources

 2. Accept the github assignment for PA8, [https://classroom.github.com/a/AR45gqck]
    Import your PA8 github repository into Eclipse as usual.
 
 3. Run the given starter code and see what it does.
 
 4. Copy your PA6 code into the Eclipse project.
 
 5. Fix any issues that your PA6 submission had. Make the above changes to the PA6 requirements.
 
 6. Implement the TODO items in the provided PA8Main.java.
 
 7. Make a video of running `Ecosystem.in` through your program.
    Please consider creating a video file with https://obsproject.com/.  The quick start instructions 
    (https://obsproject.com/wiki/OBS-Studio-Quickstart) are pretty helpful.  
      * Run the PA8Main and leave up the java Ecosystem window.
      * Go into OBS.
      * In OBS, click on Settings in lower right corner and output.  Check that output is mp4 or mov.
      * Click on the add button for a Source.  Select Window Capture, which is at the end of the list.
      * Select Create New.
      * Then select the java [Ecosystem] window in the drop down list that starts out looking blank.
      * At some point you may need to Add Existing Source to get the window to show up in OBS.
      * Then quit the java [Ecosystem]
      * Then in quick succession (kludgy part), click on start recording in OBS and then run Ecosystem 
        in eclipse.  A movie file will be put in whatever directory was specified in Settings.
        If you can figure out how to start recording right when the app starts running, please post that
        information on piazza.


## Resources

The provided code uses some new concepts.  We will be covering them in class.
Additionally, here are some references.

  * drawing to a canvas, https://docs.oracle.com/javafx/2/canvas/jfxpub-canvas.htm
  * lambda functions,http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/Lambda-QuickStart/index.html
  * colors to pick from, https://docs.oracle.com/javase/8/javafx/api/javafx/scene/paint/Color.html


## General requirements

This assignment is different from other assignments you've had so far 
in that you are given a lot more freedom to design your output the way 
you want. You can try to mimic what was done in the video and get the 
credit for it, but however you choose to output your ecosystem, the following 
general requirements must be met:

* Each animal must be **one-of-a-kind**, meaning they must be distinguishable 
  from any other animals and the background. In the example video, this is 
  done by using a different color for each animal against a brown background. 
  You do not have to do it this way, for example, you can choose to use an 
  image for each animal instead of a colored tile.

* There must be a command log which displays commands as they are being executed. 
  In the example video, this is done in a `TextArea` at the bottom of the Ecosystem.
  
* Animals must visually move around the ecosystem.


## Extra Credit

### EAT
For all locations, the first two animals that are at that location should try to eat
each other. Only alive animals should remain in your ecosystem.
  * Birds eat insects. If a bird eats an insect that insect is no longer alive.
  * Insects can eat mammals. If an insect eats a mammal the mammal should remain alive. 
  * Mammals can eat other mammals (yes, we know a giraffe eating a lion doesn't make sense, 
    but for simplicity bear with us).  If a mammal eats another mammal, the eaten mammal should no longer be alive. 
    If two mammals run into each other, the first one at the location should always win.  

### EAT (x,y)
```
EXAMPLE USE: EAT (2,3)
```
Any animals at (row,col) should eat. 

### Eat [type]
```
EXAMPLE USE: Eat lion
```
Has all animals of the specified type eat. If there are no animals with that type, do nothing.


Animals must eat to stay alive. Additionally animals will only stay alive for a certain number of moves.
  * Mammals die of old age after 25 moves, when eaten, or if they haven't eaten in 10 moves.
  * Birds die of old age after 15 moves or if they haven't eaten in 5 moves.
  * Insects die of old age after 10 moves and when eaten.


If you decide to implement these methods, you must show your own test cases and outputs for those 
test cases. Additionally, include a README describing which test cases you used, your implementation, and how it works.


## Grading Criteria

Half of the PA8 grade will correctness.  For this assignment, this is the GUI output.
You should also expect that we might run your program with additional input files 
besides the ones provided.  We will also be viewing your demo video.

The other half of the PA8 grade will be your decomposition and code clarity.

### Decomposition

* Points will be taken off for copy, pasted, and edited code that
  should have been encapsulated in a method.
  
* Should carefully select data structures that implement the required 
  functionality.

* Your program should contain 10 or less java files. All of the Java files should be <350 lines 
  of code.  We won't be including the usage instructions in the file header.

* Each method should be less than 30 lines.  This INCLUDES
  comments, but not the method header.  It is easier to read a 
  function if it can all fit on one screen.

* Make things as simple as possible.
  * Don't use lambda functions or other features in non-standard ways.
  * Reduce the amount of conditional nesting as much as possible.

* Declare collection variables using interface types.

* Your code should be decomposed well. main should be a good summary of 
  your program and no method should be overly long or trivial. Your methods 
  should not be chained. Do NOT have main just call one method that does everything.

 * Redundancy is a grading focus; some tasks are similar in behavior or based off 
   of other tasks. You should avoid repeated logic as much as possible.

Code Clarity
* YOU should be able to read, understand, and explain your own code
  to someone else a couple days after you wrote it.
  * No magic numbers
  * No methods written to just get the test cases to work

* There needs to be a balance between no comments in the body of the
  methods and a comment for every line in the program.  Either extreme
  will result in points off.

* The file header should include instructions on how someone would
  use this program.  To use the program, one would need to know the
  input file format.

* Use meaningful variable names.  Loop iterators can
  be simple (i for integers, s for strings, n for numbers, etc.).

 * We will be modeling some of the issues we are seeing with code.

 * We will ask permission to show clear code examples.


The coding style in terms of spacing, etc. should be done automatically every time you 
save in Eclipse. As long as you stick with those defaults, the syntax style should 
be fine. At workplaces the style requirements can be extensive. In this class, we have 
the following requirements:
 1. No lines should be longer than 80 characters line.
 2. Do not mix tabs and spaces. Use spaces consistently.
 3. The left curly brace should start on the same line as the loop or conditional.

Remember, we will be grading the code that you submitted for PA6 again. Therefore, you must fix any errors 
that were pointed out in your PA6 grading or receive further deductions.
  
## Submission

For this assignment, you are **REQUIRED** to submit all of the following files
to Gradescope before Friday April 5th at 11:30pm.
  * All the Java source files needed to run your program.
  * Ecosystem.mp4, or other video format that can be run on multiple platforms
  
To create the video, you can use a program to record your screen as you run 
your program (see OBS instructions above), or you can simply record your screen 
with your smartphone or tablet. Do note however that the video you submit must 
be of good enough quality for the SL's to clearly see your ecosystem and command logs.

Write your own code. We will be using a tool that finds similar code.

It is recommended that when talking with others about the assignment, do not write
anything down.

