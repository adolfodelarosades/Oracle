# 8: Using Explicit Cursors

* Using Explicit Cursors - New - 28m
* Cursor FOR Loops - New - 15m
* Practice 8-1: Using Explicit Cursors - New - 23m
* Practice 8-2: Using Explicit Cursors: Optional - New - 11m

## Using Explicit Cursors - New - 28m

All righty, let's take a look at Lesson Eight on using explicit cursors. We are here in Unit Two, Programming with PLSQL, Lesson Eight, "Using Explicit Cursors." OK, the objectives-- after completing this lesson, you should be able to do the following, distinguish between implicit and explicit cursors, discuss the reasons for using explicit cursors, declare and control explicit cursors, use simple loops and cursor FOR loops to fetch data, declare and use cursors with parameters, lock rows with the FOR UPDATE clause, and reference the current row with the WHERE CURRENT OF clause.

OK, so what are explicit cursors? So a cursor is a pointer to a private memory area that is used to execute SQL statements in PLSQL blocks. And we have two types of cursors. We have implicit cursors and explicit cursors.

So we talked earlier about implicit cursors. And implicit cursors are the ones that are automatically opened by PLSQL in order to process a select statement. Explicit cursors, on the other hand, are cursors that are defined by the programmer.

And you know, I paraphrased that a moment ago. But here we are showing you that implicit cursors are created and managed by PLSQL. They're created for select or DML statements, closes after the associated statement is run. And hopefully you remember those implicit cursor attributes, SQL%FOUND, SQL%NOTFOUND, and SQL%ROWCOUNT.

And so here they're showing you that an explicit cursor is created and managed by a programmer in the PLSQL block. Now, when we define an explicit cursor, what we'll do is we'll define a select statement. And the select statement forms a particular data set that we call the active set.

And the active set automatically gets a pointer that points to the first row in that active set. So if I do a select star from employees, my active set is my whole table. And I get this little pointer that gets pointed to the first row of data in that table.

And in order to control explicit cursors, we're showing you the flowchart of what we need to do. Now, we have a couple of different ways of writing explicit cursors, by the way. So what we're showing you here is what I would consider the longhand method, where we declare the cursor. That's where we create a named SQL area.

We open the cursor, which identifies the active set. We have to load the current row into the variables. We do that using a fetch. And then we test to see if we have more rows, test for existing rows, as we're saying here.

Now, if we don't have any more rows to process, then we'll go ahead and close the cursor which releases the active set. However, if we are not empty, if we still have rows left remaining, we have to go through this kind of a looping mechanism where we will fetch the next row. And then we'll fetch the next row. And then we'll fetch the next row until finally we've processed all of the rows in the cursor. And in that case, we can go ahead and close the cursor which releases the active set.

So how to use explicit cursors, I think what I'll do is I'll do my demos. And then we'll come back and take a look at the book. Let me open up a new worksheet for you here. OK, so I'll have a declaration section. And I'll come in and I'll say CURSOR empcursor-- oops, if i can spell empcursor correctly-- is select star from employees.

Now, remember in the book it said, hey, we're going to go ahead and open the cursor and then we're and fetch the row from the cursor into our variables? So that kind of implies that I need to have variables as well. So I'm going to go ahead and define a record of the employees%ROWTYPE.

Now, since my cursor is selecting all of the rows, my record needs to match the structure that I'm pulling from. So I'm just doing it a really simple way. I'm defining a cursor which selects the whole table. I'm defining a record which allows me to store a whole row from the same table.

Now what I need to do is I need to open my cursor. And let me correlate this to what the book was showing us. Let me go back a page, a couple pages. So I've declared my cursor. And now I've opened it.

Next what I need to do is I need to do the fetch. And I need to do this kind of a loop process so that I fetch and check to see if I have more, and then fetch and check to see if I have more before I finally close my cursor.

So that's what I'm going to do. I'm going to fetch empcursor into emprecord. And then just to show you that my record now has the values from my cursor, I'm going to do my record.last_name. I'll go ahead and print that out.

And I'll go ahead and run this just to show you that I'm getting back King. But you know, if I run it again, I'm only getting back King. So if you think about that pointer pointing to the first row in my active set, the first row of my table basically is what I'm pointing to. And so what I need to do is I need to do some sort of a loop.

So remember, if I have a loop, I need to have an end loop. And what I need is I need to have a valid exit condition. So I'm going to come in. And I'm going to say exit when.

Now previously, we exited out of our loops with a valid exit condition. And we also used the implicit cursor attributes, exit when sql%rowcount greater than 5, something like that. Well, we have explicit cursor attributes as well. Instead of doing SQL%rowcount greater than 5, or something like that-- this is an implicit cursor attribute meant to be used with implicit cursors.

With explicit cursors, we will, instead of using the SQL keyword, we're going to use the name of the cursor. Exit when empcursor%rowcount greater than 5. Or exit when empcursor%notfound. So basically, once we run out of rows in the cursor, that's when we're going to exit our loop.

So let's go ahead and run it this time. And you'll notice that in this case, I just got a bunch of Kings. And so what did I do? I have my fetch up here. I'm going to reverse where my loop is.

Open the cursor loop, fetch the value into the record. I don't want just a bunch of Kings. I don't want Stephen King over, and over, and over, and over again. And let's go ahead and run it again.

So that's one thing I wanted to show you. Make sure your fetch is in the right spot. When I reversed my loop and my fetch, then you notice that it runs correctly.

Now, sometimes we do something like this. We'll go ahead and have a fetch before the loop. And we'll have a fetch after the loop. And you have to be kind of careful when you build your looping mechanisms. Do you notice how I have gets twice at the end?

So you had to be kind of careful about your exit condition. Exit when empcursor%notfound. Let me move this. Let me move it further up in my loop. Let me run it again.

Exit when empcursor%notfound. Fetch the cursor into the record. So you notice I still have a problem with gets. And by the way, do I get King up at the top? You notice how I don't get King up at the top.

So I'm actually not going to put my fetch up at the top, because I'm actually going to miss King on the top. Let's go ahead and run it without that first fetch. There I've got King. I still have a problem with gets listed twice.

So I'm actually going to move this back. I'm going to put it down there. It looks like I'm missing my semicolon. There we go.

All right, so it still doesn't like that in that position. I still get gets twice. So let's go ahead and swap the order of these. And there we go.

So you know, it pays to kind of know your data. You know, you should go in and make sure that you're selecting the correct data. Make sure you're not processing in the same row multiple times. Make sure that you're not skipping a row.

So this is the definition of the structure that you'll probably want to kind of mimic. Open the cursor. Loop it. Fetch the cursor into the record.

Check for the existence of rows. Do your process, whatever that process happens to be. End the loop. And then end. And, best practice, we should close the cursor as well.

Now, it's not mandatory that you close the cursor. But if you open and close the same cursor within the same PLSQL executable with different values-- maybe you want to have a parameter where you're processing all of the rows from department 10, and then you want to process all other rows from department 20, and then you want to process all the rows from department 30-- if you don't close the cursor before you try and reopen it with a new department value, you're going to end up getting an error that the cursor is already open.

OK, let me show you that. I won't close it. And I will go ahead and just repeat this right there. I'll try to open the cursor again. And I haven't shut it. And you notice that I get an error message. The cursor is already open.

So we can actually do a check. We have another explicit cursor attribute called if empcursor%isopen then close empcursor. So this is an explicit cursor attribute. We actually have four of them, cursor name %isopen, cursor %found, cursor %notfound, cursor %rowcount.

And what this can do is to close the cursor and then reopen it. Now, I haven't showed you how to do parameters yet, but that's kind of the case. I may as well show you how to do parameters now.

What I can do is I can do this and say pdept number. And what I'll do is I'll modify my query. And what I'll do is I'll open my cursor for department 10. And then I'll open my cursor for department 20.

OK, I only have one employee in department 10. I only have two people in department 20. So I'll tell you what. I'll go ahead and put down 10 here so that you can tell that that one comes from department 10.

OK, so this one came from department 10. Then I closed it. Then I reopened it with department 20. So I may as well put 20 here as well.

So, really easy to add a parameter-- now, when you do parameters, you're not allowed to give it a size. You can you is a dedicated data type like this, number, varcar2, any of those. You can use the percent type attribute as well.

But you're just not allowed to give it a size. So just remember that. We'll talk more about parameters when we go in to procedures and functions coming up.

OK, so there is a parameter. I'm using the parameter. When I open my cursor, I close it. I reopen it. And then I should also close it on the end. All right, so there you go.

OK, well, let's take a look at the book. And I'll show you what the book is going to say about it. So here we have declaring the cursor, CURSOR c_emp_cursor IS SELECT employee_id, last_name FROM employees where department_id equal 30. And DECLARE v_loc, that's just the standard variable. But then we declare a cursor, CURSOR c_dept_cursor IS select star from departments where location_id equal v_locid.

Open the cursor, easy. Fetch-- we're fetching the row from the cursor into the two variables. In this case, we're using two scalar variables. We have two columns in our employees table that are selected. We have two variables.

So we're fetching the cursor and the two variables. Again, you have to be careful about the order of the variables. They have to match the order that you've listed the columns and the cursor definition.

And then we're adding on the loop. And we're adding on the valid exit condition. And that's where they're showing you the explicit cursor attribute, EXIT WHEN cursor name %NOTFOUND. And then we're closing the cursor.

Now, I showed you, when I did mine, I defined a record based upon the row type of my table. What we're showing you here is maybe a better idea, is to declare your record according to the structure of the cursor. So let me go in and show you that in my demos here.

So right now my record matches the structure of this cursor because they're both selecting a star. But what if my cursor is selecting last name and salary? Well, guess what. Now my record can hold 11 pieces of data, but my cursor is only selecting two pieces of data per row. So I would actually error out if I ran this, wrong number of values in the into list of a fetch statement.

So what we can do is we can put the name of the cursor here. And now my record is going to match the definition of my cursor. And so you'll notice now that I can interact with my last name. I can interact with the salary instead, either of those two columns that I'm selecting here.

So I've got my last name up here. I've gotten my salary down here, because I wanted my salary here. I wanted my last name here. So that is really the recommendation when you define records to hold your rows from cursors so that the records always match the cursor definition.

OK, now we have a shortcut for you guys. There is something called a cursor FOR loop. The cursor FOR loop is a shortcut to process explicit cursors. It implicitly opens. It implicitly fetches. It implicitly exits. It implicitly closes. It implicitly defines the record.

So let me go in and show you. I tell you what. I will copy this part of my demo. And I'll copy that into another worksheet here. And let's just go ahead and run it, make sure it runs successfully.

All right, so let me show you how much easier we can get this. Declare cursor empcursor. We'll go ahead and put a parameter in here. And I may as well copy the rest. Well, yeah, I'll just copy this.

OK, now I'm not going to define my record. I'm just going to go to my executable section. And then I'm going to do my cursor For loop. For emprecord in empcursor loop. We have a loop. We have an end loop. And all I need to do is just print out the last name.

So here is my cursor passing the parameter. And automatically opens it, automatically fetches, automatically closes. So let me just clear that out and run it again just to show you.

Really easy-- let's do department 90 instead of department 10. I'll change this to 90. And there we are, the three people in department 90, King, Kocchar, and De Haan. So this is a cursor FOR loop.

Now, if I didn't want to put a parameter in here, I don't have to put a parameter in here. And I could just print out all of my names of my employees, all 107 of them. I don't have to worry about position of my exit condition versus my process and my fetch.

It worries about all that for you. This is our implied record. It always matches the structure of our select statement.

Now we can even get it more simple. I could actually put my select statement here. And if I did that, I don't even need my declaration section. And so that's a really easy way. Whoops, looks like I have an extra underscore there, unfortunately. There you go, so really, really, really easy way to use a cursor.

## Cursor FOR Loops - New - 15m

All right, so let's take a look at the book again. And that's what they're showing you here, CURSOR c_emp_cursor IS SELECT employee_id last_name FROM employees WHERE department_id equals 30 FOR emp_record and cm_emp_cursor loop. And then we're just using the values from the record, record.field, record.field.

Now, cursors are used for just grabbing a whole chunk of data and processing through it. They're similar to index by tables. With index by tables, however, you have an index. So you can pick and choose the order that you want to process, because you could refer to the index and then do whatever process you want on a particular row.

So if you were in a shopping cart application, if you were ordering something online, and you put a bunch of stuff in your shopping cart, and all of a sudden you decide you don't want the third item in a list of eight, you could go and delete just that element. So that's kind of how I would use an index by table, allow people to load up a shopping cart and then delete things they decided they didn't want before they place their order. With a cursor, you're just selecting a bunch of rows and processing through the bunch of rows.

All right, I talked about explicit cursor attributes. Here is where we're telling you about those in the book. If the attribute ISOPEN, evaluates to true if the cursor is open. NOTFOUND or FOUND, evaluates to true if the most recent fetch does not return a row or if it does return a row. And then we have %ROWCOUNT, evaluates the number of rows that has been fetched. We can have more than one exit condition. Exit when cursor_name%ROWCOUNT greater than 5 or cursor_name%NOTFOUND.

All right, here is where they're talking about the ISOPEN attribute. You can fetch rows only when the cursor is open. So it's recommended to use the ISOPEN cursor attribute before performing a fetch to test whether the cursor is open. So here they're saying, hey, if not the cursor is open, then open the cursor, meaning, if it's closed, open it.

So here is an example where we have more than one exit condition. EXIT WHEN c_emp_cursor%ROWCOUNT greater than 10 or c_emp_cursor%NOTFOUND. We have 107 rows. We only get 10 printed out here, so we can tell which exit condition kicked in here. the EXIT WHEN the cursor%ROWCOUNT greater than 10 is what controlled this one.

And here is where they're showing you how to do a cursor for loop with a subquery similar to what I showed you. For record name in your subquery loop, do your process. And then end your loop. We don't have to declare the cursor when we use a subquery.

All right, cursors with parameters, I talked about that already. Parameters allow you to open an explicit cursor several times with a different actors set each time. So here we're passing in department 10-- or sorry, a department number through the parameter. We are opening the cursor for department 30. And we get all the people in department 30 listed. And then we're going to close the cursor. And then we're going to open it with department 10. And we're going to get anybody that works in department 10. There is only one person in department 10. So that is your parameters.

All right, I mentioned that a lot of times, cursors are used just to process a bunch of data. So what if we wanted to grab a bunch of data through our cursor and then iterate through it in order to do some sort of an update on the table? Well, what we can do is, we can lock the rows to make sure that we have control of those rows before we do our update. We want to use explicit locking to deny access to other sessions for the duration of a transaction.

You know, usually when we build these PLSQL components, we'll schedule those to run at night. And we want to make sure that there is nothing else that's going to affect the runability of our sub program. And so we'll go ahead and put a lock on the rows then do the update or the delete on those rows. And then we'll do a commit or a rollback, which will release the lock. And then other people can have access to it.

So what we'll do, let me go and do a demo on that. Now, let me take it back to something simple here. I won't use parameters just to keep it simple. We'll just process the whole set. So what I'll do is I'll do a for update. Now, just in case somebody else already has a lock on the rows, I'm going to put a weight reference on there. This allows us to wait 10 seconds. And I tell you what. Let me do rollback here. And let me open up another worksheet. Let me show you what happens.

So this person here in this session is going to go and execute this update statement and update the row. I haven't committed it or anything right now. So I still hold the lock on this row. So now when I come in in another session and I want to come in and update employees, set salary equal to salary times 1 where current of empcursor. What we're doing with the where current of clause is we're updating a row in the employees table that matches the row that we're currently on in the cursor. So if we're processing row by row by row, this ensures that we're kind of synchronizing the pointer and our cursor to our update statement on the table that the cursor is based upon.

So let me go ahead and run this, get rid of that one so you can see that one. Now, because the other session has a lock on the data, you notice how it's hanging? But because I put a weight 10 reference in there, after 10 seconds, it's going to return control back to my session. And you notice what it says. Resource busy. Acquire with wait timeout expired. The requested resource is busy. Retry the operation later. By the way, I'll comment this out, because this accidentally ran at the end.

So that's what that does, is it ensures that I don't get locked. When somebody else gets to the rows first, I want to make sure that my executable didn't hang. You can also say no wait, by the way. Oops-- and what will happen is it will return control immediately. There you go, resource busy and acquire with no wait specified or timeout expired.

If you don't put a wait reference there, it's going to hang indefinitely or until something else kicks it out. Like maybe there is a blocking session initialization parameter that's set by your DBA that says, hey, if somebody keeps you waiting for more than 15 minutes, let's kill that other session.

But now let me go ahead and roll this back. So I'll undo that change here. And the rollback will also release my lock. This time I'm going to go ahead and do the run. And it's successfully completed. But because I have the for update clause on it, Now this person is not able to make any changes because the for update locks the entire active set.

So now what I would have to do over here is I would have to do some sort of a command or a rollback or something like that. And it's always a good idea, if you have a for update clause in your cursor, make sure in your block that you have a commit, and if you have an exception handler, that you also allow for terminating the lock through maybe a commit or a rollback.

And what that will do is it will go ahead and release the lock at the end. And you notice now how, over here, this person was able to finish up. So just be considerate of that, what happens when you use the for update clause.

So here is where the book is talking about it. UPDATE employees SET salary equal to whatever WHERE CURRENT OF the cursor. And then the book example-- we're locking all the rows in department 30. We're going out there and setting the salary go to $5,000 for each of those individuals. And they should have put a commit to undo the lock. By the way, you can put a for update, a column reference too, so for update of salary, for instance.

So in the event that you have a cursor that has more than one table in its definition, maybe you do a join of some sort. If you put the column refrence in there, it will only lock the rows that belong to the table that has the salary column in it. And the other table would not be locked. But if you don't include the column reference, then all the rows that are part of the active set for both tables would get locked. So just kind of keep that in mind.

OK, quiz time, explicit cursor functions enable a programmer to manually control explicit cursors in the PLSQL block. That is true.

OK, so you should have learned how to distinguish cursor types, implicit cursors, and explicit cursors. Implicit cursors are used for all DML statements in single-row queries. Explicit cursors are used for queries of zero, one, or more rows. You should have learned how to create and handle explicit cursors, use simple loops and cursor FOR loops to handle multiple rows in the cursors, evaluate cursor status by using cursor attributes, and use the FOR UPDATE and WHERE CURRENT OF clauses to update or delete the current fetched row.

So we're going to have a try this was Practice 8. You're going to declare and use explicit cursors to query the rows of a table. You're going to use a cursor FOR loop.

You're going to apply cursor attributes to test the cursor status. You're going to declare and use cursors with parameters. You're going to use a FOR UPDATE and the WHERE CURRENT OF clauses. OK, so that's going to do it for Chapter 8.

## Practice 8-1: Using Explicit Cursors - New - 23m

I will now demonstrate practices for Lesson Eight, "Using Explicit Cursors." Let's just look and see how many we have. It looks like we've got one where we're going to have some output, it looks like for different departments, and raises, and that sort of information. It looks like we have a number two. And that's the output from the number two. OK, so it looks like we have two different problems for this one.

All right, let me demonstrate the solution for 8-1, "Using Explicit Cursors." We're going to perform two exercises, as we expected. First you use an explicit cursor to process a number of rows from a table and populate another table with the results by using a cursor FOR loop. Secondly, we're going to write a PLSQL block that processes information with two cursors, one that uses a parameter and it looks like one that does not.

And then we'll go ahead and start with number one. We're going to create PLSQL block to perform the following. Step letter A, it looks like we're going to have a declarative section. So let me open up a worksheet.

OK, we're going to declare and initialize a variable named v_deptno of the number type. And we're going to assign a valid department ID. So it looks like they're going to assign department 10 at this point. So let me go ahead and do that, declare v_deptno of the number type initialized to 10.

In letter B, we're going to declare a cursor named c_emp_cursor which retrieves the last name, the salary, and the manager ID of employees working in the department specified in whatever department we put for v_deptno. So you know, who are the departments in department 10, basically. So let's go ahead and do the cursor, CURSOR c_emp_cursor IS select the last_name, salary, and manager_id from the employees table where the department_id equal v_deptno. OK, so far so good.

Now in step letter C, it says in the executable section, use the cursor FOR loop to operate on the data retrieved. If the salary of the employee is less than 5,000 and if the manager is either 101 or 124, we want to display the message, whatever the last name is, due for a raise. Otherwise we want to display the message whoever the last name is not due for a raise. So let's go ahead and demonstrate that.

We'll start our executable section. We'll do a cursor FOR a loop. So we're going to do an implied record here called emp_record. And we're going to put the name of our cursor next. We'll go ahead and loop.

If the salary inside the record is less than 5,000 and the emp_record.manager_id IN 101-- I'm sorry-- dot manager_id equal 101 or emp_record.manager_id equal 124. And by the way, we're using parens around the or conditions because the or operator has less priority or less precedence than the and operator.

So we want to make sure that we look at our manager IDs individually and then apply the summer condition. If we didn't put parens around this, then we would just be looking at salaries less than 5,000 who work for 101 or anybody that works for manager 124. So make sure you get those parentheses in there to get the correct result out.

Let's do it then. Let's go ahead and get the last name, dbms_output.put_line emp_record.last_name, due for a raise, else dbms_output.put_line emp_record.last_name concatenated to not due for a raise, end if, end loop, end.

All right, continuing on to page six, we're supposed to test the PLSQL block for these different cases. We'll transfer department 10 first. So let's go ahead and run it for department 10. Oh, it looks like I have an error. Let's see what the error is. Line 14, column 44, encounter, looks like a double quote someplace maybe. Ah, missing a single quote on the end, there we go. That'll do it.

Ah, emp_record, I see exactly. It's supposed to have an underscore. That's on line 11. There we are. Try it again. There we go, Whalen due for a raise. Let's go ahead and try it for department 20. Hartstein not due for a raise, Fay not due for a raise. Let's try for department 50. OK, a bunch of employees-- it starts with Weiss not due for a raise and ends with Grant due for a raise.

And then let's try department 80. And we see that department 80 starts with Russell not due for a raise and Johnson not due for a raise. OK, so that looks good. Now, I don't think they wanted us to save that. No, they don't want us to save that.

So next let's go in to number two on page six. You can open up a new worksheet. And we're going to write a PLSQL block that declares and uses two cursors, one without a parameter and one with a parameter. The first cursor retrieves the department number and the department name from the departments table for all departments whose ID number is less than 100. And then the second cursor receives the department number as a parameter and retrieves employee details for those who work in that department and whose employee ID is less than 120.

OK, so step letter A, declare a cursor called c_dept_cursor to retrieve the department ID and department name for those departments with department ID less than 100. We're going to go ahead and sort it on the department ID. Let's go ahead and do that.

DECLARE cursor c_dept_cursor is, select the department_id department_name from departments where the department_id is less than 100. And we're going to sort it. It's going to be sorted in ascending order, it looks like, by default.

All right, let's go on to page seven. We're going to declare another cursor called c_emp_cursor that takes the department number as a parameter and retrieves the last name, the job ID, the higher date, and the salary from the employees table of those employees who work in that department with an employee ID less than 120. So let's go ahead and do that one.

Another cursor, we'll call this one c_emp_cursor. And here is where we're putting our parameter in, v_deptno of the number type. Remember that your parameters aren't allowed to have a size, so make sure you don't put a size on that. And then we'll select a last_name, the job_id, the hire_date, the salary from the employees table where the department_id equals v_deptno and the employee_id is less than 120.

Now in step letter C, we're asked to declare variables to hold the values retrieved from each cursor and use the percent type attribute while declaring the variables. All right, so it looks like about six different variables, one called v_current_deptno. It's going to be the departments.department_id%type, another one called v_current_dname. That one's going to be the department.department_name%type. And then we're going to do v_ename. It's going to be the employees.last_name%type. And then we'll do a v_job. And we will do one for the hire date, and finally, the salary.

OK, next we're going to open the c_dept_cursor. And we're going to use a simple loop to go ahead and fetch the values into the variables that are declared. And we're going to display the department number and department name and use the appropriate cursor attribute to exit the loop.

All right, let's go ahead and do that. We'll go ahead and open the c_dept_cursor. We're going to loop. We're going to fetch the record from c_dept_cursor into your two variables, v_current_deptno and v_current_dname. I'll tell you what. I'll go ahead and wrap those variables around so you can see that a little better.

All right, and then we're going to exit when c_dept_cursor%notfound, when we have no more records left in the cursor. And then let's go ahead and print those out, dbms_output.put_line. And I'll tell you what. I'm just going to copy these from the book just to make it easy to avoid typos and things like that on the labels.

OK, department number, v_current_deptno, that variable, department name, v_current_dname, the value coming from that variable-- continuing on to page eight, we're going to then open the c_emp_cursor by passing the current department number as a parameter. We're going to start another loop and fetch the values of emp_cursor into the variables and print all the details retrieved from the employees table.

So we should check whether or not the c_emp_cursor is already up and before opening it again. We're going to use the appropriate cursor attribute for the exit condition. And then when the loop completes, we're going to print a line after you have display details of each department and then close the cursor called c_emp_cursor.

All right, let's go ahead and do that. So let's do an if c_emp_cursor%ISOPEN, then we need to close it. And then let's go ahead and open it. And we'll pass in the v_current_deptno. And then we'll loop. And then we'll fetch the row from the cursor into the variable v_ename, v_job, v_hiredate, and v_sal.

And then we'll have an exit condition when c_emp_cursor%notfound. And then we'll go ahead and print out the appropriate values, dbms_output.put_line v_ename concatenated to a space concatenated to v_job concatenated to a space concatenated to v_hiredate concatenated to a space concatenated to the salary. We'll end the loop. And then we'll close.

Well, before we close that, we'll do another dbms_output. It looks like they're just going to have a bunch of hyphens or underscores depending on what you want. And then we'll close the cursor.

Then we'll end our outer loop-- or not our outer loop, but our other loop. And then we'll close-- actually, I guess it is our outer loop. Here is our main loop. And so this is closing the inner loop that is started here. This is closing the outer loop, which is started up here.

OK, now let's go ahead and continue on to step number nine, execute the script. And let's see what we're supposed to save it as. Oh, they don't want us to save it, so OK-- well, at this point anyway.

All right, let's go ahead and run it. And oh, get some errors, so line 20 you have a fetch. So let's go out to our outer loop. There is our open c_dept_cursor, loop, fetch c_dept_cursor into v_current_deptno and v_current_dname. Well, let's make sure I spelled it correctly.

I'll tell you what. Let me look through here again. Cursor c_dept, cursor, there we go. Oh, missed my BEGIN keyword. So here is the end of my variable declaration. Here is my open. So I was just missing my begin. There we go. Let's try that again, shall we?

OK, so let's compare that with page nine. There you go, administration, marketing, purchasing, human resources, down through the very last department, which is the executive. All right, well, I guess that's going to do it for the demonstrations for Practice 8-1.

## Practice 8-2: Using Explicit Cursors: Optional - New - 11m

 
I will now demonstrate practice 8-2, Using Explicit Cursors. Now notice that this one is actually an optional lab. So it does tell us, if you have time, complete the following optional practice. Here, you're going to create a PL/SQL block that uses an explicit cursor in order to determine the top n salaries of employees.

I'm going to go ahead and start with the solution page. We're going to execute the lab_08_02.SQL script to create a new table, called TOP_SALARIES, for storing the salaries of the employees. So let me go ahead and do that. I'm going to open up the lab_08_02.SQL. Notice it's going to create a table called TOP_SALARIES, so I'll go ahead and run that into MyConnection connection.

And you noticed that it created the TOP_SALARIES table. Let's go over and just refresh our table list, so that we can see it over here. And let's see what it looks like. It looks like just a single column there, called SALARY. And let's go ahead and close the script there.

And then step number 2, it looks like we're going to have to create a declarations section, so I'm going to open up a new worksheet. All right. In the declarative section, declare a variable called v_num of type number. That holds a number n, representing the number of top n earners from the employees table.

For example, to view the top five salaries, enter 5. Declare another variable called v_sal of type employees.salary. And declare a cursor called cm_cursor, which retrieves the salaries of employees in descending order. And remember that the salaries should not be duplicated, so it sounds like we're going to have to have some kind of a distinct methodology.

All right, so let's go in and do a declare v_num, number with the precision of 3, initialized to 5. OK. Another one called v_sal employees.salary%type. And then our cursor.

Now let's go in. OK. So I'm just thinking, they don't have a distinct in there, but I notice that they have a reminder that the salaries should not be duplicated. So what we would do is I'm going to go ahead and do a distinct. select distinct salary from employees. order by salary descending. OK, the solution, they don't have a distinct, but I think I'm going to go ahead and do that on mine since they said they don't want the salaries to be duplicated.

And then step number 3. In the executable section, open the loop. Fetch the top n salaries and then insert them into the top_salaries table. You can use a simple loop to operate on the data. Also try and use the percent row count and percent found attributes for the exit condition. And make sure that you add an exit condition to avoid having an infinite loop.

So let's go ahead and do what they're telling us here. Begin. Open our cursor, c_emp_cursor. Let's fetch the cursor into the v_sal variable, while-- we'll do a while loop-- c_emp_cursor%rowcount is less than or equal to v_num and c_emp_cursor%found loop.

And we'll do an insert into our table called top_salaries into the salary column. The values from the v_sal variable. And then we'll end the loop. And then we'll close our cursor.

OK, so let's look at that logic. Here's our cursor. Select distinct salary from employees. Order by salary descending. Open the cursor. Fetch the cursor.

So we're going to select the salary into the v_sal variable, while the row count is less than v_num, while the row count is less than 5. And we're still finding rows in our cursor. OK, we do a secondary condition here. Remember, if we run out of rows, it's going to throw an error on a cursor if we don't have it handled correctly in the looping mechanism.

So we're either going to do a 5 or until we run out of rows in the cursor. And then we're going to insert, into the top_salaries table, the values from the v_sal variable. And then we're going to fetch the cursor into the v_sal variable again. And then we're going to end the loop, and then we're going to close our cursor.

All right, looks good. So let's go ahead and run it. And then in step number 4, we're asked to go ahead and select from the top_salaries table and see what that looks like. OK, it looks good. Let's compare that to what theirs look like.

Now they have duplicates in their screenshot. 17,000. 17,000 twice. And that's because, as I mentioned, they do not have the distinct in theirs. So we could actually do a rollback if we wanted to make sure that it matched what theirs looks like, and I could go ahead and remove that distinct keyword. And we can run it again.

And then select from the top_salaries table. And there, you notice how we have duplicated salaries there. All right. Well, let's take a look the last step. Test a variety of special cases, such as v_num equal zero or if v_num is greater than the number of employees in the employees table. And then empty the top_salaries table after each test.

So yeah, let's do a rollback again, and let's test, as they're saying there. OK, let's try v_num of 0, as they were describing. Let's see what happens. We'll select star from top_salaries. Notice nothing in it was zero.

Now we have 107 rows in our tables, so let's try 110. And let' see what that looks like. And let's select star from top_salaries. And there we go. So we still only got 107 rows even though it doesn't need to run it 110 times. So there you go. OK, so that is going to conclude the demonstration for practice 8-2.
