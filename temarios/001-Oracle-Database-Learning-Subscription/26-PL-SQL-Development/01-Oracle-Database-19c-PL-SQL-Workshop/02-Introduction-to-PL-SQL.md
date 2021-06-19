# 2: Introduction to PL/SQL

* Introduction to PL/SQL - New - 30m
* Practice 2-1: Introduction to PL/SQL - New - 7m

## 01 Introduction to PL/SQL - New - 30m

OK, my friends let's take a look at Chapter 2, an Introduction to PL/SQL. We are here in Unit 1. Notice Lesson 2, PL/SQL Overview.

And let's take a look at the objectives. After completing this lesson, you should be able to do the following-- explain the needs for PL/SQL, explain the benefits of PL/SQL, identify the different types of PL/SQL blocks, and output messages in PL/SQL.

OK, first up on the agenda, understanding the benefits and structure of PL/SQL. Now, some of the limitations of SQL are listed here. SQL performs one operation at a time on the database and lacks the capability of logically grouping multiple database operations. And so with PL/SQL, that's going to enable modularization in the application. And it's going to provide better security, enables maintainability, and also provides for exception handling.

Now, modularization-- what does that mean? So we like to think about doing a task and only that task as part of a unit of work. And so if I had, say, five different things that I wanted to do to my data, what I would do is I would divide that up into five individual tasks. Each one of those tasks, we would consider that being a module.

So I might end up having five different procedures, for instance, in order to handle those five different tasks. And so the idea with modularization is you break up this really complex tasks into smaller units of work. And we're going to be talking more about security and exception handling.

But as far as the maintainability, if you are going to store objects in the database as compiled subprograms-- like procedures, and functions, and triggers-- then if you wanted to go and make changes to those objects, since they're stored in the database, you can just go find it in the database. And you can quickly and easily edit it as long as you have the added capabilities in that particular object. And so that makes it easier to maintain because it is stored in the database. There's only one version of that object stored in the database. And it's easier to maintain as a consequence.

So here we have an example of somebody trying to log in to, maybe, an application. And they are presented with a page that has a place to put a username and a place to put a password and then a button called Submit. And what's going to happen is when they click the Submit button with their username and password parameters, those are going to go into a PL/SQL object in the database, most likely a function. And then that function is going to return a true or a false.

If that function returns a true, then they're going to be able to log into the application. If the function returns a false, then maybe we're going to send them to an error page instead. And so the response is going to be generated based on the output from the PL/SQL program unit.

So what does it stand for? What does PL/SQL stand for? It stands for Procedural Language Extension to SQL. It integrates procedural constructs with SQL. It provides a block structure for executable units of code. It provides procedural constructs, such as variables, constants, and data types, and also control structures, things like loops and conditional control statements.

So conditional statements are if, then, else, or case, for instance. And it allows us to write reusable program units. We write it, we compile it, we store it in the database, and then we reuse that stored object over and over and over again.

Now, for about the first 30% of this class, we're going to be talking about anonymous blocks. Anonymous blocks are not stored in the database as stored objects. So those need to be compiled every time they're used. And they're compiled as they're used automatically.

And then, eventually, we're going to show you how to start storing these in the database as stored objects. But we're going to teach you about anonymous block structure first, because we need to teach you the basics of the language first before we start applying that to stored objects.

So some additional benefits PL/SQL-- integration of procedural constructs with SQL. With SQL, we tell it what to do. The database engine figures out how to do it. With PL/SQL, we kind of give it additional steps on how we want it to perform. For instance, what happens when we get an error? How do we want to handle that?

We also get improved performance because it's a reusable unit of work, because it's already compiled and stored in the database as a database object that's going to help to improve performance. Also, we have other abilities, like having the ability to store the results in the result cache of a function, for instance, so that if somebody supplies the same parameters, and it's previously been executed with those same parameters, we might have cached the results so that we don't have to re-look up the value or recalculate the value. We can just pull up from the result cache.

And then modularized program development that we talked about already. Integration with Oracle tools-- PL/SQL is an Oracle proprietary language. It integrates really nicely with other Oracle tools. Portable-- what that means is that it runs on any operating system that has an Oracle database installed on it, and backward compatible.

So if I wrote something in version 10g of the database, and I wanted to run that in version 19c of the database, I should be able to run the same object, the same PL/SQL code, assuming that it references the correct objects in both databases. So it's portable-- runs anywhere where Oracle runs.

Also, it has the ability to include exception handling, which is where we tell Oracle how to handle it when something occurs. And then also, support for Object Oriented Programming-- if you've already got modules written in Java or C, you could actually just call those from PL/SQL, and those would then be executed by Java or C.

Now, the runtime architecture of PL/SQL-- so we've got what's considered, basically, two separate engines. We've got a PL/SQL engine, and we've got what we used to call a SQL engine, which we now call the SQL statement executor. And the PL/SQL components are handled in the procedural statement executor, which is the PL/SQL engine. The SQL statements are still handled by the SQL statement executor in that SQL engine.

Now, as far as the structure, now we're showing you the anonymous block structure, by the way, we have a declaration section, which is optional. This is where we define variables and cursors and user-defined exceptions. And we're to going to be going over all of those objects as we proceed with the course.

We have to have a begin. The begin is mandatory. That's what we call the executable section. And inside of that executable section we have to have either one or more SQL statements or one or more PL/SQL statements. We have to have something in there that is a placeholder for an executable section. So we could say begin null semicolon end semicolon, and that would run the null with the semicolon is the placeholder for the executable statement.

And then, optionally, we can add an exception section. And that's what actions we want to perform when exceptions occur. And then we have to have an end. So mandatory structures begin with some sort of an executable statement and an end, as well.

All right, let's take a look at the PL/SQL blocks. So PL/SQL blocks, as I was mentioning, fall under anonymous blocks and fall under what we call subprograms. subprograms are stored in the database as compiled objects. And they're showing us functions and procedures and triggers as a summary of what we call a subprogram. And of course, as I mentioned, we're going to be covering functions, and procedures, and triggers later on in the course. That'll be towards the end of day 2, the beginning of day 3 out of this five-day class.

OK, so here is an example of an anonymous block. Now, here they have a declaration section, starting with the word declare. We have a variable called v_fname. The data type is a VARCHAR2, and the size is 20. And then we have the BEGIN keyword, which starts our executable section.

SELECT first_name INTO v_fname FROM employees WHERE employee_id equals 100. Now, we're not really going into the rules of PL/SQL at this point in the book, anyway. But I'll go ahead and summarize. Any time you're selecting data from a table in PL/SQL, you need to store that in some sort of a storage structure. In this case, we're storing that in something that we call a scalar variable.

And we're able to store a single first name at a time into this scalar variable. That, by the way, is what scalar implies is only a single data type and a single occurrence at a time can be stored. And so that's why we have the WHERE clause where the employee_id ensures that we're only bringing back one first name.

If we happen to bring back more than one first name, we would actually get a database error. And we'll show you some examples of that coming up in later chapters. But declare the variable, and then use the variable inside the executable section.

So you're going you want to be very careful about the semicolons. Notice the placement of the semicolons. We have a semicolon after the variable name, or after the variable definition, I should say. We have a semicolon at the end of this SELECT. And then we have a semicolon after the END keyword.

Now, that little slash character, what that is is it's a PL/SQL delimiter. It basically designates that that's the end of our PL/SQL unit. And if you are doing this in command line, if you were doing this in SQL Plus, you would have to put the slash character. And then when you hit Enter, it would go ahead and execute that PL/SQL block. If you didn't put this slash character, and you hit Return, it wouldn't realize that that's the end of the block, and it wouldn't actually execute.

Also, if you have a combination of PL/SQL statements and standalone SQL statements inside of a worksheet in SQL developer, you're also going to need that PL/SQL delimiter. Now, let me show you an example of that. I happen to have an environment up and ready to go here. So let me get rid of my results.

So let me just do a couple of demos. OK, begin and end with a semicolon. This is not going to execute successfully. You notice I get an error-- encountered the symbol END when expecting one of the following.

And by the way, it does tell us the line number and the column. Line 3, column 1-- that means line 3, character position 1. So this is where we encountered the error. Notice that wherever my cursor is flashing, it does tell me where my cursor is located, line 3, column 1. So that kind of matches with the error message is telling us.

Now, you may not have line numbers enabled. So if you wanted line numbers enabled, this is probably what your environment will look like. So if you want those line numbers, you put your cursor here in the margin. You right-click it. And you just select Toggle Line Numbers. And that will put your line numbers there. And that helps the error reports to be easier to read.

Now, if you want line numbers to be permanent, you can always set that in your preferences. You can go to Tools, and you can go to Preferences. And you can go to Code Editor. And there's a Line Gutter option right down there. So Preferences, Code Editor, Line Gutter-- put a tick in the box for Show Line Numbers. And that will always put the line numbers up there every time you start SQL developer.

And again, just in case you want your fonts to be a different size-- I showed this previously, but just in case you want the font size a little bit different, you can go ahead and change that. So I showed you that in the exercises for chapter 1 but in the labs. But just in case you haven't looked at the labs yet, that's how you change your font size to be a little larger.

OK, so we noticed, as I mentioned, you have to have some sort of an executable in the middle. So if I put a null with a semicolon-- let me clear my error message-- you'll notice this runs fine. It doesn't do anything, but it runs fine.

Now let me do a combination of PL/SQL and SQL. I'll do both of those. And notice what'll happen. We'll end up getting an error message at line 5-- encountered the symbol SELECT. This is PL/SQL. This is SQL. We didn't put our little PL/SQL delimiter right there.

So SQL Developer is not understanding that we're at the end of our PL/SQL, and now we want to go a standalone SQL. So I'll put that little block terminator slash there on line 4. And now you notice that it allows us to run everything. So there we go.

Now, if I wanted to get a little fancier, let me build something like what they were doing in the instructions so you can see what the output looks like. Declare v_lname, varchar2(20) I think is what they did in the book, right? Begin, select last_name into v_lname from employees where employee_id equal 100.

And by the way, it's always a good idea to make your code beautiful. So you can right-click your worksheet and come down to the Format option. And it'll wrap and indent and take care of the capitalization of your keywords. And you notice the code looks a lot easier to read. And then I can go ahead and run it. And you notice that it executes successfully.

So as I mentioned, if I comment out that where clause and put a semicolon up here and try to run it, what I'm trying to do is I'm trying to put 107 last names into a variable that's built to take one at a time. And that's going to give me an error-- exact fetch returns more than requested number of rows.

This type of variable is only designed to take one name at a time and only one data type. And because I'm trying to put 107 last names, because that's how many names I have in my employees table, we get this error message saying, hey, we're getting back too many rows. [LAUGHS] So you want to make sure that you only return a single row at a time, or a single name at a time, rather.

Now, we do have things that we're going to show you later. If you wanted to pull back every single last name, we could do a loop, and we could loop 107 times. And for every iteration of the loop, we could get back a different name. So we'll show you how to do that a little bit later, but we'll start simple at the moment.

OK, so let me go back to my PowerPoint. There we are. Oh, they were doing first name. Sorry, I did last name. [LAUGHS] All right, so as you probably saw, I clicked on the Run Script icon to execute the anonymous block. You want to do that with your PL/SQL code, because PL/SQL includes, usually, commands.

And if you don't run it as a script, if you run it as a statement using the first button, it's only going to run wherever your cursor's flashing. And if your cursor happens to be on the line that isn't part of a block, it's not going to run anything. So it's just easier to use the Run Script button to make sure that everything runs.

Now, how do we generate output messages? For instance, how do I check what the last name is of my employee 100? Well, in order to do that, we have a package called DBMS_OUTPUT. Inside of that package we have a procedure called PUT_LINE, and the PUT_LINE procedure is designed to allow us to see the values that are stored inside of our variables.

Now, in order to be able to use this in SQL Developer, we have to use the command SET SERVEROUTPUT ON one time per session. So as long as you're in the same session, and you've already executed SET SERVEROUTPUT ON, you don't have to keep on using it. But it's good habit to go ahead and embed that inside of your scripts just to make sure that, when you run the script, it's automatically on.

All right, so let's show you what the book answer looked like. So you notice they put the SET SERVEROUTPUT ON. Now, it's a command, so technically, you don't have to put the semicolon. But we went ahead and put the semicolon there so that you can see that that's the end of that command.

And then we've added the DBMS_OUTPUT PUT_LINE clause where we put a literal string there. The first name of the employee is-- and then we concatenate that together with the variable. And as long as the variable has a value, it'll be displayed. So it looks like, in this case, the first name of the employee is Steven. Looks like they got a little extra space there in that literal, doesn't it?

So let me demonstrate that myself. Let's go ahead and-- now, I'm going to copy this to a fresh session by clicking on this little button right here. There's still a button here opens up what we call an unshared worksheet. So this actually has its own session.

And so I'm doing this just to show you that if I have dbms_output.put_line, and I put that last name of the employee is-- and concatenate that to v_lname, I just wanted to show you that, by default, it doesn't print that line out. And that's because I have not put my SET SERVEROUTPUT ON command there.

So now I'll run it as a script. It's going to run line 1 as well as lines 2 through 12. And you notice that now I get my output. The last name of the employee is King. Now if I comment out the command-- and by the way, you notice I didn't put a semicolon on the end there. It's technically not required on those commands.

But you'll notice that even if I comment out that SET SERVEROUTPUT ON, you notice it still prints out the last name of the employee is King. It's letting me see what the value is inside the variable. And that's because, as I mentioned, this only has to be executed once per session. And since I'm in the same session, it allows it to come out.

All right, now, in this class we're going to end up using the DBMS_OUTPUT PUT_LINE a lot. We're going to end up using SET SERVEROUTPUT ON a lot. So usually what I like to do is I like to put those in something that we call snippets. So I'm going to go up here to View. I'm going to go down here to where it says Snippets, and I'm going to add my own snippet, this little plus sign right there.

I'm going to put this in the category of PL/SQL programming techniques. And I'm going to call it dbms_output. And I'm going to do dbms_output.put_line with a set of parens and a semicolon. I do have a space in the middle just so that I've got a place to put my cursor when I use it. And we'll apply that.

And then I'm going to do another one for my server output under the same category. So I'll call it serveroutput. That's what I'm going to see, by the way, in my list when I go to look for it. But the actual command is SET SERVEROUTPUT ON. I'll apply that. And I'll just show you that these are down here under the category of PL/SQL programming techniques. You'll notice I've got my serveroutput and my dbms_output.

So back here on this one, I don't have a SET SERVEROUTPUT ON, so I'm going to drag it over from my snippets right there. And my dbms_output line, I'm just going to drag that to line 11. And then I'll just put my variable name there. And I'll just go ahead and run it. And you notice that I get back the employee's name.

So go ahead and create your own snippets if you think you would like to have that capability. dbms_output.put_line-- to type that over and over and over again a couple of hundred times throughout the course of the class, you might decide that you want to do that as a snippet. And by the way, what I do with the snippets is I click the little minus sign, and that auto-hides over there. And you can just put your cursor over that, and that's those snippets will pop back up whenever you need them. And that's going to be my recommendation.

OK, so that's how we view the output of the PL/SQL block. So let's take a look at the quiz. A PL/SQL block must consist of the following three sections-- a Declarative section, which begins with the keyword DECLARE and ends when the executable section starts. So think about that. Is a declarative section mandatory, or is that optional? We already know that the declarative section is optional. So we already know that this quiz question is false.

So this is what we have to have-- an Executable section, which begins with the keyword BEGIN and ends with END. So we have to have that. The Declarative section is optional. The Exception section is optional, as well. So that makes this false.

All right, my friends so that's going to do it for this lesson. We're going to have you guys go ahead and do practice 2. And what you're going to be doing in practice 2, you're going to identify PL/SQL blocks that execute successfully. And you're going to create and execute a simple PL/SQL block. OK, let's go ahead and get started with that.

## 02 Practice 2-1: Introduction to PL/SQL - New - 7m

I will now demonstrate practices for lesson 2, Introduction to PL/SQL. For the overview, we see that the Home Oracle Labs PLS labs folder is the working directory where you save the scripts that you create. The solutions for all the practices are in the Home Oracle Labs PLSFSOLN folder.

Now in Practice number 2, we see that we only have two different practices. The first one is we're going to take a look at the different PL/SQL blocks and we're going to try and determine which blocks execute successfully. So let's go ahead and maybe try each of these blocks. And that way you can see if they actually do work or not.

So I'm going to go ahead and open up a worksheet. And let's start with letter A. Begin, I guess I better-- I'll tell you what, I'll copy it out of the book just to make sure that I get the case capitalization exactly the same.

All right, let's run it. What do you think? PL/SQL procedure successfully completed. So yeah, letter A would run. Let's take a look at the letter B.

This one won't run, by the way. I know already up front. So let's go ahead and Paste that. And you notice, it does not run, as I was mentioning. OK.

And let's take a look at the letter C, declare, begin, and end. OK, so both letter B and letter C are missing the executable section of your block. And so neither B or C will run. That's not the only problem, by the way, with letter B. Letter B is also missing the begin keyword.

So yeah, we see that letter C will not run either. Let's take a look at letter D. And let me copy that.

So this one will successfully run. Although, we're not printing out anything. We are not printing anything out because we have not initialized our variable. And since we haven't initialized our variable, it doesn't print anything out. But it does run successfully.

All right, number two, create and execute a simple anonymous block that outputs Hello World. Execute and save this script as lab22solution.sql. So let me do that.

I think I'll go ahead and leave most of what we have up here. I'm just going to edit what I copied and pasted out of the book, because all I need is for this to print-- Hello World. Whoop. There we go.

Let me clear my script out, put it on the bottom. And let's go ahead and run it as a script. And you notice we get back Hello World. OK, now they do want us to save the script as lab22solution.sql.

I am going to jump down to the solutions, just so that you can see how to do that. Click the Save button. Select the folder in which you want to save the file. Enter that 22solution.sql as the file name and click Save. So I'll go ahead and do that. Save.

OK, I could put that under Labs. And I can call that lab_02_02.soln. OK, lab22solution.sql, we'll save it. And you notice that I now have that saved as a script.

OK, so just to summarize what we did in number 2, we checked these different statements. We saw that the block in B does not have the mandatory executable sections. It starts with the begin keyword. The block in C has all the necessary parts, but also no executable statement.

And so both letter B and letter C will not run correctly. However, letter A and letter D do execute successfully. And then in step number 2, we created an anonymous block in order to print out the string Hello World. And then we saved that as a file called lab22solution.sql. All right, that's going to do it for the demonstrations for practice number 2.
