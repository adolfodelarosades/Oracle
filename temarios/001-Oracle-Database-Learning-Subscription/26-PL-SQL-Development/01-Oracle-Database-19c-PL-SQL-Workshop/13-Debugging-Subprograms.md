# 13: Debugging Subprograms

* Debugging Subprograms - New - 22m
* Practice 13-1: Introduction to the SQL Developer Debugger - New - 21m

## Debugging Subprograms - New - 22m

OK, my friends, let's take a look at lesson 13 on debugging subprograms. We are here, unit number 4, working with subprograms, lesson 13, debugging subprograms.

OK, so the objectives-- after completing this lesson, you should be able to describe the functionality of the SQL Developer debugger. You should be able to debug subprograms, and use various features of SQL Developer debugger for debugging.

So some things before debugging PL/SQL subprograms-- now before you start debugging your PL/SQL subprograms, you need to have the following privileges. You need to have the DEBUG CONNECT SESSION privilege. You need to have the DEBUG ANY PROCEDURE privilege. You need to have the EXECUTE privilege on DBMS_DEBUG_JDWP. And you need the EXECUTE privilege on the object that you want to debug.

So you can look at the privileges of the current user by executing the following statement. ORA61 does not have the DEBUG CONNECT SESSION and DEBUG ANY PROCEDURE privileges. And so we would need to grant them by executing the following statements as SYSDBA role user.

So I am going to go ahead and demonstrate that for you. So I am going to select star from user_sys_privs. And you'll notice that I have CREATE TABLE and UNLIMITED TABLESPACE privileges.

I am going to Connect as sys DBA and run these. In fact, what I'm going to do is, I'm just going to copy those. And I'm going to do that as the PDB1 sys administrator.

That's the administrator for the pluggable database. And I'll go ahead and run that. And you'll notice that the grant succeeded. So now if I go back and select star from user_sys_privs, you'll notice that I now have the debug privileges that I need, OK?

Now I do have a procedure that I'm going to compile that invokes a function that I have not created yet. And so the function is called get_location. So I'm actually going to go and compile the function first.

Now in your labs they have you compile these out of order as part of a troubleshooting step. But since I know that's going to happen, I'm going to go ahead and create the function first, and then create the procedure.

And if I go in and expand my procedures and refresh, I see that I have my EMP_LIST procedure. Now the idea with this procedure is I want to take a look and see how the data is flowing, for instance, into my record here on line 17. So I might just click on the number 17, and that puts what we call a breakpoint in there. And that is an area that you want to investigate as you're starting to debug your code.

Now what I also want to do is, I might want to take a look at when my row from my cursor goes into my record, and down here and down here, where I am assigning values, just to make sure that the correct information is going into my different variables and records.

And go ahead and put a breakpoint on anything that you want to investigate during the flow. And what I'm going to do now is I'm going to come up here and I'm going to compile for debug.

Now once it's compiled for debug-- and I'm going to double check my messages here. It looks like it's compiled fine. No errors.

Next I'm going to hit the little Debug icon. And I'm going to be able to designate how many rows I want to run.

Now for the purpose of demonstration I'll just put two here. So I'm only going to loop twice. But you'll notice I have an error message, and it says network access denied by access control list. So let me go back to the book and show you, on the next page here, that you may get this error while running the SQL debugger or the PL/SQL debugger in 19c.

What is this? So what it does is it implies that the current database session is trying to establish a connection with the debugger on the local host, but is not able to do so. So we need to grant the permissions to the user so that you can go in and run the debugger.

And so your user that has SYSDBA role would need to execute this. So let me go back to my demonstration environment, and I'm going to go and copy this chunk of code here. And I am going to copy that into the pluggable database administrator screen as well, and run that.

OK, so let me go ahead and do that. It does say that we're granting it to ora61. So it successfully completed.

So now I should be able to come back and run my debugger. So let me go in and hit my debug. I'm going to go at two again, and I'll click OK. And this time I get a debugger toolbar. And it pops up here at the top, and it pops up down here at the bottom as well.

Now we have the ability to kind of follow what's happening with our variables a number of different ways. And so the Developer toolbar, not only is it showing-- or not the developer toolbar, but the debugger toolbar, is showing at the top and also at the bottom. You can use either one. They both do the same thing.

And if you hover over the buttons it tells you what they're all about. This one terminates the debugger. This button right here finds the execution point. So that's where it's pointing now. We're right there at my first breakpoint.

And this one here steps over a chunk of code. This one here steps into a chunk of code. So what's the difference?

So this one here, what if I put a call to another subprogram inside of my procedure? Well, maybe I want to step over the call to that program and only explore what happens after that. So it allows me to step over what's happening next.

This one here steps into. This one says, hey, maybe I want to step into the next line of code, the next breakpoint. This one here allows you to step out. And this one here lets you step to the end of a method.

This one here resumes. This one pauses. This one here suspends all breakpoints.

So what I'm going to do, I'm going to hit this button right here. And this, by the way, as you notice, is a shortcut of F7. So if you wanted to use your F7 key on your keyboard, go ahead and do that. I'm just going to go ahead and click it.

And you notice that my little pointer, this one right here, you notice that it jumps down to the next breakpoint. And I'm not actually seeing my values any place, OK? So what I need to do in order to track the values that are happening on those, sometimes you have to come up here and hit View, and then you have to come down to Debugger.

And you notice that you have four different categories. You've got Data. You've got Log. You've got Smart Data. You've got Watches.

Let me go to my Data. And let me also view my Smart Data. And what's going to happen on some of these is I'm going to-- and by the way, I'm going to get rid of my Messages log here. I'm going to get rid of my breakpoints here. You can set your preferences there by hitting this little element right here, by the way.

So here's your breakpoints, the default actions on your breakpoints, the data. Data windows settings are debugger specific and can only be adjusted after the window has been shown by the debugger.

We got the Inspector. We've got Smart Data. Same message on those windows. Watches, all of those things are different elements that we can go in and set. And we'll define what each of those does here in just a moment.

So what I'm going to do is, I'm going to go to out to the book, and we're going to describe all of those elements of the debugger, just to make sure that it makes sense to you, OK?

So the flow, again, add the breakpoints, Compile for Debug, Debug. Hitting the button. Some of the parameters you may need to supply a value for. For instance, you know, what is the value of P_ID. This case, how many times do we want to loop? 100 times in this case.

And then what's going to happen when we click OK on that, it's going to show our developer toolbar. And assuming you didn't get the error it's going to show the developer toolbar.

So using the Debugger Log tab toolbar. There you go. There is the definition of each one of those elements that I highlighted.

Number one terminates. That halts and exits the execution. Number two finds the execution point, which means it goes to the next execution point. Step Over bypasses the execution of statements of a subprogram invoked from the current subprogram and executes the statement after the subprogram call.

Step Into executes a single program statement at a time. If the execution point is located on a call to a subprogram, it Steps Into the first statement in that subprogram.

Step Out leaves the current subprogram and goes to the next statement with a breakpoint. Number six, Step to End of Method goes to the last statement of the current subprogram.

Number seven is Resume, which continues the execution. Number eight is Pause, which halts the execution but does not exit. And then number nine, Suspends All Breakpoints, turns off all the breakpoints in the current PL/SQL block.

Now there you see that I've got some of those different other tabs-- Smart Data, Data, and Watches. And that's what we're talking about on this next page.

The Breakpoints displays breakpoints, both system defined and user defined. Smart Data, what is that? It displays information about variables. You can specify these preferences by right clicking in the Smart Data window, and selecting Preferences.

Number three is the Data tab. That's where you can see the data and all the variables. And number four is Watches. This is where you can monitor all the watches set while debugging.

So what if you had 100 different variables? What if you wanted to keep track of maybe 10 of those? So what you can do is, you can set up a Watch for those 10 different variables. And you can focus on just those variables through your custom Watches.

All right, so there is the emp_list procedure that you saw me compile, and also where it's calling to get_location function. So I compiled the get_location function first. I set my breakpoints. I compiled for Debug. I went in and set the value for how many rows I want after I had the Debug button. And then click OK.

And then I click F7, which steps into the code. Now the program controls stops at that first breakpoint. And then if I wanted to advance, then I hit F7 and it'll advance to the next breakpoint.

So in order to view the data you'll notice that where I'm currently executing at the OPEN cur_emp cursor, you notice on the Data tab it shows that my record currently does not have any data in it. Because the record is the next step where I pop the row from the cursor into the record.

When I click F7, that's going to advance to the next breakpoint, at which point it's already populated my record with the value from the cursor. And I'm down here on line 18 with my WHILE loop. And so you'll notice that my record here in the Data tab is starting to get populated with the data.

Now you can modify the variables while debugging the code. You can right click one of the elements. In this case, it's going to be the i that we're going to modify.

Right click it. Select Modify Value. Go in and change it. Click OK.

And you notice that we've changed that to 3 rather than 1. So in the event that you want to-- maybe you had looped. You had designated that you wanted to loop 100 times, and maybe you want to change that to, you know, 98, implying that you've already done the first 97 records. So that's what you can do with editing those.

Case Step Over versus Step Into-- Step Into is going to go into our code, and that's going to be where we're calling our get_location function. Step Over, on the other hand, steps to the next line after this subprogram call.

And so here's our get_location call. Step Over steps over that get_location call and advances our pointer to the dbas_output.put_line. Step Into would go into the execution of the get_location function.

And then Step Out of the code. It's going to step out of the get_location function and advance to line 23, which is the dbms_output.put_line where we're printing out the last name of the employee.

Step to End of Method, you'll notice that this takes us clear to the End keyword for our anonymous block. Notice it loops until i is not equal to PMAXROWS. And it's going to step to the end.

All right, we can debug a subprogram remotely. In order to do that, we have to switch to Write mode using the Edit pencil. We add the breakpoints. We compile for Debug. We select Remote Debug.

We enter the local machine IP address and Debug Import. We issue the Debugger Connection command and call procedure in another session such as SQL Plus. When the breakpoint is reached, control passes to SQL Developer, and then we debug and monitor data using in the Debug tools.

All right, so back to my example here. So I've got my breakpoints. I've got my, you know, different categories of breakpoints that I may want.

And by the way, sometimes you are going to want to kind of play around with the size of your window in order to see all of the elements that you're trying to do. So here's my procedure. Let's go ahead and run it to the next line.

And again, I'm going to go up here and just remind you that the View Debugger, we can look at our data-- our Smart Data, our Watches, our Log. So there's our Message log. And we can also control that from down here as well. And it's telling us in our Messages log where our breakpoint is currently executing.

All right, so you're going to get some hands on with this particular debugger in your practices. So let me go back to the summary of what you're going to do in practice 13 overview.

You're going to create a procedure and a function similar to what I did. You're going to insert breakpoints in the procedure. You're going to compile the procedure and function for Debug mode. You're going to debug the procedure and step into the code. And you're going to display and modify the subprogram's variables.

All right, so that's going to do it for the lecture for lesson 13.

## Practice 13-1: Introduction to the SQL Developer Debugger - New - 21m

I will now demonstrate practices for Lesson 13 on debugging subprograms. I will start with the solution. And on the introduction to SQL Developer Debugger, we experiment with the basic functionality of the SQL Developer Debugger. Now we are asked to go ahead and enable server output. So I am going to go and run my setserveroutput on command from the snippets here. And let me go ahead and run that.

And then in step number two, it says to run the solution under Task 2 of sol_04.sql to create the emp_list procedure. And then it looks like we're going to get a compiler error. And so let me go ahead, and open up that solution script. And it's going to be a sol_04. And we're going to write Task 2. And let's see where Task 2 is. OK.

It looks like it starts on line 23. And it's going to run all the way to line 75. And what I'm going to do is I'm going to go ahead and just copy and paste that into my worksheet here. And let me get rid of these multi-line comments. All right. So I'm going to go ahead and run all of that. And it looks like we're running all of that code.

And we end up getting the error message-- identifier get location must be declared. OK. And then you notice the next step, we created a function called get_location. So, our answer to the question, you know, why do we get the error? OK. You may expect an error message in the output if they get_location function does not exist. If the function exists, you get the above output. OK.

So, now that we've created it, if we rerun lines 3 through 32, and clear out the error messages, then it gets successfully compiled. OK. And so, that is what they're telling us here in line 3, run the solution under Task 3 of sol_04.sql to create the get-location function. Well, I included it all on one script. And uncomment and select the code to create the function. And then, recompile the emp_list procedure as I did. OK.

So if you did everything correct over here in the procedures, you should see an emp_list procedure that is compiled with no errors. And you should see a function call get_location. And let me just refresh my functions. And there's my get_location function. OK. So make sure that you have both of those before you continue. All right.

Now, also, I want to point out that in this solution, there is some information that you may end up having to run. You may have to run from lines 9 through 15, in order to have the privileges to be able to run the debugger. OK. So I'm going to copy that. And I'm going to paste that in the PDB1-sys connection. OK.

Your pluggable database administrator is the one that needs to grant the permission to ora61, in order to be able to debug. Now your book actually has those instructions up in the very beginning, page 2 of Lesson 13 Practices, it says, hey, if you encounter an access control list error while executing this step, please perform the following workaround.

Open SQL Plus, connect to assist DBA, execute the following code. OK. You don't have to do this in SQL Plus. All you have to do is open up a window in SQL Developer for PDB1-sys. OK. Copy this code here from the book into your worksheet, and just go ahead and run it. And that's going to go ahead and grant the permissions to your ora61 user to be able to do the debugger.

And by the way, you may also want to grant some additional permissions. I'll show you where those permissions are located. So if I go to sol_04 under home/oracle/labs/plpusolution, and open up sol_04. There's a couple of more commands that-- actually, no, sorry, wrong path-- if you go to Code Examples, and you go to Code Examples for 13, Code Example 13.

I would also go ahead and do these two commands, grant debug any procedure to ora61, and grant debug connect session to ora61. OK. So let me pop that in this PDB1-sys. And I would run both of these as PDB1-sys and grant those system permissions to ora61. And as long as you have done all of that as the PDB1 system administrator, then you can continue on again with step number 5.

Step number 5, edit the emp-list procedure and the get_location function. OK. So I am going to click on emp_list over here in the object tree. And I'm also going to do the same with get_location. So I'm going to right click-- well, I'm just going to click on get_location, as well. So emp_list-- I'm going to right click emp_list by the way, and say Edit.

And, I think I've got too many-- there we are-- too many things open. So let me move this over. What I'm trying to do is to emp_list and get_location in the same location, right next to each other. I'm going to go ahead and close my Code Examples there. OK. emp_list and get_location. I'm going to close out the rest of these tabs, because I've already executed those. All I'm interested in is emp_list and get_location at this point. OK.

So step number 6 says, add four breakpoints to the emp_list procedure to the following lines of code. Open cur_emp. So line 15, click on it. While cur_emp%found. OK. That's line 18. Add a breakpoint there. v_city initialize to get_location. That's line 22. And then close cur_emp. That's line 26.

Page 7, number 7, compile the emp_list procedure for debugging. OK. So, I'm going to click here, compile for debug. OK. And, notice that warnings are expected, because of some deprecated parameters from 11g. And then, page 8-- what I'm going to do is click on debug, the little debug icon. OK.

Next page. OK. Where it says P_MAXROSE. OK. Next page. We're going to change that to 100. And then click OK. OK. Now, if you are not seeing the data and the smart data tabs right here, go up to where it says View, go down to where it says Debugger, and click on Data and Smart Data and Watches so that you get these tabs here in your debugger. OK.

Now it's going to default to showing you the Debugger toolbar, both at the top and the bottom. OK. So this is what it should look like. On to the next page, here's where we're examining the value of the variables in the Data tab. OK. What are the values assigned to rec_emp and emp_tab and why. And notice, we have a message there. You may have to open the Data, Smart Data, and Watch this tab by clicking on View, Debugger, whichever one of those that you want, whether that's Data Smart Data or Watches, so that you can get those tabs open as I mentioned here. OK.

And they're saying, OK, what are the values assigned to rec_emp and emp_tab. Let's look at that. rec_emp and emp_tab. OK. Looks like nothing is assigned yet. Right. Let's look at rec_emp. Nothing's assigned yet to those, because they're null. Right. And that's because we just barely open the cursor. Right. So on to the next page. That's what they're showing here. Hey, we have all nulls for our record and for our emp_tab index table.

Next, step 11, use this Step Into debug option to step into each line of code in the emp_list, and go through the while loop only once. Press F7 to step into the code only once. That's this one right here. F7. And now it says, examine the value of the variables in the Data tab. What are the-- what are the values assigned to rec_emp and emp_tab? OK.

Well, we're-- we are right here, cur_emp. OK. Let's take a look at our data. I have no data here on either one. So let's Step Into again. Let's Step Into again. OK. There we are. You notice how i is 1. Let's take a look at our rec_emp. Still null. Let's go ahead and hit F7 again. You notice how now, where we're at this execution point, where we're initializing our-- so here's our rec_emp. emp_tab is initialized to rec_emp. OK.

So, in the line 16, we've actually grabbed a row from our cursor and popped that in our record. So that's why our record now has values in it. Let me go back up. Let's take a look at our index table, and see if we have any values in there. OK. We don't have any values in there yet. So I'm going to hit F7 again. And now when I go in and look at my values for my emp_tab, you'll notice that I have at Key 1, I have all of this data for Whalen stored at Index 1.

So that's what they're telling us to do here in number 11 and 12. OK. Use this Step Into debug option to step into each line of code, and go through the while loop only once. I've only done that once. I'm looking at my first iteration here. And let me go back up to where I can see i, i is only 1. And then, onto the next page, page 13. And this is where it told us to go ahead, and click on F7 until emp_tab i initialized to rec_emp line is executed. And I showed you that.

We're pointing to Whalen. Right. And now what we want to do is we want to modify the i counter to 98. So we're going to right click i. And we are going to modify the value. OK. And we're going to change that to 98, and click OK. Now, next page, they're showing us what that should look like. And then the next, page 15. OK.

Continue pressing F7 until you observe the list of employees displayed on the debugging log table. And how many employees are displayed? So let's go ahead and run that. Keep pressing F7. There's what they're showing us there-- Toronto-- where i is now to 99. OK. We can expand this, if you want to see that. Let's go back. OK.

i is now at 100, so we're at the maximum number of rows. You notice as I'm clicking F7, and it's going through the code. And, finally, we are in our output line here. Right. And let's take a look at our i value. OK. So this is what we're saying here. OK. How many employees are displayed? Well, it looks like we've got four employees displayed. Right. We can go ahead and expand those. All right.

So number 16. If you use this Step Over debugger option to step through the code, do you step through the get_location function? Why or why not? So, although the line of code, where the third breakpoint is set contains a call to the get_location function, this Step Over executes the line of code, and retrieves the return value of the function. However, the control is not transferred to the get_location function. So, just making sure that you know what Step Over versus Step Into means.

So it does execute it. We just don't see that execution, because it stepped over the call and ran it. All right. Now Smart Data, just to show you what that looks like. We've got our emp_tab and the Watches-- we didn't have you set any Watches-- but you could create your own watch, as well, by right-clicking on your Watches. OK. So that is going to do it for the practices for Lesson 13.
