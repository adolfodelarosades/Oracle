# 1: Managing Your PL/SQL Code

* Lesson 16: Using Oracle-Supplied Packages in Application Development - 22m
* PL/SQL Quiz 16 - Content Link
* Practices for Lesson 16 - PL/SQL - 7m
* Lesson 17: PL/SQL Design Considerations - part 1 - 37m
* Lesson 17: PL/SQL Design Considerations - part 2 - 15m
* PL/SQL Quiz 17 - Content Link
* Practices for Lesson 17 - PL/SQL - 26m
* Lesson 18: Using PL/SQL Compiler - 29m
* PL/SQL Quiz 18 - Content Link
* Practices for Lesson 18 - PL/SQL - 12m
* Lesson 19: Managing Dependencies - 31m
* PL/SQL Quiz 19 - Content Link
* Practices for Lesson 19 - PL/SQL - 5m

## Lesson 16: Using Oracle-Supplied Packages in Application Development - 22m

This is Chapter 16, Using Oracle-Supplied Packages in the Development Environment.

So we showed you how to create your own packages. We even showed you a couple of the built-in ones. Just realize that Oracle has scores of other packages doing just about anything you want to do. I'm going to direct you to the OTN site or the docs.oracle.com site to see all of them.

This chapter is just meant as just a cursory overview of a couple of them. DBMS Output we've used a little bit. UTL File, that's kind of the key emphasis here is how to do I/O with operating system files. And then they're going to introduce UTL mail. We don't really have the mail set up here. But the idea is to generate a program that can send an email with or without an attachment. So a couple of these we'll demo in more detail.

And again we have scores of packages to do just about anything you want to do. Go look at the docs.oracle.com site. Look for packages.

And we're just going to show you a couple of them. Now DBMS Output was one of the original debug programs. If you're an old programmer, you know that before the fancy new graphical debuggers, you had to echo information back to the screen. And when a program failed, you looked at the last message that it output, and that's where you want to go inspect the program.

Here we see, again, an abbreviated list, the DBMS output. There's other ones for session information, a scheduling package, HTP does output for web development. Again, this is just a sampling inside here. We'll show you a couple of the benefits. Probably Util File is going to be the big one.

Now DBMS Output, the put line, this was the very first program that you guys used, and we've been using it here. I've got my Show Employees example. This is where, using a cursor, I'll just echo some things back to the screen. So this is DBMS output. So there's the package. Put line just happens to be one of several. On the right-hand side, if I describe DBMS output, it'll show put line.

But it also shows that there is-- in addition to put line, there's a put, there is get lines, there is enable. What DBMS output does, it actually, while the program is running, it writes to a buffer. It does not write directly to the console until after the program finishes successfully or unsuccessfully. But while the program is running, if your program's outputting messages, it buffers it. And then when the program ends, that's when the results are displayed if you have your set server output on.

So this is just to show you that there's a couple options inside here. Notice in my example right here, I have sort of-- if you want to think of it as single spaced output inside here. That's because in the loop I'm just putting the line, and it gives me a new one. Here's where I'll borrow this and show, say, there's-- instead of putting out, say, a blank line, one of them is called new line. So if I put that after each one is echoed, recompile the program, DBMSoutput.new_line.

And now we've got the code compiling. So when I turn around and run this, now you'll see that it puts a new line between each of the programs. And if I were to take that new line, put it, say, outside, and then have a little footer message, this would just be output.putline. And I'll just say Confidential or something like that.

So now instead of putting a new line between each record of output, I'm just doing it at the very end before I show, say, a report footer.

And then let me just introduce you to this. Here's where put line echoes the line with a line feed. If instead I use put, watch what happens here. Now all of the data in this loop will be appended to each other. So you can see right here if I run this, now the data for each record has put the record out. But then it waits and puts the next record inside here. So you can actually create, in this case, an appended string, which then is echoed at the very end with the put line.

Again, I'm not going to get too fancy with it. It's really not used that much for get lines and so on. But it does have that capability. Anyways, that's just a little bit more about DBMS output.

This one here, Util File, is kind of a cool one. This one allows you to write a PL/SQL program that can read and write operating system files. And we talk about operating system. It's on the operating system of the database, so a remote or local database inside here. Now, a couple things supporting this would be a SQL directory. So real quickly, just little administrative things inside here. There is a data dictionary called all_directories. I think I have it over here as well-- yeah-- in my sample code we're going to look at here.

So if you, as this user, look at your all_directories, I'll now see that for my user, I've been given access to one operating system path. And I'm on a Windows system. You may be on a Unix or Linux system. And we've given it a name. So again, just a reminder. A SQL directory is a name given to an operating system, because we can't reference operating system semantics directly.

So I've got this thing called reports_dir. Now keeping that in mind, that's been created. I've been given the appropriate permissions. Util File contains a bunch of procedures and functions to interact programmatically with the file, open the file for reading or writing, getting and retrieving lines, and so on. My job here is not to go into detail about Util File, but just to kind of introduce you to it, and then show you some code that you can kind of cut and paste and use inside here.

So very high level view here just shows that when you open in your program a file, you have to open it for reading or writing or appending. And you have to tell it where it is. That's where that directory object in the file comes into play. If you're reading, obviously, the file has to already exist. If you're writing or appending-- well, with write, technically, it doesn't have to exist. It'll create it anew or overwrite it. Append means it'll add to the existing file.

And then notice my get line and put line, kind of like DBMS output. But instead of putting to the screen, this one is Util File put line, can output to the file. So you can output a line at a time. And then once you're finished, you close the file. And we'll do a little demo here.

Now again, certain things that can happen as you're executing would be exceptions, such as you don't have permission to write to the directory, or you've put the wrong file name or the wrong semantics in. So these are just some of the exceptions you can trap for if needed. Again, I'm not going to get too much into the minutiae of each of these functions and procedures. And in the book, I need to stop the PowerPoint just for a second here and show you guys, on the following page they have some sample code for you to write. I just didn't have it in the PowerPoint there.

I've got this code here as well. And what it is, it's called Read File. And what it's going to do is-- and here's what I was you guys to think this as. Think of this as recipe code. Just like a great baker is not going to remember all the dozens, hundreds, thousands of recipes, don't do the same thing as a programmer. Don't try to memorize every single program. This is an example of recipe code. You kind of cut and paste and store away and then use as needed.

So really just showing that we've got some Util File declarations. This is a buffer that's going to hold information. We are reading from the file. And then notice in here we open the file. So I'm going to give it a directory and file name. I'm going to open the file, and I'm going to open it for reading. So we're going to check to see if it's open, open it for reading.

And then what do I do? Well, I use my get line over and over again. And what get line's going to do is loop from the first line to the last one. Now in my case, I just happened to echo it back to the screen. You don't have to do that if you don't want to. I don't necessarily like that, but that's fine. We'll leave that in. So this will keep looping until there's no more lines to get. At that point, the get line will cause an exception where now I can go ahead and close the file.

So it's actually a pretty concise program. Again, for your use, just go in and copy and paste this and kind of tweak it. Let me go ahead and create this. And I guess before I execute, I'm going to show you where the file that they're referencing is. Now remember, under my reports dir, it said that on my drive here on the C, I've got a temp 2 folder.

So let me open up a folder, and under my C drive I've got a temp 2. Right now I have one file called instructor.txt. I'm going to take a quick peek at it, and it's just a flat file. It just contains data. Doesn't matter what the delimiter is or anything like that. And just notice right down here, you've got Bell, Everett, McCain, and Jones. So keep that in mind. I'll close that.

And let's see if my program that I just created can read from that file. So here's me doing my read file. Actually, what I'll do is I'll move this over to an anonymous block. That's a better demonstration because I'm using it inside of some other PL/SQL code. I'll comment out the show emps here just for a second, and cap that off with a semi-colon.

So I'm asking my program to execute this code, which is going to open the file from that directory and then echo it back to the screen. So here's where-- let's take off the Select statement here and run the code, and there we are. See that? Remember, Bell, Everett McCain and Jones? So now I'm actually looking at that particular file. And it's not retrieving it from the database. This is retrieving it from the file that's out in the operating system.

Just a quick test here. Watch. I'll go edit that file. And so if I come in here to my instructor.txt and down here, change that to Brown or something like that, I'll save the file. I won't have moved anything into the database. So it's still here in the file. And all I have to do now is rerun the report. And you can see that I'm reading that file live. So you see the edited change inside here.

That's a pretty cool little procedure. And again it's using the Util File. So cut and paste the code. That's one example. Let's jump back into the PowerPoint. And now when I jump back inside here, they're going to show some other code. And this code is going to write to a file. So the previous code read from a file. What I'm going to do here is actually write out to a file.

Now we've got the code spread across a couple pages. Let me show you in the code example. So clean things up a little bit. And then here we have, again, recipe code. This one's called Sal Status, give me a directory and a file name. But instead of reading from that directory, noticed what they're going to do here. They're going to write a file. What's the file going to contain? Well, it looks like they've got a cursor set up to get some information from the database. So I'm going to get some information in a cursor and then build a file, so to speak.

Notice my cursor for loop, that executes this query. And then for one record at a time, I'm going to go ahead and put that information out to a file. Now they're being a little fancy. I'm querying department names, last names, and salaries. What they're going to do is grab the department information, and then indent and show the employee information. What am I doing? I'm going to use my put line, but instead of putting it to the monitor, I'm using Util File. So that's going to put it out to the file.

So again, recipe code. Here we check to see if the file is open. We're going to go ahead and open it for writing. Looks like we'll put some header information, new lines, loop through, put one line at a time from the cursor. Remember cursor is really fast. And once I'm done, we'll go ahead and close the file. This is a really fast way of interacting with a file.

Let's modify that. So there, now it's been created. Let's see how they're going to use it. I'll use it the same way I did over here. Let's put it in an actual PL/SQL block. And I'll comment out the read here for a second.

Now this is going to go to the same operating system directory, but it's going to create a file. Now remember, right here I don't have-- all I have is the existing file. I don't yet have that sale report 2. Let's go ahead and run that. And let me see. I put a semi-colon. Let's put the right semi-colon, right syntax. Now the procedure's successfully completed. If I go back to the operating system, there's a file that didn't exist five seconds ago. And if I look at it, that's the content of the file.

So this is a pretty cool feature that lets me, in PL/SQL program, both read and write to operating system files. So I can create my own data upload or data dump type of operations.

And just to finish up here, if I created the file, well, I could certainly read it. So what I'm going to do here is actually use both, one right after the other. And I'll change that to a 3 just to be a little different, and show that. Now I can go ahead and create yet another new file with data from the database. And then I can turn right around and read it with my other procedures.

So see that? I executed it. Both executed. I now have a third file out there. And to confirm and actually see it, I just ran the other procedure to read it. That's pretty cool. So take some of that as sample code, recipe code that you can use on your own.

That's Util File. Let's move into the last one. And we could have picked, , again, scores of other examples to show you. This one just as an overview and introduction to what we call the Util Mail Package. When I write applications where users have to press a button and submit information, maybe to their manager or something like that, behind the scenes I'm executing this Util Mail.

Now it relies on the SMTP output service and the database already being set up and initialized. So the database has to be set to use this. But once I do that, I can programmatically send just messages, or I can send with binary or text attachments. And so the next steps here, these are things that your database administrator would have to do, install the Util mail package, set up and grant the appropriate privileges. But we're going to see some of the code inside here.

So again, these are scripts that would have to be done by the SYSDBA, alter it. And then here's a quick simple example of doing what? Sending a message. Now notice the parameters, even the named parameter inside here, this is a very simplified one. How is this one set up? A quick description shows that send says, in this order you put the sender and the recipients, the carbon copy, blind carbon copy, and so on.

Now the previous page here shows a very simple example, a simple, almost one-sentence message. But if you look down here, the message could actually be a VARCHAR, which can be up to 32K. So you can actually build a pretty big message, not something necessarily that you type, but you could programmatically build a message and then send it.

Now the next version shows Send Attach Ra. One of the arguments in here is an attachment. And then here's a sample of what it might look like. Notice in this one, so I'm sending it-- again, using the named notation. There's the sender, there's the recipients. The message could be an HTML body. Again, this could be built programmatically.

And then we see this attachment using a function called Get Image. Now that's an example of any type of file because it's a binary. Could be a Word file, Excel, PDF, any type inside here. That is a function that they show on the next page inside here. Actually, they'll show it in your sample code on how to write that. And then that also points to a directory.

Now the other variation is just send attach VARCHAR2. And that one just shows that it can be a flat file. And now you're doing attachments, so you can send the body of the message with an attachment. And you can do that programmatically.

All right. Again, just a handful. There are scores of other ones, specialty packages. Look on the OTN and documentation sites for that.

Quick quiz. The UTIL File package is used to access text files in the operating system of the database server. The database provides functionality through directory objects to allow access to specific operating system directories. Sounds kind of like what I demo'd there, so the answer to that is true.

You've already been playing with the DBMS output. We just showed you a few variations. Util File was probably the biggie inside here. And then just an introduction to that. And more documentation on how to write that.

You guys, in the practice, are going to use Util File to generate a text report similar to what I just did. Thank you.

## PL/SQL Quiz 16 - Content Link

PL/SQL Quiz 16

Quiz for PL/SQL lesson 16

https://learn-prodfapap.oracle.com/education/html/pages/UPK/PLSQL_Fundamentals_quiz16/index.html?p_cloud_id=951&p_loid=14524

## Practices for Lesson 16 - PL/SQL - 7m

 
This is the practices for Lesson 16, Using the Oracle-Supplied Packages. In this one, we're going to pretty much do what we did in the lecture portion, and they want us to use util file to generate a text file for departments. That is employees with their job and department, and we'll go ahead and create this using the SAL_REPORT. Now I mentioned that with util file, this type of thing, this is where I refer to this as recipe code. I, in my 20 years, 20 plus years of doing this, I never try to do this sort of off the top my head. So this, as I mentioned, is more of a cut and paste operation.

So I'm going to borrow the code, but I'm going to walk through it a little bit more as to what they're doing. So from the lecture portion, this is the recipe for creating a procedure to write to a file. And so in this one, they want us to call it the Sales Status, and then to arrange the data a certain way. Now this is based off of a query off our Employees table.

And we have deliberately put an ORDER BY clause so that we've got related rows adjacent to one another in the output. So a little setup here-- you will need a variable. Notice the type references the package. This is the cursor we're going to use. Again, any valid query, unions, intersects, subqueries can be used. And then what we're going to do is generate a report header, and we'll do a break at each new department. So as the department rows are read in the cursor, only if the next row that's fetched, if its department is different, will I print out a new header.

So we've created a couple variables. This is where we open the file, the W for writing. And then I start outputting lines, so this is my report. I'll just put in ACME Report, fictitious company. And then new lines, if needed. And now I've got my for loop here. Remember this cursor for loop. It's going to execute the query, and then for each of the records, I'm going to check to see if the old department equals the new department. First record it won't, so we'll print that department and name, but it'll be skipped if the subsequent records are in the same department.

And then I'm just formatting this any way I want. We just happen to be outputting the information with some strings and actual data. And then I'm just, at this point, putting in some new lines. You don't have to do that. Actually, just to be a little different, I'll take that out. Now that's going to go ahead and keep looping, grabbing each of the records until it's finished. Once it's finished, we put a little End of Report, and then we close. So again, this is the standard recipe for interacting with a file open, put lines out, and then close.

Couple exceptions-- this is where, if you've got an invalid file, unable to write to the operating system, maybe permissions or the setup isn't there. But we'll go ahead and create that particular procedure. And then a reminder that in there, you'll also have a directory. So there's a REPORTS_DIR, and they want us to call that. So let's go ahead and show-- I'll come up to the top, and we will execute the sal status. The directory is the REPORTS_DIR, and then the name of the file is going to be out in the operating system.

Now they asked me to use one that was similar to one that I actually created in my lecture portion. You won't have created it yet. They call it salreport2.txt. So I'll call it salreport-- let me make it 5.txt just to be a little different, because right now if I take a quick peek, in my REPORTS-DIR, its' pointing to this directory.

You can see during the lecture, I created a few here. We'll just go ahead and now execute, and there it says, invalid path. That's because I misspelled it. It's REPORTS_DIR. Again, if you want to double check that, go look at your all_directories, so all, underscore, directories will tell us what directory objects I have access to.

And you'll probably have several, in my case, REPORT_DIR, so spell things correctly. Come back. Let's re-execute. Get success, and now if I peek over here, you can see there's a file that didn't exist just a moment ago. And if I open it up, here's what we did. We generated my ACME report header and a couple of new lines, and then you could see a break here at each new department. I'd probably go back, tweak it, put a new line in or something. But now you can see that I've compartmentalized the output into a flat file.

And let's just double check. So we've created the report, and then they didn't ask you, but I went out and showed the content of the file. And that is Practice 16.

## Lesson 17: PL/SQL Design Considerations - part 1 - 37m

OK, folks. This is Chapter 17. It's called PL/SQL design considerations. This is in still Unit 5. The objectives in this one are to touch on a number of different things, all dealing with PL/SQL performance. So we're going to talk about how to make the code faster, more efficient. And so there's a bunch of different bullet points. No logical relationship, necessarily, between them, so I'm going to jump from one topic to the next.

And we'll talk about best practices. Here they talk about constants. We've done a little bit of this before. Get into things like local programs, runtime privileges. Something new here-- autonomous transactions, new things as far as granting roles, execute privileges. And again-- topics we haven't seen before, but parallel enabled. And then once we get to the bottom part here, we'll see how to make our SQL and PL/SQL even faster.

So I'm going to just jump from topic to topic. I'll let you know when we switch there. There's not necessarily a logical flow across the entire chapter. They've grouped the bullet points. We're going to first talk about some best practices as far as standardization, private subprograms, privileges, and so on.

First one in here-- they're just showing that as a best practice get together with your fellow developers and come up with some type of standard as far as programming-- how you're going to maintain the code, how you're going to name your variables. Do you do indentation? Get everyone to do it consistently, and then it makes it easier to maintain, read each other's code, and again, apply that standard across.

We're going to start with exceptions and constants. If you, for business purposes, need to have for clarity different names for either constants or exceptions, one recommendation is to use packages. Remember, a package gets loaded one time into the shared memory area, the SGA. Here they show an example where, if you needed to change the name-- again, for business purposes or something-- for exceptions, consider putting that into a package.

Let me show you that real quickly. So in here, I'll also do it with my test lock. Let me do a little split group. So on the left-hand side, I've got the code showing. And this is just partial code. You'd do it for more examples. But they're saying that for certain exceptions-- in this case, error codes negative 22, 92, and 22 77-- those are, it looks like, foreign key and sequence number exceptions-- what we're going to do is create a package.

Notice only the spec is needed. There's no procedures or functions. No body is-- well, how do we use this? Well, we use it in the Exceptions section, where you guys are used to using the built-in ones, like the win no data found. That's where we could go ahead and send a particular message. So this would be the message. I'm just being generic here.

But if you want to use the package exceptions, now we just use the dot syntax. Put in error_pkg dot-- I'll pick on one of them. This is the FK_BRR. So now whenever an exception-- in this case, a foreign key exception-- occurs, I can trap for it with my package exception name. Go ahead and run that, and you see that-- I just wanted to see that it compiled and was able to reference that successfully. So that's an example of a package for exceptions.

Now, the next example is something we actually saw earlier here they show it in the demo. They're showing an example where, if you standardize on using SQL code, SQL ARM, that's probably a good thing to do. And that's what I do in my when others clause-- let it show the actual error code or error message. I'm echoing it. You can put that into a log file or something if you wanted to. And then the same concept applying to constants. In an earlier lesson, we showed how you could do some constants. I think they were tracking conversions-- miles to kilometers, kilometers to miles.

So they created some variables. This is the same thing, or similar, in that maybe the company has some variables they always want to use, so they're creating a constant package in this case and then the variables. Just like the exceptions, now I can go ahead and reference those by their package name. So this is going to be-- I guess we'll talk about the shipped example here. Again, for me, I'd probably pick a shorter name for the package. But here we'll put in the C order shipped.

So this is just me referencing a variable which happens to be, in this case, the package. So there is the setting. Now you don't have to repeat these definitions, put all of them into a single package. Now you're sharing that code across all the instances. That's a best practice. And again, they're showing referencing it here with an update command.

Next one in here is known as a local subprogram. Kind of interesting-- if you look at the declaration of this procedure, right before the main part of the program, you'll see another definition. This is the definition of a function that is inside the definition of a procedure. This is now known as a local subprogram. And you can do it with functions or procedures, and you can even do it in functions and procedures-- that is, any type of named SQL can have its own function and/or set of procedures so that now if you've got some specialty program or processing that's only needed just for that one procedure, then you don't have to create an outside standalone function.

Create a private function. This means that this can be called from within the procedure, but it can't be called anywhere else. So I'm not able to call that particular function from anywhere else. But a better use of this would be if you're repeating it. If you're using it many times inside the body of the code, that sets up a good example for why you'd want a local subprogram. So that's just doing a simple-- we'll create it. There we see it's called Employee Sal. Then we'll go head and execute. Now, this is just going to retrieve and then display the salary times some tax amount. So if I execute that, there's the 0.825 times whatever that person's salary, employee 100 salary. That's a demonstration of a local subprogram.

Moving on to a different topic-- one of the things that people don't necessarily realize is when they-- I'm going to jump to the program-- when they run a program, the default behavior is that when the program itself runs, like this add department, the database, when it starts doing the commands-- in this case, the insert command-- it actually assumes the privileges of the person who wrote the program. That is, the developer who writes the program, whatever their privileges are, those are the permissions in which the program actually runs. That's known as definers rights. That's the default.

Sometimes, though, the definer-- the programmer-- doesn't necessarily have the appropriate privileges to do what the command is asking here. And so you can set it up so that, as the program runs, it runs with the permissions of the invoker, or what they call the current user. Jumping back here, that's the difference between what they refer to as definers rights versus invokers rights. So prior to-- I forget the version-- version 8 of the database, you only had definers rights. That meant that the person who created the program also had to have the appropriate permissions against whatever objects it was referencing. That was definers rights. That's how the program ran.

Then they changed and allowed for the program to run with the privileges of the current user. That's the person who is running the program, not the person who created it. That also can come into play when you're dealing with unqualified objects. If you don't put in the schema in this case, then running with definers rights would assume that that object belonged to the definer, the actual developer themselves. That's not typically the case. So this would run with whoever the invoker is, and so it would assume it's the users department. So if you had different users, each with their own department table, this would behave differently with the auth ID current users.

Anyways, that's an example of invoker versus definers rights. And then we'll touch on that a little bit later. But let's move on to a different topic. Now, the next topic, we need a little setup. I'm going to create a couple of tables here. I'll explain what these are used for in just a moment. So we've got a usage and a transaction table. And here, these are two new tables. They're both empty at this point. And what I want to do is a quick, simple illustration of tracking. The example they're trying to emulate is if you go up to an ATM machine, a bank machine with your card, maybe to extract or do some changes to your balance, your statement, they want to be able to track that, even if you don't complete the transaction.

And so what they've got is one procedure that logs the usage. So when you put your card into the bank machine, it'll actually insert into the usage table the card and location. I'd probably also put in a time stamp as to when you showed up. But again, this is a simple example. And then notice they do a commit. Well, then they also have a bank transaction that actually does the transaction-- so if you're, in this case, modifying a bank balance or something like that. And here, they're calling that log usage. So they're doing the insert. And notice this procedure is not committing the transaction. They want to leave it up to this procedure to do the insert, and then maybe another transaction, which could include either a commit or a rollback if they cancel out of the transaction or something.

Well, notice what happens here is that when this procedure does the insert, it then calls the log usage. That's the one we saw right here that's inserting into the usage table. But then this one is doing a commit. A potential problem-- if this doesn't insert, even if the commit occurs in the subprogram, you know what? That commit will certainly commit the insert into the usage table, but it will also commit into the transaction table. I don't want that to happen. I want this to potentially be committable or rollback-able if we want it. But still, I want to log the usage and commit that they showed up. So I want to show that they showed up with the card. I want that to be committed. I don't want this commit, which is being done in the subprogram, to affect the transaction that's being done here.

So what we have is something known as an autonomous transaction. This is the illustration in the book here. They're showing that if procedure 1 calls procedure 2 but procedure 1 is doing its own DML commands, like inserts, deletes, and so on, the call to procedure 2, which executes over here, does its own inserts, updates, and in this case, deletes. They want this commit to only apply to what happens in procedure 2. They don't want it to carry over and affect what was happening here.

Now, by default, that's what would happen. That is a commit, even in a subprogram, would commit changes both here and in the outer block, the outer procedure. So what they have here is something known as a precompiler directive autonomous transaction. So if you say pragma autonomous transaction, now what happens is when procedure 1 calls procedure 2, the commit that occurs here only applies to the transactions in procedure 2, leaving procedure 1's transactions to be either committed and/or rolled back. So now procedure 1 can control its own transaction without being affected by the commit of procedure 2.

In my example, I'm going to create these two procedures. There's the one that logs the usage. Here's the one that does the transaction. And what I'd like is that if we do a transaction, we'll see that show up in the Transaction table. So let me go ahead and execute the transaction. I now have two records-- one for the transaction. So if you look right here, I can see there's the usage and transaction. And I would potentially like to maybe undo the transaction, but I still want it to log the usage. So I still want to track if somebody has showed up at the ATM machine, even if they decide to cancel out. So this is where, if I do a rollback, normally, that rollback would apply to both of the inserts that I just did. So that would have, in this case, wiped out that they even showed up at the location.

But here's what happened. Because the usage example committed its own transaction-- see right here, you can see that the usage one, when it did the insert, also committed. But because of the autonomous transaction, it only committed what happened when the log usage occurred. See that? It only committed here. That commit did not carry backwards for this insert, so that's where the rollback undid the transaction. But it still was able to record the usage. So that's an example of an autonomous transaction.

Without that syntax-- that is, without the pragma right here-- the rollback would have undone both of those inserts. So sometimes, you don't want that to happen. They're there doing the demo inside here. So that's the code I just ran-- simple tables, simple example, and then the rollback.

Yet another different topic. This one gets into something new in 12c. Remember, we talked about invokers rights versus definers rights. Well, sometimes, the invoker or the definer don't have the rights, either through roles and permissions, that you want the package to be able to execute with. So in 12c, they allowed the ability to grant a role to a package or a standalone program. So the program has to be created with the invoker's rights.

But then we can go ahead and grant roles to that particular procedure. That means that, again, neither the definer nor the actual invoker, the user themselves, they may not necessarily have permissions to do what the code-- or in this case, the privileges that the code needs. And so here, we're assigning the role specifically to the package or the standalone program. Now, when it runs with invokers rights, it runs with the privileges of the roles that have been granted to it. And that's something new in 12c.

Different topics-- these deal with some performance things. We'll get a no copy parallel. Function result cache-- that's probably one of the key ones here. So let's show those. So the next one in here-- let's see-- they're going to talk about no copy. Now I'm going to bring up an example. And we'll talk about the-- remember the modes-- in mode, out mode of a parameter. For this I'll show my example-- recall with my show employees, I passed in two employee numbers. It selected it for a display. Let's do a quick demo over here.

So if I call my show employees and pass it some numbers here, then that will execute. And I'll retrieve a handful of employees. Let me comment these out just for right now. So what I'm showing you is the parameters are being passed in. Now, if I say this is an in/out mode, that means that I could potentially modify what was passed in. So if I compile that, now we see that in/out can't have a default, so we'll just take off the default here. That's fine. Recompile it. So now it successfully recompiles. There's a successful recompile.

But I can't use constants. Once you say something is an out mode, then the parameter must be a variable. See right here, it says that you can't assign a value to a constant. Now I have to go ahead and use a variable. In fact, what I'll do is I'll use v1 and v2 to pass information. Notice both are being passed in. So I'm passing both information by way of variables.

Well, here's a general term. When I pass the value of the variables, v1 and v2-- remember, this is taking up memory area-- we use terms like-- you may have heard this in other programming languages-- we say that the variable-- in this case, v1-- can be passed by value or by reference. And what I'm going to ask you guys to think for a moment here is when I pass in v1 and v2, how are those being passed in, and what does it mean?

So when I say that v1 is being passed, is it being passed by value or reference? And then the question comes up, what's the difference? And for you CS majors, you know that when you pass by value, you're making a copy. In other words, in memory, where you had the V1, now when I pass that in, it's actually passed in-- whoops. I apologize. Value means passed in as a copy. Reference means you're passing a pointer to the actual memory area. So let me just back up just for a second just to complete that.

So again, when you say that a value is passed, when you pass it by value, it's passed as a copy, a separate memory area. When you pass it as reference, you're pointing to the original memory area. So let's look at this. Since p1 is in only, in means that the value can be passed in. It can't be modified. So that means there is no harm if I were to pass the actual memory area. So v1 is passed by reference.

But here's the thing. Parameter 2 is an out mode, giving permission for the procedure, in this case, to modify the parameter that's passed in. Well, as a safety net, what they do is they say, well, I don't want that to potentially corrupt the original memory area. So out mode variables are not passed by reference, which is a pointer to the original memory area. They are passed by copy. So I actually make a copy of the variable so that v2, while show emps is running, is working on a copy. That means down here, it updates the copy. If everything is successful and no exceptions and so on, then as the program exits, the copy overwrites the original memory area and then goes away. That's all implicitly handled.

Well, not a big deal. It's a little bit of overhead when you have an out mode that's just a scalar data type-- numbers, dates, and so on. But suppose what you're passing is an array, like a collection. Well, now you get into potential issues. Because remember, an array is an in-memory table that could be dozens, hundreds, thousands, millions of rows, and so on. And so if I have an in/out mode that is for a collection type-- in this case, notice what they're doing here. They're saying they're creating a-- or in this case, calling a procedure that is doing what? It has an out mode, in out, and they're passing it a table. See, that's a collection. And that is of that type right here. So it's not a simple scalar data type, like my number. It's a potential collection.

Well, in that case, when you pass by value, now it has to actually copy the entire structure. That's where it can get a little expensive, both in performance and in memory. So if you know that you've handled all the processing and exception handling in the program here, what you might want to do is say that even though it's an out mode, tell it not to copy. So there's something called a NOCOPY hint. It's something you have to play with, do some performance testing and tuning and so on to see if it really affects things. Probably not going to have that big of an effect on a scalar data type. If, however, you're dealing with tables-- in this case, large collections-- this is where you might see some significant overhead. See that? We can enhance performance by reducing the overhead when passing parameters.

Now, the memory is passed by pointer. It's a little two-edged sword, though. They talk about here that what you gain in performance, you might not get if, for some reason, the memory gets corrupted. Because there is no sort of roll back capability. Likewise, this is known as a hint. A hint means that it will do it if it can. If it can't, it just reverts back to the default, which is to copy it. That comes into play if you're dealing with remote procedure calls.

That's a call to a procedure package on a completely different instance. And there, you can't reference the memory. So again, this is a hint, something to test and benchmark. And then they just talk about a few things that you need to keep in mind. So this deals with the collection. It doesn't work with associative arrays, but it does work the nested tables and V arrays.

Again, another topic in here-- let's jump to this next topic. This one is dealing with what we call parallel enabled. Let me scroll down. Yeah. Now, before I show the function, I just want to talk about a feature that came in several versions ago known as a parallelized query or DML statement. Notice I'm being careful. It's parallelized-- not paralyzed, but parallelized query or DML statement. What does that mean?

Well, it means that if you've got a large query or a large DML statement doing dozens, hundreds, thousands, millions of updates, and so on, what you can do is the database will try to spread the load across different processors. So instead of doing all the work on a single processor, if you've got a multi-processor system, it will try to spread the load.

Now, the DBA can get into degrees of parallelization and so on. But I'm just talking generally that now if I do, say, an update command or something that affects millions of rows, instead of having a single processor do it, what I want to be able to do is spread the workload. Well, if you create a function-- let's do this with a little demo here. If I were to give everybody an update-- and maybe that's millions of rows-- but I'm going to use a function. Now, this function is pretty nice. It's going to go in and it's going to double their salary. I probably wouldn't do that.

But I'm just showing that when we use a function-- now, one of the key words in here they're showing is called parallel enable. Let me discuss what that would look like if we didn't use the parallel enable. So if I were to create this function as we normally do and then turn around and run this, again, if this was a really big table, this may take a while. Because at this point-- well, this one says it's out of range. Oh, I've got some triggers in here that are affecting the code. Let's do a simpler calculation. I'll just do plus 1, a simple example. Let's see if that-- I may have to disable the trigger if it's going to interfere. Yeah. It still shows that it's interfering.

So earlier chapter, we talked about triggers. This is where, just for demo purposes, I'm going to restrict the salary. There's the salary check at that point, so I'm going to disable that one just so it doesn't interfere with the command. Now, that's 108 rows-- pretty simple, pretty fast. But if this was 100 million rows-- I work with customers that have billion-row tables-- well, this may take a while, even if you're on a multiprocessor system.

You say, why is that? Well, the database sees that you're executing a function. It has no idea whether that function is dependent or independent of previous or simultaneous executions of the same function. The function may update something which the next call to the function references. See, there is a dependency in that case. So the database, by default, doesn't know that there is or is not a dependency between multiple executions of that function.

So the default behavior is, you know what? I'm only going to have one copy running at a time. That means that in the system here, it's just going to use one processor. So you've ruined, in this case, the parallelization by forcing it to use a single processor. Well, that's where this keyword comes in. Here's where, if you know that parallel executions of the simultaneous copies of the code can be running in memory, you're giving permission to the database. You're telling the database, hey, this function is not dependent on, in this case, a simultaneous execution. And now the database goes, oh, I can update this 100 million row table, and I can spread the workload across the multiple processors.

So if you know you're doing the parallelization for DML and you happen to call a function, by default, it may slow things down. Now we know that we can go in. If there is no dependency on simultaneous execution, we can say, hey, database, you have permission to run multiple copies. That's parallel enabled for parallelizing queries and DML statements.

The next topic in here is pretty cool. This is something they should have implemented years ago, versions ago. But the idea is that functions, when they execute, don't necessarily remember the value of a previous execution. They've got an example using a hire date. I'm going to pick on a slightly different example. One of the things I want to do is deal with potentially large table scans. What I've got is a query that's going to sum up all the salaries, maybe in my 100-million row table or something like that, maybe a million employees. So this is where I want to find out what the grand total is.

Well, if I turn this into a function, which I've just done-- so here's a function called get total that says if you select that sum, put it into a variable, I'll return that variable. So I'm going to create the function that's now going to return that same result, which I just showed. And then over here on my test block, I will call that particular function. So this is the total. This is my grand total. And now I can go ahead and say get total. If I run that, there's the total. That's the sum of all the salaries. Not a big deal.

But suppose I call it multiple times. So in this case here, if I call it once or twice or something like that, or even three times, when I run it, how many times did it have to scan that potentially million-row table? Well, you'd think since it ran it the first time and it got the result, nothing changed about the table, that it should remember that. Well, you know what? It doesn't. It doesn't remember that unless you put in this result cache hint.

Now, if this is not in there-- so if I don't have that result cache hint, then it means every execution of the function has to rerun the entire guts, if you will, rerun the SELECT statement, rescanning the table inside here. Well, this is where we can get it to remember the result by putting this result cache hint. So if we put this result cache hint, now I've recreated the function. And I'll ask you guys-- now when I run this, how many times did it have to scan that table? And the answer is just once. Why? Well, that meant the very first call was able to remember the result so that the next call saw that it was already stored.

Here's the great thing, though. That's called a function result cache. That function result cache is storing it in the SGA. Remember, the SGA is the shared memory area. What that means is that that's available to everybody. So anybody that runs this function for the first time has to go through the effort of getting the results queried, but everyone else gets the result from the SGA. That means it only had to do it once, so it already had the results remembered.

Now, if I run this again, how many times did it scan the table? Well, you know what? None. Why? Because it remembered it from the previous execution. And in fact, anybody that now runs this will see the result much faster than having it requery or re-run the code inside here. That's called a function result cache.

Here's the thing-- it also automatically monitors the table. So the database says any committed changes will invalidate the cache, meaning it'll invalidate and then rerun it the first time. So if you have a situation like data warehouse tables that don't change but say once a day or something, this is a great way to get some summary functions to generate results one time, and then in my reports and graphs and so on, be able to reference that without requerying the table. This is a great result inside here.

There is an optional RELIES_ON clause. In 12c, it does that automatically. In 11g and earlier, you may have to put in a RELIES_ON clause-- something like this, RELES_ON, and then reference the tables or table. If it was a JOIN condition, you could put a comma-delimited list of tables here. And that now means that it will automatically monitor that particular table. This is required in 11g. Not required in 12c. DETERMINISTIC clause-- that's another way of telling the database that it's allowed to run multiple-- in this case, run the function call once so you can avoid redundant calls.

Now I'm going to take a little break. Before we jump into this next topic, let's take a quick break. We'll come back and talk about bulk binding.

## Lesson 17: PL/SQL Design Considerations - part 2 - 15m

All right. Back from our break, we'll continue this last one here. It's a single bullet point, quite a few topics though, dealing with returning clauses, bulk binding. What is this getting into? Well, remember we said that when code executes, when your PL/SQL code executes, some of the code is executed by the PL/SQL engine, some by the SQL engine. Remember, it's happening in memory.

Whenever you have dl commands, you have cursors opening and closing. When you have select statements, cursors opening and closing. Well, that's expensive from a programming perspective, having to manage this memory. So what we're going to see in here is we're going to talk about techniques to cut down on these context switches and extra work that's being done.

To start off, this is just one. Normally, when you insert, update, or delete something in the database, if you want to see what that change was, you have to run a separate select statement. So in the code example here, if I were to give say, a particular employee a 10% raise, I might want to know what is that 10% raise. So that would involve a separate select statement.

Well, here we see something called a returning clause. Notice this returning clause is actually part of the update command. It's not, there's no semi-colon here. This also applies to insert, update, and delete. So here's what you can do. You can update a record and then while the cursor for the update is up and running, you can reference and return values into.

See that INTO clause? That's the INTO that you would have had to use with a select statement. This one deals with a single record because you're just returning into scalar variables. So this is kind of nice. You cut down on the work that it's doing, because you don't have to do a subsequent-- in this case-- a select command. So this is going to show if I update someone's salary, it will have done the update and returned, in order for me to reference. OK? So that's a returning clause. We'll see other ones of doing that.

And here they're disabling a couple of triggers so it doesn't interfere with some of our demos. And I guess they're even doing a roll back. We'll do the rollback to undo that example. And then let's talk about some other techniques. We're familiar with the concept of a for loop. And what I'll do is remind you of that. So here I've got a procedure that raises a salary. We're dealing with a collection. And remember, this collection here allows me to assign some values.

Now I'm just picking on a few. This would be more appropriate if you had a collection of thousands or millions of records. But let's show you-- I'm going to take away this for a second-- and show you the traditional for loop. We say I want to issue some update commands, multiple times. Now this update is going to iterate, the for loop's going to iterate just four times. But again, in a real world example it might be 40,000 or 40 million times.

So what happens with a for loop? Remember, the PL/SQL engine does everything up to the for loop. Then it has to hand control to the SQL engine. That's called a context switch. So it has to switch from the PL/SQL to the SQL engine. Well, when the SQL engine is done doing its update, it has to do a context switch to go back to the PL/SQL for loop so it can come back and do the next iteration, which then does another context switch.

So what it means is, for every iteration, you have to do two handoffs from the PL/SQL to the SQL engine. Not a big deal if you're just dealing with 4 or 5 or even a couple hundred records, and so on. But as this grows, the number of context switches can affect the result. And so if I run this so I could create that code, and then I can turn around and-- let me see here, they're going to execute this raise salary by a certain percentage. So I could execute that raise salary, and there it executed successfully.

All I've done is doubled by however many iterations the context switches. So that means if I've done it four times, the context switches 8. Again, not a big deal with such a small set. Anecdotally, I work with companies that have 100 million row. I work with a company that did 100 million row inserts. And so they had a for loop that was iterating 100 million times. Well, how many context switches? 2 times 100 million, 200 million. So it took their program three hours to run.

We showed him how to use a for loop-- I'm sorry, a for all statement. What this for all does, it looks like a loop, but in a sense it's a loop that belongs to the SQL engine. See, the for loop belongs to the PL/SQL engine, as does the end loop here. The for all uses the same syntax. And in here, I can say, you know what? Loop through that same set of, in this case, collections, from the first to the last.

But here's the thing. This is all handled by the SQL engine. So how many context switches now occur? Well, it doesn't have to go back and forth, it just does one context switch. Now the for loop can iterate through, that is, the SQL engine can iterate through all of the collection. And then it does one context switch. How many context switches total? Two. See, it had to do, in this case, from the PL/SQL to the SQL engine, then the SQL engine iterated through the collection, whether it's four or 400 or 100 million times. And then it does one context switch back.

Well, the company that did the 100 million row inserts, their program when they switched it to a for all went from 17-- I'm sorry, went from 3 hours to 17 minutes. Big improvement. So the larger the set of records you deal with, the more this for all statement can help. And notice, it's also part of the command itself. It's actually part of the insert, update, or delete. That's known as bulk binding. So the idea is that you can do the bulk binding, and then not do the context switches that are happening. Again, small record sets, negligible. As the recordset grows, this is where the for all can help.

We'll will touch on the bulk collect in just a moment here. But again, the idea is that we can do some mass changes. We'll see some of the exceptions inside here. And then they're doing what I just demoed. So they took that list, and to fit it on the page, that's what my list looks like right here. So they populated the collection and then they wanted to quickly make modifications. So inspect, see if you can make your code faster with the for all versus the for loop.

Now they also get in here where you can loop through and find out which particular row you're working on. So they've got some attributes. These are kind of like the SQL %. Remember SQL % row count? This is a SQL % bulk row count. And so this is doing the same thing. And so they're showing that as they run the code, they can do the table. Let me create the table here. And then they're just going to show a quick insert.

So now I'm running this block using the for all. And then inside here, they can show which iteration. So there's where we inserted one row at a time for each of the iterations inside here. OK. So the for all did a mass bulk bind of the inserts. This is my way of seeing what the for all worked with. That's known as a bulk row count.

Now one of the limitations we talked about was with the INTO clause. Remember, one of the restrictions inside here was if you have an INTO clause, how many rows can a select statement return? Well, you know, it's one. We know that we can only return one row inside here. Well, I've got a collection. See that? I want to have a table, a collection of department rows. This is my collection. And if I had to populate this previously, we had to do a for loop. I had to iterate through the dozen, hundreds, thousands of departments and one at a time assign them to the collection.

Now once they're assigned, that makes working with it really fast. See, this is where the for loop at this point, where you're processing the rows, would be really fast. But what was kind of slow was getting the records one at a time. Well, here's where we have something called a bulk collect. This is the first time we've seen this. And a bulk collect says, you know what? We don't have to get one record at a time. I can get all the records.

The analogy that I use is this is analogous to, I'll say it's similar to when you open up a cursor. Remember when you open a cursor, the select statement gets all the records, brings them back at one time? That's what we're doing here, but we're doing it with a collection. So a cursor, let me just work with the rows one time, this is a kind of a mess collection of all of the rows. So I make both operations fast. Now I've got a really fast way to load memory, and then I can iterate through using this bulk collect. Right?

So there's the proper compilation. And you can do this with benchmarking and testing and you would see that this would be significantly faster. Now that bulk collect can also be used with cursors. So if you've got cursor declarations, remember when we open a cursor you usually have to loop through and fetch each one at a time? Well, if what you're doing is taking all the rows from the cursor and moving them into a collection, well consider now using the bulk collect. So this is a way to rewrite some of your cursor declarations.

Notice, no loop is needed because that's a mass move of all of the records. That's called a bulk collect with a fetch. And then here's a command that has everything. In this one, we've got the for all applying to the update. It's updating, in this case, using the reference to the collection. So this means it's going to be a very quick update. And then I also employ a returning clause. Where previously we returned a single value, now I can do a bulk collect.

So this command has everything, all with two context switches. So if I have a collection, I can very quickly process the collection with the SQL engine. And then while the SQL engine finishes processing, it can actually bulk return a bunch of valid values, in this case populating yet another collection if my program needs it. So this is an example of using the bulk collect, the context switches cutting down just to two context switches, eliminating a lot of loops and separate cursors and so on. So that's called a bulk collect.

And then in a set of collections where you may have deleted some entries, that's known as a sparse collection. They have some variations, and where you can save the exceptions and then display those. And then let's see right here, just some variations. Instead of using the 1.. or first to last, they've got another way of saying, you know what? Just say for I in the values of that collection. So this is the one I like to use, then you don't have to worry about sparse collections.

Phew. All right. Big chapter, lot of topics, but we can help build speed. So real quick quiz. The NOCOPY hint allows the compiler to pass the out or in/out parameters by reference rather than value. Remember, pointer versus copy. This enhances performance by reducing overhead. And the answer to that is true. So if I don't have to copy it, then I can get much faster execution, right? So that's true.

So we've covered a lot of things. Probably the biggest ones would be the function result cache, getting it to remember results. And then the bulk binding. Other ones useful, things like no copy, autonomous transactions, knowing the difference between definers and invokers rights-- that's probably something to keep in mind. All right. You guys are going to practice with the bulk fetch and the autonomous transaction in Practice 17.

## PL/SQL Quiz 17 - Content Link

PL/SQL Quiz 17

Quiz for PL/SQL lesson 17

View Content https://learn-prodfapap.oracle.com/education/html/pages/UPK/PLSQL_Fundamentals_quiz17/index.html?p_cloud_id=951&p_loid=14525

## Practices for Lesson 17 - PL/SQL - 26m

And this is the practices for lesson 17. So design considerations for PL/SQL. So in this one right here, we're going to create a package that performs some bulk fetch of faculty information for specified jobs.

The data's going to be stored in a PL/SQL table in a package-- that's a collection. You can also provide a procedure to display the contents. Likewise, you'll create an add_faculty procedure that inserts new faculties. Procedure uses a local autonomous subprogram to write a log to log each record each time, whether it successfully adds the record or not.

So a couple things before starting the practice. They want us to download a file, write some code, and then let's take a look. Let's jump ahead here.

So here's the practice. We're going to use that same faculty package in here. We're going to add a get_faculty procedure with the job_id.

So let's go into the syntax. Here's my faculty. And there's already the get_faculty. So we're going to overload this. So there's a procedure called get_faculty to functions. And there's the overloaded one right here.

Let's jump down by the job_id. I already created that ahead of time. But that's the one they wanted you to create. I'd probably put it up next to this procedure here.

So we've got several. There they're doing it by the faculty ID, salary, and job. Couple of functions. This one's going to do it by just the job_id. And they want me to populate the collection.

Let's jump back. Oh. Right here they want to create a nested table. They probably should have had us create that first. But I think they did that because they were creating this in the package body. So there's the get procedure-- get_faculty-- in the package spec.

Now if I jump to the package body, we'll see the current get_jobs. But let's jump up to the top here. And here we're going to create the Boolean table. This was done in a previous lab.

And then what they want us to do is add in the new get_jobs. So let's make sure. So here's the add. There's the one that takes three arguments. There's the two functions.

And then actually here's a spot where we're going to go ahead and put in the new procedure. So this is borrowing from here. We want to add in the procedure. So here's where we'll put in the new get_faculty. And that's a procedure. So we've got the is, begin, null, and end.

So let's see if this compiles. And it does. So there we've got the packaged started. Now what they want us to do is to do a bulk collect and populate this faculty table. So that's going to be of the faculty table type.

So I know I need to put something into this, since it's based off of the row. Here's where I'll select the entire row into pulling this from the faculty_details. But I'm going to do it where it's based on the job_id that we're passing in. So this is where the job_id equals the parameter that we're passing in.

Restriction, though. That select into it only require one row. I might get a bunch of rows here. So this is where I use the bulk collect. That's the bulk binding technique inside here.

Let's compile that. And table or view does not exist. Faculty. Run it again. And everything's good. So there's the proper messages. So that's that part.

Let's see here. Creating a procedure. So we've used the bulk fetch. That's the bulk collect. Now we create a new procedure in the spec and body called show_faculty.

So let's jump in. Now what is it going to do? It doesn't take any arguments. Displays the contents of that table.

So a quick jump here. There's the show_faculty. So there's the syntax for that one. No arguments.

Now we jump to the body. And it looks like in here they've already got things kind of flushed out. Let's do show procedure, show_faculty is. There's a begin and an end. Let's do a dummy statement. And just get it to compile. So whoops, I see a typo already. Procedure. So there's a procedure.

And then we can echo something back to the screen. So I know I'm going to use my DBMS output. Let's go grab the dbms_output.put_line.

And then what I'm going to output is the contents of that faculty table. So this is the faculty_table. That's the collection. And we'll put a for loop.

Most likely I'm going to reference it as i. So I need to loop through. I'm going to say for i in 1 dot dot whatever the count is. So the faculty_table.count. Let's go ahead and do a loop. And then there's my end loop.

But I'm only going to do this if the table has something. So we don't necessarily need to run through this. I can say if the faculty table is not null. So this is just a predicate that will check that there's anything there before I even try to do it. So let's end the if statement.

And let me just double-check. So that'll just output the records there. What I'll probably do is just maybe put a little header at this point. So this is going to be the Faculty-- Faculties in the package. We'll call it in the package collection, or in memory table-- whatever.

So put a little header. Then it's going to output. Let's compile. And it says, wrong number of types to PUT_LINE. PUT_LINE, dbms_output.put_line Oh, down here. dbms_output.put_line. And what did I do with that one? So that's going to take the faculty_table.

Oh. Let's jump back up. So that faculty_table is a faculty table type. And this is up in the definition right here. Ah, it's a row ID. So it's not just a single one. This is the ad_faculty_details.

So let's jump back here. Let's take a quick peek at the ad_faculty_details. Just trying to find an open spot here, and trying to remember all the values.

So inside here, in the package body, when I ask it to show, I need to specify which column I want to see. So this is the Faculties. So over here the faculty IDs, I guess. So it'll be the faculty_id. That's a dot faculty ID. Let's try that one.

And there we go. And we could also put the name or something like that if I wanted to. Actually, let's do that. They didn't ask for that in the output here. But I usually like to see some personal information.

So we'll ask it to also show the let's do last name. Compile that. So there's the procedure to show.

And then, whoops. Let's demo this. So it says invoke the get and show for the [INAUDIBLE]. Let's do the show_faculty. This is my faculty package, show. Over here we can now do a execute faculty package dot show_faculty.

And you know what I need to do. I need to set server output on. And I also need to get the faculty. So I need to kind of set it first. So here we'll just copy and paste that.

And they wanted me to pick. So this is get. I want to get the faculty members who, let's see. Which one did they want? They wanted the FA_ST. So let's do the faculty staff. That will set the stage. And then that right there should display the two people who are in that. So that's reading it from the collection.

And then one last one. FA_HOD. That's the head of department. So we'll set the collection, and then read the current collection. So a different set of folks.

That's that one. That finishes up Task 1.

One other task here is Task 2. The manager wants to keep a log of whenever the add_faculty procedure in the package is invoked, to insert a new faculty. It's going to be able to log this. They've got a lab to create a table. I've already got that lab up and running. This is 17-2. It's going to create a log table.

So an entry ID, user, time. We'll use the sequence here for the primary key generator. That's my new. I'm sorry. LOG_NEW. Let's double-check under the tables here. Yep there it is. See? There's my LOG_NEW.

And then not sure if that has already been created. It has. That's all right. So you guys are going to create those two.

Let's jump back and see what they do want us to do here. So we've executed that in the faculty package. Add a new add_faculty procedure which performs the actual insert. Add the procedure called audit. So we're going to add that one as well.

And for this we'll use an autonomous transaction to insert a log record. So in here they want a new add_faculty to perform the actual insert. So we're going to modify.

So let's go down. So here's the add_faculty. This is the one that takes. So this is sort of already been done for us. Let me take that out for a second.

So there's my add_faculty. And they want me to add a local procedure-- so a private one called audit new faculty-- and insert a new record inside here.

So this means following the is, where I normally declare a variable. So I can now create a private procedure. So it's going to be a procedure. What did we call it? Audit the new faculty. And we say it is the following.

And we're going to have a pragma. I'll put it here. pragma autonomous_transaction.

Now we can declare what we're going to keep. Store the user current time, faculty name in the log table. The current user is going to be my v_user. That's usually a varchar. It's going to be based off my user function.

And then there's the user function returning. And then a begin and an end with my dummy statement. So let's compile this just to make sure I've started off on the right foot here. And it looks good.

So now I can do the actual insert into that table. So looking at this one, we can see there's the log new. So there's a number, the string date, and another string.

So let's do an insert. So insert into the new-- actually, it's called log. New faculty. And the values are going to be, just to double-check, it's the ID user time and name. So the ID user time and name.

The ID is going to be based off this sequence. So that's the log_newfac sequence. So we can make that dot nextval. I will grab the next value there.

And then the user is going to be based off of the variable I just created at the top. The time is going to be sysdate-- that'll grab the time.

And then what else did they want? They wanted the name. So in this case, this is going to be the p_first_name and last_name that are passed in right here. So that's going to be the p_first_name. It's a single column. So we'll just put the full identifier. Last_name.

That should work. Let's see if this compiles. All right. That's good. And when you do a pragma with the autonomous transaction, when this runs you actually have to do the commit.

So the idea is now I've created this local procedure. And now they actually want me to call it. So store the username. Use the log_newfac in the entry. Modify the add_faculty. Now invoke the procedure.

So there's the audit new. And now when it goes to insert, we're also going to audit.

So there's that. So here they're calling. So now I'm going to go ahead and call that private program. So that's doing the step. And it'll commit the record.

And then let's go ahead and test this. Let me just double-check. So one last compile. Make sure everything is good. Now we can come over and test it. And this is going to be my faculty add_faculty.

And before I run this I'll look at the table. And what do we have? We've got some record. Who do they want me to put in here? Ah, we'll make up some names. We'll put in, yeah, Max Smart. So Maxwell Smart, I guess is the FA_SF. So Max Smart FA_SF. So there's Max Smart.

As I recall, it's going to be the email address. And it's going to be the job. That's going to be the FA_SF. And then a null salary for right now.

Now before I run this, let me show, if I look at this audit log, just let me go ahead and just do a select star from the log_newfac table. That should be empty. And actually, did I do that correct? log_newfac. [INAUDIBLE] log_new-- not "lob." Log.

Oh. It already ran once. See? I already ran it one time as a test. That's Steve Morris. And if I execute this, there the procedure succeeded.

And then I go ahead. And I can see now there's two entries inside here. That's even if I decide to undo it. I didn't do a commit of that record. So I should see right now that there's Max, row 13. But if I do a rollback, now querying this undoes the entry for Mac, as far as into the faculty_details table.

But I, in this case, shouldn't have done a rollback on the insert. So this is showing that we can monitor something and commit the change, even though the outer transaction didn't work. And that is the end of Practice 17.

## Lesson 18: Using PL/SQL Compiler - 29m

And this is chapter 18, using the PL/SQL compiler. Getting in still to unit 5, almost toward the end here. After this lesson, we'll introduce you to some of the PL/SQL compiler initialization parameters, something called compiler-time warnings. Now, just jumping back here, we're used to the compiler. Remember when we edit a program and we hit the gear icon, that's the compiler compiling the program. And all we've seen so far is that the compiler either successfully did the job-- no errors, program can run.

Or it didn't. I'm going to put a typo in here. We'll put a couple x's at that point. Now you'll see that instead of the message that it compiled successfully, I get error messages. Well that's all we've seen. We've either seen no messages or error messages. That's the red x's. But it doesn't necessarily mean that if you fix the code that everything is necessarily good. We can see under this Messages here that it did compile, the previous one just compiled with errors. This one just compiled, but no errors.

But if you look at the code, you can say well, at this point, the function, if you're looking right here, does return. But remember, when a function returns, that's the end of the function. So what we have is a situation where, see that line of code? That line will never get executed. Even though it passed compilation, it really won't do well if I go to call it.

In fact, watch right here. If I now say show me the result when I pass it two numbers. Over on the right-hand side, I'm just calculating 22 times 77. And when I go ahead and run that, you'll see that, at this point, it comes back-- well first of all, it says it can't be used as a target there. Let's change that to a variable. I'll just call v2. That's fine. And when I now go ahead and multiply that to get, nothing comes back.

Now this might be a candidate for debugging, but this is where, why didn't the compiler tell me? Why didn't the compiler tell me that the program was going to run and that code would never execute? Well, we didn't tell it to. All we told to do was tell us error messages. So there's another set of messages known as warning messages, which the compiler can look for and tell you about. It's just that you have to turn these on, all right?

So we'll talk about compiler warnings in the second part of the chapter here. Before we do that, though, get into optimization parameters for code type, what we call optimize levels. These are settings you can set for your environment that influence how the compiler compiles or warns you. And the first one we're going to get into is something called PL/SQL code type. I'll touch on optimize level in a moment here.

When we run a program, that is, when we compile a program, we think it's compiling it down to the machine code-- the ones and zeros. But in reality, all code, whether it's a function, trigger, procedure, or whatever, actually compiles to an interpreted mode. That means that it has to run through a last-second interpreter in order for it to execute. That's a little bit more overhead than a truly compile program.

There's a table out there. It's called USER_PLSQL_OBJECT_SETTINGS that can tell us how the current code is stored, all right? I'm going to show you the entire table. They're just showing a couple columns. We've got room. So I'm going to show you what this USER_PLSQL_OBJECT_SETTINGS table shows. And if you order it, it'll-- thus case, we'll do it alphabetically. I'll order it by name. Now you can see I've got an alphabetic listing of all my procedures, triggers, functions.

And then what it's telling me is when this program runs, it's going to be run in INTERPRETED mode. That's because that's the default setting, as opposed to what we call native code. So what's the difference? Well native code is compiled actually down to machine code. It's not run through an interpreter. So native code tends to run faster, depending on the operation you're doing. If they're I/O or CPU intensive, native code can run anywhere from 5%, to 20%, to 30% faster-- especially for CPU intensive things like working with collections.

If you're working with collections, code that is native can run significantly faster. In fact, all code runs faster native than it does interpreted. So why do we even have interpreted? Well, in order to do debugging, in order to run the debug, you have to have the code in interpreted mode. And so that's why on a development system, you leave that PL/SQL_CODE_TYPE setting unchanged, and you do all your debugging and testing.

But if you move it to QA performance system or a production system, the recommendation is in this case, compile all your code in native mode. How do you do that? You can set the session. In fact, there's a way to set the system. I'm just a regular user here. I'm not the system administrator. But if I was, I could set the entire system so that when any programmer compiles a program, it'll go to native mode versus interpreted.

Now this only affects from this point forward. So if I alter my session right now-- you can see the session's altered-- it has not changed anything that's already been compiled. So if I requery-- let's go back here. If I requery the table, you'll see that nothing has changed. It just means that from this point forward, if I either recompile or as I create things, they'll be now saved in, in this case, native mode.

Let's pick on a couple programs here. And I'll embed this. Let's pick on one of my procedures. So there's a couple procedures and you can see there's my ADD_COURSE. Now you can recompile this a couple ways. We could pop it up in an editor. So if I do an editor and just hit the gear icon, that recompiles the program, OK?

If I use the command line, I could alter a procedure and recompile it that way. Let's pick on my ADD_FACULTY. And for this one, I'll do a right mouse and just compile it right here. So I've compiled a couple of different ways. Watch when I requery the table. We'll now see that those two are now stored in native code.

Now can you tell when you execute any one particular procedure or function that it runs faster? Probably not, but overall, if all of your code is native, you'll see a significant increase in performance of all your PL/SQL code-- triggers, functions, procedures, packages, and so on. So this is probably the quickest and easiest way to improve the performance on your system. I go to a lot of sites where the even long-time DBAs don't realize this particular setting.

So I would do this. Monday morning, go in to your DBA, ask them to select-- in that case, they'll select all PLSQL_OBJECT_SETTINGS, ask them to query that and see how code is currently stored, and therefore executed. It runs either way, so it doesn't matter whether it's interpreted or native. It runs the same. You don't change the functionality. It's just that if it's native, it'll run faster.

And what I'm doing here at the session level can also be done at the system level. It's even in a .ora setting, because that's called PLSQL_CODE_TYPE. And again, for production environments, keep it interpreted so you could do debug-- I'm sorry-- development environments keep it interpreted so you can do debugging, in production change it to native.

Now what's this other setting in here? There's that PL/SQL table here, looking at that. There's something also known as the optimize. See that? OPTIMIZE_LEVEL one, two, and so on. This is another compiler setting. What you do with the OPTIMIZE_LEVEL is you're telling the compiler to interrogate the code to see if it can maybe improve either the size storage or performance of the system.

By changing the OPTIMIZE_LEVEL to zero, one, two, or three, you're telling the compiler to spend less or more time inspecting the code. OPTIMIZE_LEVEL 0 means it basically compiles the code the way you wrote it, so to speak. That might include-- let's take a quick peek here. That might include like variables that you declare but never reference, OK?

So if I compile this function-- we'll get into fixing this in a moment-- when I compile this function, if you declare variables or exceptions that will never execute, a LEVEL 0 will compile that into the finished source code-- I'm sorry, into the finished machine code. This does not change your source code. So this OPTIMIZE_LEVEL will only change the compile version of the code, not your source code. So the idea is that LEVEL 0 is the fastest way, but it might have some unnecessary stuff inside there.

As you change the level from zero to one, to two and three, you're asking the compiler to spend more and more time. Now you can read up on the optimize levels, but one means that it may look at the code and see that that's not needed, so not to the source code, but in the compile code, it may eliminate that.

Changing to a LEVEL 2 may actually rearrange the code. This is a real small example, but if I had a larger example, it may actually shift code around. Again, not to change the logic of your program, but to change how it actually compiles and executes. It's trying to optimize, trying to make it run faster.

We showed an example earlier where you had a private subprogram, in an example where you had a private subprogram where you call it in the main part. Well that call-out involves a context switch. That's where if you change to a LEVEL 3, the compiler may say, you know what, I can actually compile the actual code at the place where the private subprogram is called. That means less context switches and faster execution.

Something you have to play with and benchmark, you can also set the OPTIMIZE_LEVEL here. Now these are command line ways of setting it. There's also-- they don't show it, but there's a GUI way as well under my Tool Preferences. If we look under the Database, there's Compiler options. And this is where you can set, system-wide, or in this case, for your particular session here, one of those levels.

Now the default is actually level 2, and so you can go ahead and keep that as the default. Or you can go ahead and set that to level 3. And all that does is now you don't have to set it each time you come in with a command line one, OK? That means that when I compile the code, and then I look at it in that user objects settings, we'll see that in my case, I just recompile that function-- what is it-- CALCTOT, and you can see now it's taking both settings. It's taking the OPTIMIZE_LEVEL as well as the CODE_TYPE. And ideally we've got faster executing code. That's what these compiler options do.

Now, another thing the compiler can do is right now it's only sending us either it successfully compiled or we get error messages. What it's not doing is warning us. There are a series of warning messages which we can ask it to turn on and off. Right now you can see that this compiled successfully, no error messages. But it's not warning me about, say, some potential issues.

So let's see. Now there's several ways to turn on and off warnings. You can do it through a command line, you can do it through the GUI, you can even do it through a package call. You can execute a package that turns on and off these. We're going to show each. And the idea is to turn them on so that when you compile a program you can see and maybe follow the warnings.

Warnings don't stop the program from executing. So with a warning, you still have syntactically correct code, it just may be improved if you follow some of their advice. So we have some potential issues that you could address. Now the warnings come in three different categories-- INFORMATIONAL, the lowest level one, PERFORMANCE, and then SEVERE. You can turn on any combination, or you can turn on all of them, depending on what level of messages you want to receive.

We're going to do the declarative and GUI way. And then we'll show the programmatic way to turn those on as well. The command line way is with an ALTER command, just like we altered the code type settings just a moment ago, we're going to be able to alter the sessions. This is a setting you can do, but it only does it for the current session. So I don't usually use this one. Let me collapse this for a moment. And then just show that, just like you altered the code setting, here I'm saying let's alter my session so that from now on, I want to see severe messages, I want to see performance messages, but I don't want to see informational messages.

Well, you know what? Let me show you all of them. Actually, before I turn this on, just a reminder that right now my calctot function is compiling successfully, even though I noted a few potential issues in here. See no warning messages, also no warning messages, but only error messages.

All right, let's turn this on. My session's been altered. Now from now on until I exit out, notice when I now compile, instead of seeing just the regular message that it compiled, now you see it compiled with warnings. Now you can ignore warnings. You don't have to follow the advice. It just means that you might. So we'll look at some of these.

In fact, notice right here it comes back and it says at the bottom, 8,3 unreachable code. Well line 8, starting in position three, is that code that will never execute. And why is that? Because the function returns before it executes. See that? I'm seeing that when I look at this warning message. Again, it's not the red x's, it's the yellow triangles.

Other ones, this one says that P2 may benefit from a NOCOPY copy hint, CALCTOT returns without a value. Let's address these a little bit at a time. So if you ignore it, that's fine. The program still runs, may misbehave a little bit. Let's change it though. Let's go ahead and I'm going to move my return clause. And what I should see, now when I recompile, so I'll recompile, and we'll see that that warning went away. See that?

So I didn't have to, but I addressed the problem. This one says P2 may benefit from a NOCOPY hint. Let's follow that advice. Let's go ahead and put a NOCOPY. Remember that applied to the value verses reference and recompile it. And you see that when I-- now my warnings are going down. Let me see. Oops, I've got to spell this correctly-- nocopy. So there's the NOCOPY hint, and the warnings are going down.

Now some of these I don't necessarily need to follow. Like it's asking me to do the AUTHID, you know, definer, current user, or something like that. I don't necessarily have to follow that. And then you can turn on and off by using this ALTER command with the enable or disable. So set that.

I don't necessarily use this. I like to use the GUI way, because it remembers it from session to session. So let's do this. I'm going to go under my Tools and Preferences, and then that same place, that same node I went to under Database Compiler, this is where we saw the optimize level just a moment ago. We also see the warnings. And so you can enable which category of messages you want to see. I like it because now I don't have to run that alter command each time.

And then, now as I compile the program, it'll pop up and show me warnings. At some point, though, this is me personally. I usually turn off the warnings if I'm working with a program and I know that I just want to see that it compiled properly. I'm ignoring the warnings, so to speak. I may go in, and under the Preferences maybe turn off the INFORMATIONAL and the PERFORMANCE-related messages, but have it still show me what it considers SEVERE messages.

So you can have it still show some warnings and not others. Here it's not really showing me-- it just said that it compiled with warnings, it's just not showing them to me, or you can turn off all of the warning messages. Now that's the two ways to do it through the ALTER command or the GUI way, through the point and click. And then, again, it's a way of seeing that in the warning level.

I'm also going to show-- now they're demoing what I've already done, that is turned it on and then compile the program. Do you see the warning? See PLW? That's the PL/SQL warning message or code. It's not an error code. So the idea is to recompile the program, follow some of the advice, ignore others if you're not interested in doing it, and then you can turn that off.

Now the third way of doing it, turning on and off warning messages, is done programmatically. Similar to the ALTER command. You're just running a package to set it. And so in here you'll see examples for setting and turning things off. I'm not going to get into full detail, but you can capture the current settings and then set them to something a little different. So this is their DBMS_WARNING. Execute this to get or set warning levels.

And they show the example. I'll bring the ALTER command, just so you can see that it looks very similar. So there's the ALTER command way of doing it, and then, right here, you'll see the programmatic way of doing it. So see I could run a-- I call that a command line way of turning on and off messages. Here they're calling the package-- now they're using EXECUTE, but this could technically be inside of a begin and end.

And this is now a programmatic way, in this case, enable all of the messages and so on. So these are similar, it's just that this is done through a package procedure execution, this is done through an ALTER SESSION command.

All right, that's the package way. And again, they're just showing you examples on how to set those inside here. They give us some sample code. This is a programmer's program for you guys, if you want to use it-- or not. And so they've got a procedure. What it does is it compiles programs. You know what? They didn't give me the code for that one. No big deal. Let me see if I can actually-- I can't cut and paste it.

So let me just walk through this. They didn't actually give me the code. So notice in this one, they have a program called compile_code and then recall the ability to do dynamic SQL allows me to append objects with strings, creating a dynamic command, which initially starts off as a string but then there's my EXECUTE IMMEDIATE. So there's my ability to execute.

And then, beforehand, they're using the DBMS_WARNING package to get the current environment settings, add some new ones, echo it back to the screen. Then I can run the ALTER command with my settings, and then they reset. They reset and show that the settings have been restored. All right, that's just some sample code. Use it if you'd like. Now you just run the program to alter your session. So that's using the compile_code.

Lastly, this is something new that came out in 11g, and it deals with the when others clause-- talks about sort of best practices here. One of the things I did, you saw me when I compiled my program here, I want to show some messages. Let me quickly go up and show one of the warning messages.

So I'm going to turn on all of my warning messages and then recompile. And I want you to note what it's telling me here. My compiler comes back and it says that at this point, your program returns without a value at line 12. Well, what's line 12? Line 12 is the end of the program. It says that if I properly return, that's great. So what happens if an exception occurs? Well notice what I said, if an exception occurs , well then don't do anything. That's kind of odd behavior.

Let me kind of force the issue. Instead of doing a multiplication, I'm going to do a divide by. So I'm going to say whatever two numbers you pass in, this calculate total function's going to divide the two numbers. And I'll ignore the warnings. Let's jump to the test and show that it will do the job. So if I now say 22 and I pass in the variable, instead of seeing the product of those two numbers, it's going to show when I divide 22 by 104. See that? It's doing a proper-- in this case, it's doing a proper calculation and returning the result, OK?

So that's the expected usage. If I now come in and change that value, then you'll see that, again, it's doing the result. But suppose I change this to zero. See if I change that to zero, now it's going to take this divided by the second argument. And you know when you divide by zero, what happens? Well, in this case it says, hey, the function returned without a value. I didn't get a zero divide error, what I got is this unusual result. It said, you know what? Your function returned, but what-- it really didn't do anything. See that? It returned without a value.

So what it's asking, it said when others clause, you really shouldn't do nothing. Now I could do a negative 1. So watch if I compile this, now any time I have a zero divide situation, we'll go ahead and return, in this case, what the function says it's going to return. So that should be a proper compilation. So this now says when I divide by zero, it returns negative one. Now, it's still sort of a bad practice. I might want to instead do something a little different.

So here's the recommendation. So the recommendation is that if you have a when others, you really should propagate out the exception that got it to that point. And you can do that with a RAISE or a RAISE_APPLICATION error, OK? So we raised the exception that got it to that point, or RAISE_APPLICATION error. If you just use the word "raise," now instead of returning with no value, whatever exception got trapped will now be passed on to the calling environment, which is a better practice.

So now if my calculation does divide by zero, now the outer block can come back and you can see here, now the exception was passed and I get my divisor is equal to zero. That's that negative 1476. So this is kind of a best practice. All we're showing is that's a warning that now pops up.

And they're showing the same thing. They're showing a WHEN OTHERS, it does nothing. And you see that message. So it's a best practices.

All right, of the warnings, quick quiz here. The category of PL/SQL compile-time warnings are a, SEVERE, b, PERFORMANCE, c, INFORMATIONAL, ALL of the above, I guess, or e, CRITICAL. And you remember the three types. They were the SEVERE, PERFORMANCE, and INFORMATIONAL. So it's a, b, and c, not e.

All right, so compilers have settings. We can tweak them. Look on your production system, make sure that all your code is being saved to native code, as well as optimize. And then occasionally you may want to see warnings. I usually do that at the beginning when I'm creating a new package or procedure, just to see if it catches anything. I usually turn it off after that. I don't want to be annoyed by the warnings all the time. But again, that's a setting you can turn on, either command line, programmatically, or through the GUI wizard.

And that's what you guys are going to do. You're going to play with the initialization parameters, compile, look at the settings, and then see some of the warnings. That's your practice 18.

## PL/SQL Quiz 18 - Content Link

PL/SQL Quiz 18

Quiz for PL/SQL lesson 18

View Content https://learn-prodfapap.oracle.com/education/html/pages/UPK/PLSQL_Fundamentals_quiz18/index.html?p_cloud_id=951&p_loid=14526

## Practices for Lesson 18 - PL/SQL - 12m

And this is practices for lesson 18, Using the PL/SQL Compiler. So a series of small steps in this practice. We're going to go ahead and display the compiler-initialization parameters. And this will enable us to do native compilation. We will also play with the compiler warnings, see how to turn on and suppress them, and then identify just some different categories of compiler-warning messages.

Just a series of small tasks. First one, display the following information about the compiler-initialization parameters by using the USER_PLSQL_OBJECT_SETTINGS. That's the data dictionary. So note the settings for the ADD_JOB_HISTORY. We will jump to here. I'm going to do a select star from USER_PLSQL_OBJECT_SETTING. And then we could certainly read this. But they want us to do the object name, type, mode, and optimize. So that's going to be the name, the type, then the plsql_code_type.

And let me just double check. So the object type, compiler mode, and optimization level. So there's the compiler mode and optimization. So that's going to be the plsql_optimize_level. So now we're just pulling selected columns out of that. And then it wanted us to look at the settings for the ADD_JOB_HISTORY. We will put an order by name, and that'll get the ADD_JOB_HISTORY.

Notice it's currently stored as INTERPRETED Optimize Level 1. OK that's the first step. Next one, alter the PLSQL_CODE_TYPE parameter to enable the native compilation. And then we'll compile the ADD_STUDENT. Now, let's take a quick peek at the ADD_STUDENT just to see it's also interpreted before we do that. So next thing is we will alter the session, set the PLSQL_CODE_TYPE.

And remember, the two options are INTERPRETED or NATIVE. So we'll change that to NATIVE. This just affects our session. It doesn't affect anything currently. That is, we alter the session, peek here real quick, and show that everything is still the way it was. So our ADD_STUDENT still INTERPRETED and so on. But now we can go ahead and recompile the ADD_STUDENT.

A couple of ways to do that from the Connection tab. We could open up and then, from the procedure, just do a right mouse click and recompile. We could open it up in Editor and recompile. Or we can use the command lines. We could say alter procedure add_student and then compile. So that will run just the one command. And a quick peek at the table shows that now my ADD_STUDENT is stored and will run in NATIVE mode. So I can do that now with a series of the procedures, in fact, all of my PL/SQL code.

That's step 2. 3, we'll go into the Tool, Preferences and disable all compiler warning categories. So step 3, go up to our Tools, Preferences. Compiler warnings are underneath the database node. And there's our compiler options. And right now, it looks like everything is currently disabled. So that's step 3. And then, here, it says they want us to edit the script for the unreachable code.

This says lab 11. It's actually lab 18. Slight typo. In the Solutions file, it does have the correct one. I've already taken liberty of opening that particular file. So it's lab 18-4. And this is UNREACHABLE_CODE. Now, what do they mean by that? So it's a simple example here that just shows, in the IF construct, if you were to look at this logically, you'd see that this variable was set to TRUE.

And if you're looking at the code here, it means that if this particular procedure runs, the only thing that will ever execute is this. This line, at least in this example, will never be executed. So they consider that unreachable. Well, right now, if I create that procedure and then edit-- let's refresh. And then down here, there's the UNREACHABLE_CODE . If you bring this up and then compile, it should compile successfully. And right there, you can see that there's no warnings, no error messages, and so on.

So it just looks like it compiled cleanly. And it did. But there's no error messages or warnings. So we click the Run. We've created the procedure. What are the compiler warnings displaying, if any. And another way to see the information instead of looking at this message is from a script. You can do a select from a user errors. And that shows the last compilation inside here. That doesn't pertain to this one. This pertains to the CALCTOT procedure we executed or compiled earlier.

So no feedback on the UNREACHABLE_CODE section right here. Let's go ahead and see what they want. It says enable all the warnings and then recompile the code and use the error data dictionary. So we'll do all three. Let's go back up to Tool, Preferences, opened up to the last node. And we'll turn on. So we're going to turn on the different categories of messages, say OK, go back.

Now, in the Editor, if we go ahead and do this, we'll now see that, when it compiles, we do get a couple of warning messages inside here. One of them is that indication that we have UNREACHABLE_CODE at line 7. We should see the same thing when we re-execute this USER_ERRORS. So executing this now shows again for the UNREACHABLE_CODE example. We do have UNREACHABLE_CODE.

And again, it's just a warning. It's not going to prevent the code from executing. So that was the steps there. That was 7, 8, 9, again, just to interrogate. Lastly, we have a step here. It says create a script named warning_msgs that executes the DBMS_OUTPUT. And using the DBMS_WARNING package to identify the categories of messages for some selected message numbers.

Let's do this one here. So, in here, there's the-- we could use a begin and end. And then I know I want to use my dbms_output.put_line and then the dbms_warning package and then get category. This will tell me if it's an INFORMATIONAL or SEVERE or PERFORMANCE message. And we could hard code this in. We can also get prompted. So I'll just use a little prompt for the code. I'll just say code here.

That is a small script. And again, we could use the execute as well. Now, let's see which ones they wanted us to look at, so 550. So if I run this, the first time, type in 550-- oh, I'm sorry-- 5050. Is that right? Let me just double check. Yeah, 5050. And the procedure completes-- oh, we forgot to set serveroutput on. So just a reminder there.

Oh, one other thing. Whenever you get this prompt, you always see the feedback as well, what they call the verification, the old and new. There's a setting in here you can say set verify off. That just eliminates that feedback. So once more, 5050. See what category that is. That's considered a SEVERE message.

6075, run that again. 6075, that falls in the INFORMATIONAL. And 7100, run that again. 7100, and that's a PERFORMANCE. So we can look up in the documentation to see the actual errors associated with those anyways. Those are the different categories of messages. And that's practice 18.

## Lesson 19: Managing Dependencies - 31m

OK, folks. This is Chapter 19, Managing Dependencies. Get into some more of the administrative aspects of PL/SQL code, talk about some of the things like dependencies between code. How do I track what program's calling what program?

And then we'll see when you make a change to a program, how does that affect other programs? If you break one program, that could potentially impact others. How do we see that? So we're going to talk about the concept of dependent and referenced objects.

Quick example here. If I show you a procedure, this is my show employees procedure. This procedure only works if all the objects that it's referencing are there. So things like the employees table has to be there. The DBMS package has to be there. I'm making a call to a function here called get_sal.

So we would say that show_emps is referencing these packages, procedures, tables, and so on, but not necessarily the other way. In other words, the employee table doesn't necessarily care that the show_emps procedures is there or not, so there's no dependency between the existence of the procedure as far as the table is concerned. So that's what they're just pointing out, is that some objects can be both dependent on others and/or referenced by objects.

And here they're just showing that dependencies can be indirect. Example here, if I have a view that's referencing a table, but then I have a procedure that's referencing the view, there's not a direct dependency with the procedure and the table, but there is indirectly. In other words, if something happened with the table, it could impact the view, which could impact the procedure.

And they just show that to another level. So we would say that Procedure A depends on Procedure B, which depends on View A, and so on.

All right. How do we see this? Well, the database automatically tracks. Every single time you compile a program or create an object, the database interrogates itself to see, in this case, what objects you're referencing and are being referenced by that. We can see that through a data dictionary. There's a data dictionary called user_dependencies, a great one to look at.

I'll do a quick query of that table. And I guess if we order it-- well, I'll leave it unordered just for a second, just to show that what you see are all of your objects, not just PL/SQL objects, but procedures, functions, tables, triggers, and so on.

And then, yeah, let's put an order by, just a little easier to see. I'm going to order by the first column. That's the Name column. And you can see inside here that this is showing the name of a particular procedure. And the way I read this is I can now say that my ADD_COURSE procedure is referencing this function called valid department. It's also referencing the DBMS standard package, as well as the standard and details and so on. So it's also referencing that table.

Let's scroll down to say my employees table. Actually, I'll jump down to the show employees that I just demonstrated. Yeah. So there's my show_emps. And sure enough, we see that it is referencing the employees table, the standard package-- that's where your round and to_char and truncate functions come from. GET_SAL was the function. DBMS_OUTPUT is the package, which is really just a synonym to the package.

So this is the objects that show-emps is dependent upon. Now, if I sort of this another way, I might want to say I see that show_emps is referencing the employee table. What other objects are referencing the employee table? So instead of ordering or sorting by that, I'll order by the referenced name. That'll sort it by this column here.

Re-run the query. I could certainly put a where clause in. In fact, let's do where the reference_name is equal to employees. I want to see all the objects that are referencing the employees table, or in this case, the object employees. So see, right here I've got a view that references the employee table. I've got triggers, functions, procedures. Scrolling down, there's my show employees example.

So I call this an impact report. The question comes up that says, well, gee I see this table called employees. Maybe I want to drop it. What's the impact? What is it going to affect?

Well, if I were to drop this table, you know what? All these objects would be broken. See that? All these triggers and so on. And the database would actually recognize that. It would automatically invalidate all those objects. Even if I never referenced them, it would know that these objects are dependent. It would see this object is no longer there, so it would actually invalidate. Invalidated code and objects can't run until they are validated again.

Now, I'm not going to be as drastic as getting rid of the employee table. It's dependent on too many things and constraints that are going to stop me here. But I did create a table called emp, which is just a copy of it. And so just a quick query of that shows that it is an actual table. I'm going to show you sort of the impact here. Just want to show that it's a copy of my employees table.

So I'm going to make my show_emps reference it. Get that to compile properly. See, it found that object. Go back to that user dependency table. And for this one, we'll switch this just to the emp table.

And notice right now, show_emps is the only thing pointing to the emp table. They call it a hard dependency because it's a direct reference. Now, what would happen if that dependency was broken?

Well, here we can see these are the different statuses of an object. This also brings up another table you guys should get used to. That's going to be the user_objects. So remember, user_objects is the data dictionary that shows all the objects.

If we sort this, order by the first column OBJECT_NAME, I'll even do a descending sort just to get a little closer. And I'll look inside here. One of the things about an object is whether it's currently valid or invalid. So there's all my different types inside here.

Most of the objects are valid. I'll just look at the object name and its status. And again, the database only runs the code that is valid.

Notice there is something here HR package is invalid. Just a little heads-up. The GUI tool does the same thing. If I expand this, there's my HR package. And notice the red X that pops up. So whenever the GUI tool displays, it's really just looking at this same status. And it's just showing anything that's invalid just won't run.

It won't run immediately. It has to be validated before it can run. That might involve the database automatically re-compiling it when you go to use it. So we'll get into a little bit of that right there.

And then what I want to show is that it does this invalidation automatically. So right now we see that show employees, the show_emp procedure that I created, was valid. That's because the table does still exist.

And then I'll do something a little drastic here. I'm going to drop-- I'm going to drop the table. That's probably one of the more drastic things you can do. I'm going to drop the emp table. So now it's dropped.

And then when I re-query-- I didn't touch the procedures and functions that pointed to it, but if I re-query this user_objects table and now look for the invalid status, you'll see that show_emps is now flagged as invalid. Same thing here in the connections if we look at the procedures. Now, this one has to be refreshed. But if I refresh the procedures, we'll see that the red X shows that's invalid.

So code cannot run if it's invalid. Just to prove that inside here, if I now try to call my show_emps running that-- let's give it a few proper arguments here. There's where it's going to come back. And see right here, it says, hey, show_emps is invalid.

Now, it actually tried to help us out a little bit. One thing about any object that's invalid is instead of waiting for you to go fix it, the database actually goes and re-compiles the PL/SQL triggers procedures and so on of invalid objects when you go to use them. So just by trying to run it again, it would have seen that it was invalid. And it would try to re-compile the program to see if somehow the issue had been resolved, that is, the table maybe had been recreated. So we'll touch on that a little bit inside here.

These are the statuses of objects. It's either valid or invalid. Either you don't have access or it's compiled with errors. Now, invalid doesn't mean is has errors per se. It just means that an object that was referenced isn't there at that point.

And they're trying to demo that like I'm doing here. And they're looking at that user object. They're doing it through a view. I just did it through a procedure.

And then here's where-- now, since this particular view-- let's take a quick peek. This was selecting all the columns from the employee table for this view. Even modification-- see that. Just modifying one of the columns of the table the view was pointing to invalidates the view. That is, the database sees that the view was working with that and something happened. Doesn't necessarily have to be drastic like dropping, but something happened. It just means it's temporarily invalid until you use it again. As long as you haven't broken it, then it should re-compile and be valid again.

All right. Now to help navigate that user dependency table-- there's that user dependency table-- you could follow it from one object to the next and see indirect types of references as well. But it's a little hard, so several years ago, someone created a script and it sets up a little sort of table inside here. And they call it the utility dependency tree.

Now, in this case, we have to execute some code. Out in the labs directories, there's a script. Now, this is in the install. When you install the database, you get this util tree, utildtree. That's a utility dependency tree script.

Run it one time in your schema, and it will go through and create some objects inside here. I probably should have just run it directly. It's just doing some dropping and creating and we're just watching it inside here. So it creates a little table we can fill with things, as well as some functions and procedures.

So once this has been created, you then can populate it using this procedure. So we execute the procedure. And the idea is you pick on a particular object, like in my case the employee table. So we're also going to-- what that procedure's going to do is populate this dependency tree table, which is currently empty. So right now that should be empty, haven't put anything in it.

And the way that we clear and populate it is by executing this dependency tree. Now, I'm picking on the employee table. It has populated this. And the way that this queries the information back is through what we call a hierarchical query, if you've heard of tree-structured queries. This is where the object you're interested in shows up as Level 0. Think of that as like the root node of a branching tree.

And then inside here, you'll see that from that, it will show Level 1 objects. Anything that's a Level 1 is directly referencing the Level 0. That means all of these views and triggers are directly referencing the employee table.

If you see a Level 2, it means that it's referencing the Level 1 right above it. It's branching out at that point. And this would actually go to a Level 3, 4, 5. In other words, this shows you the level of indirection or indirect relationships that exist.

If you're interested in another object, just re-populate it, change the object name here. That's going to clear out the table and then reset it with the new object. So here I'm picking on the department table. We haven't been working with that as much, so it's not as much feedback here.

So again, Level 0's the root. Level 1 points directly to Level 0. Level 2 points to Level 1. 3 would show that as deep as you need to. So it's a useful tree to see what other objects are related to others. And that's the demo they're showing inside here.

All right. Now in 10g and earlier, if you just made a slight change to an object, anything that was pointing to the object was invalidated. But sometimes, though, the slight change really didn't impact the procedure or function. And so there was some unnecessary invalidation and therefore unnecessary re-compilations. So what 11g and beyond has done is implemented something called fine-grained dependency. And I'm going to go ahead and show an example with my show employees.

I'll switch this back to the employees table, re-compile, and then in this example, I don't really need all of the columns. So just to make it a little easier, I'm going to just get the employee_id, last_name, job_id, and salary. So that's really all I'm referencing, so I'm deliberately leaving a few columns out. This should still compile, so it compiles successfully.

And I want you to notice that my query is only referencing these columns from the employee table. So technically, it's only dependent on these columns. It's not dependent on maybe other columns inside the database.

Well, what does this mean? Well, when I track this code, when I look at the user_objects table-- let's go ahead and show-- where's my user-- yeah. See, they're doing a query between that and user_objects. I don't need to see all of that.

I just want to show you-- you know what? I'll go up to-- I'll put a little bookmark there for a second. And yeah, right here.

So this is the user object query. And I'm going to pick on my show_emps. This is where the-- object_name equals show_emps. That's my procedure. And right now, it's a valid object.

And then if I were to modify one of the columns that's referenced, the database would recognize that and invalidate the procedure automatically. So watch this. If I now said let's alter the table employees-- and I'm going to modify. I'm not going to delete anything, but I'll just modify the last_name column and we'll redefine it as a var-- I'm going to bump up the size. We'll make it 40 instead of I think 25 is what it currently is.

Now, by modifying the last_name column, that has a potential impact on the show employees table. So if I run this alter command, you can see there it altered the table. Then I look here. I'll see that the database has flagged show_emps as invalid. And that's what it should do, because what I changed could potentially impact on the show employees table.

Now it's up to me to validate that. I could do that by either re-compiling the program, but what you can also do is just call it again. This is what's nice is that you don't have to sort of visit the invalid object. All you have to do is reference it again, and as long as the change that was made wasn't drastic enough to keep it broken, watch what happens here.

When I now go ahead and run this, we'll see that it has successfully run. Now, in my case, it didn't bring anything back. But it successfully ran show_emps. Well, that was an invalid object. Well, not anymore.

If I go back, there it was invalid just a moment ago. If I re-query, we'll see that it's now valid. What happened? Well, what happened was the database in executing this block ran into an invalid object. But before it complained or forced you to manually re-compile, it actually re-compiled it itself. And it re-compiled and saw that the change that had made it invalid really has no effect, so it now validated.

That's a good thing. It means you don't have to go and do a lot of changes sometimes when you tweak your code. So that's the example that they show there.

But let's do something else. Notice my show_emps is not referencing say the email column. So I am not referencing in the employee table the email column, so let's go ahead and modify that one. So in here I'm going to alter employees. We're going to change the email column. And we'll bump it up to 50 or something like that, and I'm just making it a little larger.

Notice that altered the table. But here's where fine-grained dependency kicks in. In 10g and earlier, because I changed the table, the database would have automatically invalidated the employee table-- I'm sorry, my show_emps procedure, just because it was referencing the employee table. But fine-grained dependency means that if what I changed has no effect on the table, then it'll go ahead and leave it in that valid status.

So there's where we could see that now when the program runs, we can see that-- I should've run it. When I run it, it now shows that it's in a valid status. That's called fine-grained dependency. So it looks within the unit to see if the individual objects have been modified.

They're trying to do a demo here with this CREATE TABLE and then CREATE a VIEW off the table. So the table has columns a, b, and c. And then the view is just querying columns a and b. They look and see that that view is certainly valid, and then they add a new column to the table.

Well, if you look back, adding a new column has no effect on the SELECT statements for the view. So 10g, just because I modified Table 2, 10g would have flagged that view as invalid. 11g, which is what they're querying here, shows that it's still valid.

All right. That's they're making a change showing the valid versus invalid status. And then they do the same thing here dealing with packages. But again, that's all happening. Now it used to be that changing a synonym also invalidated. Here they've tried to mitigate that, and just changing a synonym doesn't invalidate the object.

Let's move along a little bit more. And so they give us some tips on reducing the concepts of invalidation. And again, nothing can run, no object can run if it's invalid. But validation automatically occurs when it's referenced, so the user just by calling the program can sometimes get it to re-compile. Now, obviously if it re-compiles and remains broken, well, then the code breaks and you have to go fix it.

Now what about remote dependencies? This whole week we've been talking about executing code that exists on our own system, so all of the code that we've executed has existed on my database and obviously in my schema here. But what if I execute a procedure or want to execute a procedure on a remote system?

We don't get too much into that. But if you have something known as a database link, you can make a call to a completely different database instance. Just as an example, we don't show it here, but if for some reason I had a function or the procedure itself was on a completely different instance through a database link we could get to it through this type of syntax. The DBA would have to create what is essentially a name for logging into a remote system. They get that information from the remote administrator.

But that's where, in this example, if I had a get_sal that was on say a headquarters database under a different schema, the link would be created that points to that schema. Now when I go ahead and execute, now the local database knows that it has to go across the network to get that function, to execute, pass that information and return it and so on. Now, I don't actually have that, but that's what the syntax might actually look like.

Well, how are dependencies handled here? If it's all local, the local dependencies automatically know when things are valid or invalid. If you're remote, it doesn't do that, so they used to employ something called a TIMESTAMP check. TIMESTAMP check just said that when the-- so let's resort this back to the at link. So when my local procedure compiles, it checks the timestamp of the remote procedure or function so that this can keep track of when that program was last compiled.

That means every single time it executes, it compares the timestamp. That just means if the timestamps are different, then this system knows that that has changed. Well, you know what? They really shouldn't depend on the time of when this changed. It really should only depend if the way you call it has changed. In words, if the signature has changed.

Let's say they still said this get_sal took a number. Well, I don't care when it was last compiled, so I don't really care about a TIMESTAMP check. But if for some reason they changed this and instead of a number maybe they made it an email address or something like that, now that's significant. So there, the signature may have changed on the remote system and your program wouldn't know about it.

So instead of having it do what we refer to as a TIMESTAMP check, we can do a SIGNATURE check. This is something usually set up at the beginning. It can be done through an init.ora setting. That's the recommended way.

And again, signature is probably the better way, because then it doesn't care when or how often the remote procedure is re-compiled. You only care, your program should only care if the signature, the number or the data types of the parameters, actually changes. And that's what they're trying to show. They're trying to show remote change is normally a TIMESTAMP comparison between the two. In our case, we just need to check to see if how you call it is the same, so signature mode is the recommended way.

And then a few asides here. They're just getting into some ALTER commands on how to compile either procedures, functions, and packages. You've actually seen this throughout the course. So this is if you wanted to explicitly compile.

And then things will remain broken. So if you have an invalid object and you try to re-compile it, it'll remain broken if obviously the object it's referencing is dropped or renamed; if the column has changed name, not necessarily size-wise; if the column is dropped; if a view with different columns pops up; and so on. It kind of makes sense. If the object is missing, then your code will unsuccessfully re-compile and remain valid. Now, if it re-compiles and in this case new columns are there that weren't referenced before or the columns haven't changed or a private table now is replaced by a public table, then it'll be successfully re-compiled.

Throughout the course we've been trying to show shortcuts. This actually helps to mitigate or minimize dependencies. So early on we showed you how to use the percent type or row type. The nice thing is that means that every time you run the program, should the data type or row type of the record change, your code can automatically accommodate that. Now, it may not fix everything, but it can minimize dependencies.

And then they're just going through the dependency between a package body and a package spec. And this is where a package spec may remain valid but the body itself may not be because it's referencing a procedure or something.

All right. Quick quiz. You can display direct and indirect dependencies by running the utldtree, utility dependency tree, script, populating the temp table, and then querying the DEPTREE view. And the answer is that is true. That's what we actually did to see the impact reports on various objects.

So lots of data dictionaries, check the dependencies, user objects, PL/SQL object settings, and so on. Keep those in mind as you do your debugging and coding, and again create your impact reports. You're going to run that script and then type in a few select objects inside here and then practice some re-compliation. That's Practice 19.

## PL/SQL Quiz 19 - Content Link

PL/SQL Quiz 19

Quiz for PL/SQL lesson 19

View Content https://learn-prodfapap.oracle.com/education/html/pages/UPK/PLSQL_Fundamentals_quiz19/index.html?p_cloud_id=951&p_loid=14527

## Practices for Lesson 19 - PL/SQL - 5m

This is the practices for Lesson 19, Managing Dependencies. So in this one, we're going to go ahead and use that dependency tree fill procedure against the IDEPTREE-- in this case, dependency tree view-- to investigate dependencies for objects in the schema. First of all, we have to create the procedures, functions, packages, that's going to have us execute. So we're going to load the tree structure showing the following dependencies for a couple of functions and procedures.

These were functions, procedures created in Practice 3. You can open up the solution file if you don't have those. So we need to load and execute the utility dependency tree script. Let's do that first. I've already gone out and opened it up. Here's the contents of the file.

Execute it. It's going to take a few moments as it runs through. Again, this is going to be creating the table view and sort of help procedures. And when it's finished right here, we now have these objects created.

OK. We've loaded and executed the script. Now we just need to fill the view with information about a selected procedure or functions. We use the deptreefill. This is execute deptree, dependency tree fill. And this is a procedure. I'll give the schema-- TEACH_B is mine-- and then the procedure name ADD_FACULTY.

Execute that. That gets the table filled. Now it's just a matter of doing a select * from the ideptree and seeing the output. Now that's not very informative there. Let's see if the other one's better.

Valid_job is a procedure, so we'll change this to VALIDJOB. Let me just double check-- VALID_JOBID And I'm going to double check that we actually have that as a useful function. So there's VALID_JOBID. So this is a function. It'll clear out the old one and then we can query it again.

Now again, not be the best examples. In the lecture portion, we showed better examples. One was if we look at my show_emp procedure, that's the one I had referenced-- or actually, it was EMPLOYEES. This was the table. Those are little bit better because you can see all the other objects. And there's the EMPLOYEES table.

Now I can look. And a little bit more information inside here. So we can see, the indentation indicates the level of a dependency between those. So there's direct and indirect dependencies. All right. That's the exercise. And that's the end of Chapter 19.
