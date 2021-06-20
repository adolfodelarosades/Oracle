# 11: Creating Procedures

* Creating Procedures - New - 31m
* Practice 11-1: Creating and Using a New SQL Developer Database Connection - New - 5m
* Practice 11-2: Creating, Compiling, and Calling Procedures - New - 30m

## Creating Procedures - New - 31m

Let's take a look at the next chapter, chapter 11, on creating procedures. Here we are in Unit number 4 working with subprograms, and we see that Unit 4 has several different lessons in it, from Lessons 11 through 17. And you'll notice that starting in lesson 11, we're going to be working with procedures.

And after completing this lesson, you should be able to identify the benefits of modularized and layered subprogram design. You should be able to create and call procedures. You should be able to use formal and actual parameter notation. You should be able to use positional, named, or mixed notation for passing parameters.

You should be able to identify the available parameter-passing modes, handle exceptions, and you should be able to remove a procedure and be able to display its information.

So modularizing-- I talked about this way back in Lesson number 1. Here we have Jack and Alice. Jack says, hey, Alice. I need your help in updating the database with new organizational changes. Alice says, sure. Tell me your requirements. And Jack says, I need a program which can help me change the salary of the employee, change the job ID, and promote the employee.

So modularizing code with PL/SQL. PL/SQL, as we mentioned, is a block-structured language. The PL/SQL code block helps modularize the code by using anonymous blocks, procedures and functions, packages, and database triggers. So remember that the concept of modularizing means to break up a complex task into smaller modules of work.

So the benefits of modularization are easy maintenance, improved data security, improved data integrity, improved performance. And they're reminding us that this term subprogram means a stored procedure or a function. It technically also means trigger.

So a PL/SQL subprogram is a PL/SQL block that is named. It allows us to create these modules of work in the application. A subprogram consists of a specification and a body. And we can group procedures and functions together into PL/SQL packages. And we'll talk about packages coming up.

So when you're working with procedures, we need to be able to create the procedures and then we can call them. Now, if you include parameters, we have what's known as modes for passing the parameters. We have IN mode, we have OUT mode, and we have IN OUT mode, and we're going to talk about those modes coming up shortly.

We're going to show you what formal versus actual parameters means. And then we're going to show you how to pass the parameters to your subprograms, either positionally, or named, or a combination of the two called mixed notation.

OK. So Alice says, I understand your requirements. I will come up with a solution. And Jack says, thanks, Alice. So Alice concludes that she's going to create two different procedures. One called raise_sal, which is going to allow us to raise the salary, and one for a promotion.

So procedures-- what are they? Well, a procedure is a type of a subprogram that performs an action. Procedures can return data, similar to what functions can do, but procedures always typically do some sort of an action. Of course, functions always have to return data. Procedures can be stored in the database as a schema object, and procedures promote reusability and maintainability.

So how do we create a procedure? Well, we create one or potentially edit an existing one. We compile it. We check if there are any warnings or errors. If there are warnings or errors, we view those. We correct those. We recompile those. Or if it's just a warning, make note of the warning and determine whether or not it should go back and change anything. Now, if you don't have any compiler warnings or errors, then just go ahead and execute the procedure.

OK. We use the CREATE clause to create a stand-alone procedure that is stored in the Oracle database. We use the OR REPLACE option to overwrite an existing procedure. So if it's already an existing procedure and you want to edit it, if you add the OR REPLACE clause, it will overwrite the procedure of the same name with the new code.

You can also create procedures using SQL Developer. We have something called a wizard that helps us do that. Let me show you how to do that. So I can actually right-click where it says Procedures, and I can select New Procedure, and I can go ahead and give it a Name, and I can add parameters if I want to.

So maybe I want to name this P_NAME. It's an IN mode, and I'll pass in my name. And then when I click on OK, you'll notice that it puts this into an edit window, and you can come in and replace the NULL with some sort of logic. Maybe I want to print out my name. And what I'll do is I will say Hello concatenated with P_NAME.

Let's format that. Let's compile it. And let's take a look at the Messages. You notice it's compiled with no errors. Clear my log, like I like to do. And now I have the procedure called hello_proc over here in my Procedures category. There it is right there.

I can invoke it over here from the object tree, as well. I can right-click it and I can click Run. And what I can do is I can provide my name for the parameter and I can run it. And by the way, since it's character-based, I got to put single quotes around it. And you notice that my output value, if I had an output value, would say Brent.

So or you can just run it from an anonymous block. began. helloproc('Brent'). And by the way, because I may be in a new session where I haven't printed out any values yet, haven't printed anything from my de minimis output, I may want to do my server output on command there, SET SERVEROUTPUT ON. And let's go ahead and run it. And you notice that it says, Hello Brent.

So use the wizard to create your procedures or create them yourself on the worksheet, but they're showing you using the wizard there.

OK. To compile a procedure, you can click the little gears. If you've used the wizard and it opened it up into an edit window, you can click the little gear button to compile. Again, if there are compiler errors, you do need to check those and correct those before you can run them. If you have a compilation error, those will also have a red error notation on that, as well, in the object tree.

So you can call procedures from anonymous blocks, from another named PL/SQL block. You can also use those from the command prompt using the EXECUTE keyword. If you use the EXECUTE keyword, it does not like you to wrap it around to the next line. So make sure that if you use the EXECUTE keyword that you always use EXECUTE along with the name all on one line.

Over here, they're invoking the hello procedure from an anonymous block. Here, they're creating another procedure that invokes the helloproc in another procedure. Or you can do that from the EXECUTE command prompt. And as I was showing you, you could also right-click it in the object tree and you can select Run, and you can provide a parameter value and click OK, and it'll go in and put it in the output log.

So Alice says, I have created this procedure where you can increment the salary of all the employees by 10%, and you can change that percentage to some other value, as well. But Jack says, hey, there's a problem here, Alice. It looks like it's going to update every employee from what I can see. UPDATE EMPLOYEES SET salary = salary * (1+1/10), which is 10%.

And so it looks like Jack is probably not going to like always giving everybody a specific raise of 10%. We need some flexibility built into it. So what we're going to have to add is we're going to have to add some parameters so that we can decide which employees get a raise, how much it's going to be. So that's why we're going into the parameter discussion at this point.

Parameters allow us to have a means of communication between the calling environment and the procedure. Each parameter is associated with the mode. We have three modes. IN mode parameter, which is the default. If you don't put a designation, it'll be an IN mode parameter by default. So this allows us to provide values into the subprogram to process. OUT parameters allow us to return a value to the caller. Or you can have an IN OUT parameter, which supplies an input value, which may be returned as a modified value.

And then we want to define these terms formal versus actual parameters. So I like to say that the formal parameter is the definition of the parameter when you define the subprogram. The book says formal parameters are placeholders for data in a specific specification. Actual parameters are the values that you supply to satisfy the parameter. So those can be literal values. Those can be variables. Those can be expressions. And those are substituted into the parameter list when you invoke the subprogram.

So here, we're talking more about the parameter modes. Again, we have IN, OUT, and IN OUT mode. The IN mode, again, is the default if no mode is specified. And the parameter modes are specified in the declaration of the formal parameter after you define the parameter name, but before the datatype.

So let's compare the different modes. IN mode is the default-- allows us to pass a value into the subprogram. The formal parameter acts as a constant. The actual parameter can be literal, an expression, a constant, or a variable that's been initialized. You can assign a default value for IN mode parameters.

OUT mode parameters have to be specified. The value is returned to the calling environment. It is an uninitialized variable. We have to use a variable and these cannot be assigned a default value.

Now, IN OUT mode has to be specified. The value is passed into the subprogram. The value is returned to the calling environment. It is initialized. It must be a variable. And it cannot be assigned a default value.

So let's take a look at an example. Here, we have a procedure called query_emp. The parameter p_id is an IN mode parameter based on the employee_id%TYPE. We have a couple of variables. We have a variable for the name and a variable for the salary. So the input parameter is going to allow us to provide the employee_id in the WHERE clause.

And then we're going to print out the name of the individual, as well as the salary, that are stored in the variables. So when we execute the procedure using employee_id 176, you'll notice that we get the salary, which is 8,600, and the name, which is Taylor.

And now we have modified our query and procedure. This time, instead of having the two variables retrieve the output, we're actually allowing two OUT mode parameters to capture the values coming out. So rather than selecting the last name and the salary into scalar variables, we're actually selecting the last name and salary into the OUT mode parameters.

And then we create a procedure that allows us to create, or rather return, the employee name and the salary. So you notice that we're calling the query_emp procedure from above, passing in employee 171, and getting back out the name and salary for employee 171. And you notice that when we run it, it tells us that Smith earns 7,400. So one parameter in, two parameters out to provide the name and salary.

And then we have one called IN OUT mode. I think I'm going to demonstrate this one. And what I'll do-- I'm going to go ahead and open up my code examples, so let me just go in and do that. And we have the format_phone procedure here on line 107. Let me just copy that into a new worksheet.

So we have one parameter. It's an IN OUT mode parameter. What we're going to do is we have to initialize that. And so we're going to initialize that here on line 17. This is where we're going to assign the value.

And then we're going to pass that into the format_phone procedure, and what it's going to do is it's going to change our input phone number and it's going to put parentheses around the area code, and then it's going to put the exchange with a hyphen.

So let's show you what it looks like up front. This is what our phone number looks like going in. And then when we run lines 15 and 16, we're passing that value in and it passes the modified value back out through the same parameter. So there's the in value. Here's the out value. And it's using the same parameter to both pass the value in and get the value back out.

Now, when we use IN OUT mode parameters, we do have to initialize our variable because it has to have a value when we go in and call the subprogram that uses the value.

So as I go back to the book, let me go back to the OUT and IN OUT mode parameters. So you notice how with the IN OUT mode, we use an initialized variable and it has to be a variable. With an OUT mode, we have to use a variable that's not initialized because it's going to capture a value coming back out through the subprogram. So that's where the modes come into play. So that's an IN OUT mode parameter.

When you call a subprogram, you can either put the parameter values in the specific order that the parameters are listed-- that's called positional notation. You provide the actual parameter in the same order as the definition of the formal parameters. If you do named notation, that's going to allow us to execute them in any order and we use the association operator in order to do that.

And then we have mixed mode. We can start with positional and then switch to named notation. That's what we call mixed notation. Once you start with named notation, you're not allowed to go back to positional.

So let's show you some examples. Here we have the procedure called raise_sal, where we're passing in an ID and a %. And here, we're doing the positional notation. The first value is going to go to the first parameter. The second value is going to go to the second parameter.

Down below, in the second example, we're using named notation. We're using the names of the parameters and using the association operator to associate them with the value. And Jack's happy about this one. He says, thanks, Alice. This is going to help. Please find a solution also to help me update the promotion data in the database, as well.

We talked a little bit about defaults. So if you have an IN mode parameter, you can put a default. And in that case, you don't have to supply the value at runtime.

So here we have an IN mode parameter for the percent of the raise. It's a default of 10. And when we go to call the procedure, when we supply 176, it's going to go into the first parameter. So that's going to be 176. And since we start with the first parameter, whatever first value we supply is automatically going to go to the first parameter. And then the second parameter would default to 10.

Or you could provide the values positionally, like in the second example. 176 is going to go in for the ID. 10 is going to go in for the percent. Or you could go with just named notation, where we're putting the name of that parameter-- p_id, in this case-- and initializing the value. And then it's going to accept the default for the other parameters. In this case, we're going to default to 10%.

Handling exceptions. How to drop a procedure. Displaying the procedure's information. So we should add exception handlers to our subprograms. The reason why-- here, we're showing you an example where we have an exception handler that says, hey, when we have some unexpected error that occurs, let's raise an error that says, Err adding dept, and then the name of the department name passing in through the parameter.

As long as we have an exception handler, the valid insertions will occur. Any that are invalid will not occur. If we don't put an exception in there, if one fails, they all fail. So even though two of these are valid inserts, because one fails, they will fail. So it is recommended that you should always include exceptions.

How to get rid of a procedure. You can right-click it. You can select Drop. Or you can issue the DROP PROCEDURE command. DROP PROCEDURE name of the procedure will drop the procedure. Right-clicking the procedure, selecting Drop, and then clicking Apply will also drop the procedure.

How do I look at the source code? What if I don't have SQL Developer available? What if I'm using the command line? How am I able to look at my source code? Well, we have a data dictionary view called user_source, and we can query the user_source dictionary view. As long as you filter it on the name and type of the subprogram, and as long as you order by the line, you're going to see the syntax in the correct order.

Bear in mind, if this happened to be a package or some other component that has been what we call wrapped or obfuscated, sometimes you may not be able to read the code because we don't want you to read it or somebody doesn't want you to read it. So just keep that in mind.

If you try to look in user_source and you get back a bunch of alphanumeric elements that you can't read, look for the word wrapped. Most likely, your code has been wrapped, and you don't have the permissions to see the code. Otherwise, when you go into user_source, you should see the source code, just like we're seeing over here on the right.

And we can also click on the object in SQL Developer. It will open it up, and we can then view, as well as edit, the information in SQL Developer.

So that brings us to our quiz. Which of the following is an invalid procedure call for a procedure? We have the procedure called ADD. Parameter a has a default of 10. Parameter b has a default of 20. And parameter result is an OUT mode parameter of a number type. We don't have a default for the OUT mode.

So I would say for this one, letter c is the one that would work-- ADD(10,20,ex). We're positionally matched. Letter d wouldn't work because once you start named notation when you're doing mixed notation, you can't go back to positional. So letter c definitely won't run. Letter b-- ex is going to want to go in the first parameter, and we don't have a default for the next two, so that one's going to error out, as well. So letter c-- that would be the one that would work.

OK. So you should have learned about the benefits of modularization and layered subprogram designs. You should have learned how to create and cult procedures, use formal and actual parameters, use positional, named, and mixed notation for passing parameters, identify the available parameter-passing modes, handle exceptions, and you should be able to remove a procedure and display its information.

So we actually have two practices in this one-- Practice 11-1, where we'll be creating a new database connection after you delete an old database connection, and then the second practice, where you're going to create stored procedures to insert, update, delete, and query table data. You're going to also learn how to handle exceptions and procedures and then how to compile and invoke procedures.

## Practice 11-1: Creating and Using a New SQL Developer Database Connection - New - 5m

I will now demonstrate practices for Lesson 11, Creating Procedures.

We actually have two practices for this chapter. In the first practice, which is 11-1, we will be deleting the My Connection connection in SQL Developer, and we will be recreating that connection and setting some preferences in your SQL Developer preferences.

And then in 11-2, we will be going in and creating procedures, introducing you to parameters, and showing you how to include exception handlers inside your procedures.

So I will start out with the practice 11-1, where we're going to create and use a new SQL Developer database connection. You notice that we have six different steps in this particular lab, so let me start with the solution.

What we're going to do is, we are going to right-click the connection called My Connection, this one right here. And we're going to be deleting this one. And go ahead and say yes to the Delete Confirmation message.

Next, we're going to create a new database connection, using the information that you see in the Activity Guide. I will go ahead and click the plus sign. And I will call this My Connection. Notice the case convention that we're using for that connection.

The user name is going to be ora61. The password is going to be cloud_4U in my case. You should double-check your password credentials in your course practice environment security credentials document, which should be in the Activity Guide on about page 5 or 6.

Next, I'm going to go down to the service name, and I'm going to put the service name of orlcpdb1. And I'm also going to be careful to tick the Save Password button. Next, what I will do is click Test and just double-check that I have a success message.

So just to follow along in the book, I wanted to show you that this is the same parameters that you see in the book, and I do have a success message. And what I'm going to do is, I'm going to go ahead and save it, and then I will click Connect. And now I have a new session for that connection.

So I have a couple of-- actually, I have only one preference that I'm going to set next. What I'm going to do is, I'm going to set the path to look for scripts to the home/oracle/labs/plpu directory, as noted in step number 4. So let me go ahead and do that.

I'm going to go to Tools. I will go to Preferences. I'm going to go down to the Database category, and I'm going to go down to where it says Worksheet. And what I'll do is, I will set the path.

Now, it doesn't let you really set the path by typing there. You might find it easier to click on Browse and actually browse to the plpu directory, and then click Select. That will set the path to the plpu directory, and this is where we're going to use the scripts for the rest of the class.

Next, what I'll do is click OK, and my connection is now complete. If you'd like, you can go ahead and expand the plus sign next to my connection, and you'll notice that you have the default set of tables that make up our Human Resources schema.

OK, so that is going to do it for the demonstrations for practice 11-1.

## Practice 11-2: Creating, Compiling, and Calling Procedures - New - 30m

I will now demonstrate the practices for Lesson 11-2. In the overview, we see that we will create and compile and invoke procedures that issue DML and query commands. You'll also learn how to handle exceptions and procedures. Notice that before starting this practice, we ask that you execute the cleanup 11.sql script. And if you miss a step in a practice, please run the appropriate solution script for that practice step before proceeding to the next step or to the next practice.

These labs are usually dependent on each other starting at this point, so you will want to make sure that either you finish up the labs for each chapter, or that you run the solutions script if you did not end up completing the chapter. So let me show you how to run the cleanup script. I'm going to go ahead and open, and I'm going to go to the PLPU directory, and to the Code Examples, and do the cleanup.

And I'm going to run cleanup 11. So I'll go ahead and open that. And you notice what this does, it drops a number of different procedures. I am going to choose MyConnection in SQL Developer, and then I'll run this as a script. And that just ensures that your environment is set up in order to do your practices coming up in this chapter. OK. I'll go ahead and close that cleanup script.

Now I'm going to go ahead and start with the solutions. So let me get down to the solution section. And it looks like that is going to be about page 13 for me. So in this practice, you're going to create and invoke the add_job procedure and review the results.

You also create and invoke a procedure called update_job, in order to modify a job in the Jobs table. And create and invoke a procedure called delete_job to delete a job from the Jobs table. Finally, you create a procedure called get_employee to query the Employees table, retrieving this salary, and job ID for an employee when provided with the employee ID.

Now before we do this, we do have a trigger that may be enabled that might prevent you from going in and making any modifications to any of the tables in the schema. So I'm going to show you how to disable that trigger. You're going to go down to our assessed triggers, under your MyConnection connection, and expand it.

And you notice that we happen to have a trigger called secure employees. And because of the orange and green colorization of that, I can tell that that is enabled. So what I'm going to do, I'm going to right-click it, and I'm going to disable the trigger. And I'm going to Apply. And that'll ensure that we don't get any errors, if you happen to be doing labs outside of regular business hours or on the weekend. OK.

So we can continue on now with step number one. We are going to create, compile, and invoke the add_job procedure, and review the results. We are going to create a procedure called add_job, which is going to insert a new job into the Jobs table. We're going to provide the ID and job title using two parameters. And notice the notification in our labs.

You can create the procedure and other objects by entering the code in the SQL worksheet area. And then click the Run Script button, or press F5. This creates and compiles the procedure. If the procedure generates an error when you create it, click the procedure name in the procedure node, edit the procedure, and then select Compile from the pop up menu.

Now notice that you can also open the solution 02.sq. file in the home/oracle/labs/plpu solutions directory. And you would uncomment and select the code for task 1a. Let me show you where that's located. So I'm going to click on the Open, and I'm going to go to plpu, and I'm going to go to soln. And you notice that we have a solution 02. And I'll go ahead and open that.

And this would be the add_job procedure that they're talking about. OK. So what I'll do I will go ahead and copy that. And I will paste that in my worksheet. And then I'll go ahead and compile it. And then I'm going to expand my procedures category. And you notice that I have the add_job procedure. So for demonstration purposes, that will be the way that I create my procedure for this first step.

Now let's take a look at what we're doing here. We're creating a procedure called add_job, and the parentheses designate a set of parameters. We have a parameter called p_jobid, which we're going to use as an insert value into the Jobs table. And we have a parameter called p_jobtitle, which is going to be used as an input parameter value for your Jobs table, as well.

You'll notice that the p_jobid is of the jobs.job_id%type, and the job the p_jobtitle parameters is of the jobs.job_title%type. And so, this-- when we run this, it's going to insert a job into the Jobs table. And you'll notice that we have a commit, and so that's going to make that insert permanent.

Now, coming up on the next page, we are going to have you locate that, over in the object tree, over on the left. And we're going to have you go ahead and click on that procedure, so that you can see that it opens up into a window where you could compile it, again, if you desired. And just in case you had any mistakes, if you got any errors, or anything like that when you tried to recompile it, you could just click on it in the object tree.

You can make your changes, make your edits. And then you could click the Compile button, again, and, down below, it would tell you the status of what happened as far as the compilation. So it looks like in this last log message that it was compiled successfully.

Now if you want to clear out the log, go ahead and right-click the log and click Clear. And that's how you can clear out that log, so that you don't see old messages, because the messages tend to append at the end of each execution. OK. So I'm going to go ahead and close that window. I am going to clear my worksheet.

And now in step letter B, we're asked to invoke the procedure with the IT_DBA string as the job_id, and Database Administrator as the job_title. Let me go ahead and do that. So I'm going to execute add_job. The first parameter is going to be IT_DBA. And the second parameter is going to be a Database Administrator. OK.

And then I will run that. By the way I'm going to go ahead and kind of wrap that around. And let me get rid of my log here. Now, in this case, you'll notice that it errors out. It says unknown command. OK. And the reason why is because I've split that up onto two different lines. So just be careful when you do that. OK.

I wanted to show you that error, whenever you have the execute keyword, you do need to have everything kind of down on the same line. So let me erase my script output. Execute, by the way, is a shortcut for doing a begin and an end as an anonymous block. So now when I execute it, it tells me the PL/SQL procedure successfully completed.

And then next, what they ask us to do is to go ahead and look at the row by selecting *from_jobs where job_id = IT_DBA. And I'll go ahead and run that as a statement, using in the first button. And you notice that we did insert that row into the table. OK.

And now in step letter C, they ask us to invoke the procedure, again. This time pass a job_ID of ST_MAN, and a job_title of Stock Manager. And they ask us what happens and why? So let me go ahead and do that. ST_MAN and Stock Manager. And let me go ahead and execute that.

And you'll notice that we end up getting an error. And it says, unique constraint JOB_ID_PK violated. So it looks like we already have a job_id of Stock Manager or ST_MAN. OK. So, this one here, we already have that value in the table. OK. So next, they're asking us to go ahead and create a job, or an update_job procedure to modify a job in the Jobs table. We're going to create the procedure called update_job to update the job_title.

We're asked to provide the job_id, and a new title by using two parameters. And this time we're going to include the necessary exception handling, if no update occurs. So I'm going to do that in a new SQL worksheet window. And what I will do is show you the next page. And we're going to create that procedure called update_job.

Going to replace procedure, upd_job. We're going to have p_jobid. This one's going to be IN mode parameter. And then we'll have a second parameter called p_jobtitle. And that one is going to be a jobs.job_title%type And that one is also going to be IN mode parameter. OK.

And next, we'll start our executable section. We will update the jobs title, or the Jobs table, rather. Set the job_title. I can't spell title very well. Set job_title = to p_jobtitle, where the job_id = the p_jobid. OK. And our exception handler, if sql%notfound then raise_application_error to a -20202, and we'll say, no job updated. with an end if, and with an end. OK.

Let me format that. And let's just double check that I've got my semicolons in the right spot. And as I mentioned, you know, previously, I like to usually do the show errors command, in order to see if I get any compilation errors. Now I do get an error message. Component job_id must be declared. So, let's go in and see where I went wrong. Line 2 is where it's pointing me. Line 2, character position 18, so what I did is I misspelled the name jobs, needs to be plural.

There we go. It's jobs.job_id%type. This one here is going to also be jobs.job_id%type, or jobs.job_title%type. Did you notice over here, name of the table is plural? OK. Let's try that again. Clear out my show errors message. And this time we compiled it, and we don't have any errors. OK.

So, let's go ahead and erase it. And next, we'll go down to letter B, where we're going to invoke the procedure to change the job_title of the job_id, IT_DBA to Data Administrator. And then we're going to query the Jobs table and view the results. So let's go ahead and do that. Execute your upd_job IT_DBA, and we'll do that as Data Administrator.

Go ahead and run that. Successfully completed. And now let's do a separate select. And there we go. So you'll notice that we have updated that to Data Administrator. All right.

Moving forward with the next page, what we're going to do is test the exception handling section of the procedure by trying to update a job that does not exist. So let's go ahead and do IT_WEB. And let's do Web Master. And we'll go ahead and execute that.

And you notice that we get our error message back, because we don't actually have that job_id. And if you want to just ensure that you don't have that job_id, we can go ahead and try IT_WEB, and we should get back an empty result set, because we don't happen to have that job_id in existence. OK.

On to step number three, we are asked to create a procedure called delete_job to delete a job from the Jobs table. So I'll go back to my original SQL worksheet, and we're going to include the necessary exception handling, if no job is deleted. So I am going to create or replace procedure delete_job. OK.

We'll do a couple of parameters, p_jobid, and that one's going to be the jobs.job_id%type. I said jobs, but I typed a job again. I don't know why I keep forgetting that s there. So it should be jobs.job_id%type. And we'll just do the one parameter.

And then we'll start our executable section. And we will say, delete from jobs where job_id = p_jobid. And then our exception handler, if sql% not found, then raise_application_error, and we use a -20,203 for our error code, and the error message, no jobs deleted. End if, and end, and show errors.

I'll clear out my output. And I'll run it. And I like to right-click and format my PL/SQL code, as well, before I run it. OK. And it looks like we compiled successfully, no errors. And let's go ahead and test it. Execute del_job IT_DBA. And let's run it.

You notice this successfully completed. And let's just double check and make sure that it's out of the table. I think I've still got that SELECT statement over here, by the way. Select * from jobs where job_id = IT_DBA. OK. Doesn't show up, because we deleted it.

And coming up on the next page, we're going to test the exception handling section by trying to delete a job that does not exist. So I will, too-- we'll do IT_WEB. And we get back the error message, no jobs deleted, because that job does not exist. OK.

Continuing on to step number 4, we're going to create a procedure called get_employee to query the Employees table. We're going to retrieve the salary and job_id for an employee, when provided with the employee ID. First step, we'll create a procedure that returns a value from this salary and job_id columns for a specified employee ID, remove syntax errors, if any, and then recompile the code. OK.

So let's go ahead and do that. We're going to create a procedure called get_employee. And we're going to pass in three parameters. We have one IN mode parameter and two OUT mode parameters. p_empid is going to be IN mode, employees.employee_id%type. We'll have one called p_sal, which is going to be an OUT mode parameter. Employees.salary%type.

And the third parameter is going to be the job, p_job. It's also going to be an OUT mode parameter. And it's going to be the employees.job_id%type. And let's go ahead and run our select. Select salary and job_id. And you'll notice that we're using the OUT mode parameters to capture the data coming out of the salary and job_id.

So we're going to do a salary and a p_sal, job_id and p_job, from the Employees table where the employee_id = the p_empid. All right. Format it, make it look prettier. And we will do the show errors. And let's go ahead and compile it. It looks like it successfully completed.

Next, what we'll do is we'll use the bind variables in order to print out the values coming from the OUT mode parameters. So I will create a variable called v_sal, v_salary rather. And another variable called v_job. And all this-- I'll do this as a varchar2(15).

Then let's go ahead and execute the get_employee procedure. And we'll pass IN 120 for the job_id. And we'll pass IN our bind variables. OK. And then I'm going to print v_salary, and v_job. And let's see what that looks like. OK. So, we have my v_salary, number, variable v_job.

Well, I tell you what, let me go ahead and do that. Variable v_salary-- just to be consistent on the case, let me capitalize that. It doesn't have to be capitalized, but case salary, or variable v_salary is a number, variable v_job is a varchar2(15). We're going to execute get_employee.

And just to show you that procedure over here, there it is. We're passing IN 120, and that's going to go into the p_empid. And then we're going to capture the output from the parameter, p_sal and p_job. And let's go ahead and print out the v_salary and v_job.

You know what-- I just saw I have a comma there, so. I think it's not going to like that comma. So what I'm going to do, I'm just going to highlight just the first three lines, make sure that executes successfully. And then what I'm going to do is just run the print. And you'll notice that my v_salary is $8,000, and my v_job is ST_MAN.

So, be careful about putting a comma there as I did. By the way, you don't have to put your parameter names there, if you don't want. You can just put the word print. And it'll print any bind variables that you currently have in your session. And so that's kind of a little shortcut, if you'd rather, OK.

On to page 21, this time we're asked to invoke the procedure, again, using an employee_id of 300. So let me go ahead and do that, and see what happens. All right. No data found. So, it tells us there is no employee in the Employees table with an employee_id of 300. The select statement retrieved no data from the database, returning a fatal PL/SQL error, no data found, as described. OK.

So, we probably should have put a no data found exception handler in there, but they didn't have us do that. So, we'll probably go in and make some changes here coming up shortly. All right. Well that is going to do it for the demonstrations for Practice 11-2.
