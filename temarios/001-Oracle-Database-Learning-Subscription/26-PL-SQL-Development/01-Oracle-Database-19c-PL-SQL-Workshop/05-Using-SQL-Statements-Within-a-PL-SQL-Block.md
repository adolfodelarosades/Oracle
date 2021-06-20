# 5: Using SQL Statements Within a PL/SQL Block

* Using SQL Statements Within a PL/SQL Block - New - 17m
* Practice 5-1: Using SQL Statements Within a PL/SQL - New - 15m

## Using SQL Statements Within a PL/SQL Block - New - 17m

OK, my friends, let's take a look at Lesson 5 on using SQL statements within a PL/SQL block. We are here in the last chapter of unit number 1. And the objectives for this chapter, after completing this lesson, you should be able to do the following-- determine the SQL statements that can be directly included in a PL/SQL executable block. Make use of the INTO clause to hold the values returned by a SQL statement. Manipulate data with DML statements in PL/SQL. Use transaction control statements in PL/SQL. Differentiate between implicit cursors and explicit cursors. And finally, to use SQL cursor attributes.

All right, the next section here, the first section here, SQL statements in PL/SQL blocks-- so a SQL consists of three sub-languages. It consists of DDL. It consists of DML. And there's also one not listed here, called DCL, which stands for Data Control Language. DDL stands for Data Definition Language. DML stands for Data Manipulation Language.

So DDL statements are generally not included in PL/SQL blocks. DDL statements are those statements that we use to create things, like tables. And we use DDL statements to go in and alter existing objects, like adding columns or adding constraints. DML statements are generally included in PL/SQL blocks. DML would be your insert, your update, your delete, and your merge statement.

So SQL statements in PL/SQL, we use the SELECT command to retrieve data in the PL/SQL block. We use other DML commands like insert, update, delete, and merge in order to make changes to the database. And we are allowed to use COMMIT, ROLLBACK, or SAVEPOINT commands for transaction control. So those are going to be allowed as well.

So when we have a select statement in PL/SQL, as we've described already, we need the INTO clause. And the queries can on their return a single row. So here, we notice that we are pointing to a specific employee ID. That employee ID happens to be a primary key column. And we know that we're only going to get back one first name into the vf name variable. So it looks like employee 200 is Jennifer.

Now here, we have two columns. And so what we're going to do as we're going to need two scalar variables to capture those two values. As I was hand earlier, they're going to be positionally matched. The hire date column is going to return the date into the v_emp_hiredate variable. The salary is going to be returned into the v_emp_salary variable. And we see here that employee 100's hire date is the 17th of June of '11. And employee 100's salary is 24,000.

Now, previously, we said that we can't use group functions with PL/SQL. Here, we're showing you that we can use a group function in the SQL components. And we're using that group function to populate the sum of the salary into the variable for a particular department in this case, which is department 60. And it looks like department 60, the sums of all of the salaries is 28,800.

Now earlier, we started talking about the naming conventions. So as we described earlier, you should not name the variables exactly the same name as the column names, because not only is it confusing but it might actually cause errors. So here, we see that it's causing an error. We get back the error message, exact fetch returns more than requested number of rows.

Now, what's happening is when Oracle goes in and looks at the WHERE clause, it's going to check to see if there is a column by that name first. If there's a column by that name, then it's going to go ahead and take it as a column. Now, if it can't find a column of that name, then what is going to do is it's going to check to see if it's maybe another structure, like maybe a table name. And then if it can't find it as a table name, it might try and see if it's a variable name instead. So just make sure that you're naming your variables appropriately, but not exactly the same as the column name.

So as I was saying, use a naming convention to avoid ambiguity in the WHERE clause. Avoid using database column names as identifiers. Local variables and formal parameters take precedence over the names of tables. The names of database table columns take precedence over the names of local variables. The names of variables take precedence over the function names. So just be careful over of what you name it.

All right, now manipulating data with PL/SQL, we can use inserts, updates, deletes, and merges in order to do changes to our data. We're showing you an example of an insert. Now, this looks just like a standard insert in a regular old SQL block. The only thing that's different is we put a begin keyword on the front. We've got an and on the end. So now we have PL/SQL block that does an insert. And it looks like we're putting in one new row of data into the Employees table.

Now here, we have an update. We're going to add $800 to somebody's salary. The $800 comes from a variable called v_sal_increase. And then we're going to update the Employees table, set the salary equal to salary plus $800 essentially because the v_sal_increase has been initialized to 800 for anybody who has a job ID of ST_CLERK. So the screenshot in the upper right, we're showing you what the original salaries were. And the screenshot on the lower right, we're showing you what this new salaries are based upon that $800 increase.

All right, we can also delete rows. So this one's pretty easy. We initialize a variable to 176. And then we're going to delete from the Employees table where the employee ID equals 176.

Now, MERGE statement is a pretty long statement. So we're not showing you the complete merge. We have those three dots listed here. And where we've got the three dots listed, we're actually leaving out some of the code. But this is an example of using a merge. We have a MERGE statement that has a begin and end on the end of it. And it's going to go ahead and update if the employee ID in the c emp no value exist. Or it's going to insert data if they don't match.

OK, now we're going to talk about something called a cursor. And the type of cursor that we're talking about currently is what we call a SQL cursor. And a SQL cursor, or a cursor, is a pointer to the private memory area that stores information about processing a specific SELECT or DML statement.

We have two types of cursors. We have implicit cursors. So those are created and managed automatically by PL/SQL. And then we have explicit cursors. Explicit cursors are cursors that are created and managed explicitly by the programmer. Now, we're actually going to have a dedicated chapter on explicit cursor. So we're not going to really talk about those types at this point. But just at this point, realize there are implicit cursors and explicit cursors.

And with implicit cursors, we have these components called implicit cursor attributes. We've got three of them. We've got one called SQL%FOUND. And it's going to evaluate to true if the most recent SQL statement affected at least one row. SQL%NOTFOUND is going to return a true if the most recent SQL statement did not affect even one row. And then we have one called SQL%ROWCOUNT. SQL%ROWCOUNT is going to tell us how many rows were affected by the most recent SQL statement.

So as an example, we're going to try and delete an employee whose ID is 165. Now, we don't happen to know if this is a valid employee ID. And so what we're going to do is we're going to use that implicit cursor attribute to count how many rows were deleted by that DELETE statement. So we're going to delete from the table. We're going to initialize the v_rows deleted variable with SQL%ROWCOUNT concatenated onto row deleted. And then we're going to go ahead and print out the v_rows deleted variable. And we see here that one row was deleted.

All right, before we do the quiz, I'm going to do a demonstration. Let's just take a look at the implicit cursor attributes. And let me just get up there to my environment here. OK, so let's do a declare-- v_empid number. And I'm going to initialize this to 99. Now, if you remember from a previous demo, we don't actually have an employee idea of 99. So if I come in and do a delete, then what I can do is go ahead and run it.

And-- oop, you know what? It looks like I have a trigger that's kicking in. I am actually doing this after office hours. So I'm going to go in and disable a trigger. Just in case you have the same trouble, you know how to disable the trigger. I'm going to right click Secure Employees. And I'm going to disable it. And I'll Apply it.

OK, let's try that again. Now, when we do a delete that doesn't affect anything, it's not actually going to cause an error. It's actually telling me that it's successfully completed. So what I want to do is I want to use my implicit cursor attribute. And what I'll do is I'll just go the easy way. I'll actually just do dbms output put line. And I'll put SQL%ROWCOUNT. And I'll say rows deleted. All right, let's go ahead and run it again. And this time, you'll notice that no rows were deleted, because the SQL%ROWCOUNT is telling us a count of zero.

Now, if I would have had another statement-- here, I've got a delete statement and I've got an update statement, SQL%ROWCOUNT only tracks the most recent statement. And so what's going to happen is I'm going to get a different row count this time. One row is affected. And that's because I actually did do an update. I changed employee 100's salary to $1. And that did affect the row.

So if I wanted to capture both, how many rows were deleted as well as how many rows were updated, I might have to do my SQL%ROWCOUNT more than once. And so now you'll notice when I go in and run this, I can keep track of how many rows were deleted, as well as how many rows were affected by the update. So use it as many times as you need to. I'm going to do a rollback because I don't really want to change his salary. And I have not done a commit or anything like that. So I just changed his salary back to 24,000.

All right, so that's what we're doing with the implicit cursor attribute. So let's take a look at the quiz. When using this SELECT statement in PL/SQL, the INTO clause is required and queries can return one or more rows. Now, that's going to be false. The INTO clause is required. But queries can only return one row. And so because we've got "or more rows," that causes it to error out, or to be incorrect.

All right, so that's going to do it for this chapter. We're going to have you go in and do your practices for Lesson 5. You're going to select data from a table. You're going to insert data into a table. You're going to update data in a table. And you're also going to delete a record from a table as well. And this is going to get you familiar with the implicit cursor attributes.

OK, well, let's go ahead and do that. And I'll talk to you in just a little bit.

## Practice 5-1: Using SQL Statements Within a PL/SQL - New - 15m

I will now demonstrate practices for Lesson 5, Using SQL Statements within a PL/SQL Block. Notice in the practices, if you have executed the code examples for this lesson, make sure that you execute the following code before starting this practice-- drop table Employees 2, and drop table Copy Amp. In this practice, you use PL/SQL code to interact with the Oracle server.

Now, I'm going to start down on the Solutions section so that I can show you the code and also keep track with my demonstrations for this practice. So in this practice, you use PL/SQL code to interact with the Oracle server, as I was saying. We're going to create a PL/SQL block that selects the maximum department ID in the Departments table and stores it in the v_max_deptno variable.

We are then asked to display the maximum department ID. Let me go ahead and demonstrate 1, A, B, C, and D. Going to open up a fresh worksheet. I'm going to declare my variable called v_max_deptno. It's going to be a number type. We're going to start the executable section with the begin keyword, and we're going to select the max department ID into our variable that we just created above.

And then, in order to display that, we'll use the dbms_output.put_line. And we'll go ahead and print out the maximum department_id is v_max_deptno. And then we'll end. Now, one thing that you'll remember that I like to do from my demonstration is I like to right-click and I like to format my code. And so it beautifies my code, makes it look prettier and easier to read.

And then we're going to go ahead and run it. And in my output, you see that the maximum department_id is 270, just as the book is showing us. Now, in step number two, we're asked to modify the PL/SQL block that you created in step 1 to insert a new department into the Departments table. Now, they wanted us to save that number one as lab_05_01_sln.sql.

So let me go ahead and do that. Let me save it. And I'll save it in my Labs directory as lab_05_01_soln.sql And now we'll go ahead and declare those two variables. We have a v_dept_name, which is of the departments.department_name%type. And we'll initialize that to Education, if I can spell education correctly. And then we'll do another one of v_dept_id, which is a number type. And I tell you what. Let me just wrap that code around so you can see the full definition of that.

And then, in step letter B, it says you have already retrieved the current maximum department number from the Departments table. Add 10 to it, and assign the result to v_dept_id. So we'll go ahead and do that. v_dept_id, initialized to v_dept_id+10. Or v_max_deptno. Sorry.

Next page. We're asked to go ahead and include an insert statement to insert the data into the department's name-- into the department name-- Department ID and Location Data columns of the Departments table. Use the values in v_dept_name and v_dept_id for the department name and the department ID respectively, and use null for location ID.

So let's go ahead and do that. Insert into departments department_id, department_name, and location_id. values v_dept_id, v_dept_name, and null. And by the way, if you want to just double-click these variable names, you'll see that it lights up where it's coming from, highlights it in pink. And that way, you can double check that you don't have any typos or anything like that either. So we can see where that comes from.

Now, in letter D, we're asked to go ahead and use the SQL attribute SQL%ROWCOUNT to display the number of rows that are affected. And remember, that has to be immediately following the statement that we want to track. So I'm going to put it just below my insert. SQL%ROWCOUNT gives-- now, this is just a-- it's going to print that out, that string. And then we'll reference the SQL%ROWCOUNT again in order to actually count the rows affected.

There we are. And next, we're asked to go ahead and execute a select statement to check whether the new department is inserted. You can terminate the PL/SQL block with a slash and include the select statement in the script. So at the bottom of my PL/SQL code-- let me just get this wrapped around so you can see what I'm typing here.

At the very bottom, I'm going to do a slash and then my select. Let's go ahead and run the whole thing. And there we are. SQL%ROWCOUNT gives 1. It tells us the maximum department_id is 270. And you notice that the answer statement did successfully insert a new row.

Now, the reason why mine is reverse as far as this print out is because of my dbms_output.put_line. I could actually move this further up. I could actually put that right there. And let me do a rollback. This little statement right there. And I'll erase this. And let me run it again so it looks just like what the book looks like. There we are. The maximum department_id is 270. SQL%ROWCOUNT gives 1. And here is our select statement right here.

So we should go ahead and save this as instructed there in step letter F as lab_05_02_soln.sql. File. Save As. There we go. Now, in number 3, it says, in step 2, you set the location_id to null. Next, we want to create a PL/SQL block that updates the location_id to 3,000 for the new department.

Notice there is a note. If you successfully completed step 2, continue on with step 3a. If not, they want you to first execute the solution script solution, solution 5 dot SQL and run task 2. We already did ours, so I'm going to go ahead and continue on with letter A. Next, we're going to start the executable block with the begin keyword, And we're going to include the update statement to set the location indeed at 3,000 for the new department.

So let's go ahead and do that. I'm going to do this in a new worksheet, by the way. Begin. Update departments. Set location_id equal to 3,000 where department_id equal to 80. And then we will end it. And then we will do a separate select. And then, finally, we will do a delete.

Let's go ahead and make this code pretty. I'll right-click and format it. First, let's go ahead and run the first statement. That completed. Next, let's select star from departments where department_id equal 280. I'll go ahead and run that. There you go. And let's go ahead and run the delete. And you see that one row is deleted.

So you can save this as instructed as lab_05_03_soln.sql. Let me go ahead and do that. File. Save. I'll do this under pls seth labs. lab_05_03_soln.sql. There we go. So that will conclude demonstrations for practice 5.
