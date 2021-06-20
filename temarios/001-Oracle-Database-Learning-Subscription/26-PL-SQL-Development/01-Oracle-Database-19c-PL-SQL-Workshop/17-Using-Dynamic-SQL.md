# 17: Using Dynamic SQL

* Using Dynamic SQL - New - 28m
* Practice 17-1: Using Native Dynamic SQL - New - 23m

## Using Dynamic SQL - New - 28m

OK, my friends, let's take a look at Lesson 17, on using dynamic SQL. We are here in the last lesson of Unit 4, Using Dynamic SQL. For the objectives, we are going to describe the execution flow of SQL . We're going to build and execute SQL dynamically by using Native Dynamic SQL, also known as NSD. We're going to identify situations when you must use the DBMS SQL package instead of Native Dynamic SQL to build and execute SQL dynamically.

OK, dynamic SQL and its features. So dynamic SQL enables you to generate and run SQL at runtime. You may write a dynamic SQL statement when you don't know the full text of the SQL statement at compile time, or if you don't know the number of variables, or if you don't know the data types of input variables. Also, I might add, certain are not allowed natively in PL/SQL without running it as dynamic SQL.

So here we have an example of Jack and Alice. Jack is saying, hey, Alice. I'm not quite good at writing codes to get my jobs done. Can you make it simpler, where I click some buttons and enter some values to get the job done, something that will look like this?

I could just enter the values and click Submit, and the data would be updated in the database. So you'll notice I am able to provide maybe the employee ID, and a new salary, and click Submit, and then the data would be updated in the database. And so that describes using dynamic SQL. Dynamic equals is when the full text of the dynamic SQL statement is unknown until runtime. Therefore, we can't check the syntax at runtime. Or rather, we have to check the syntax at runtime rather than at compile time.

We can use dynamic SQL when one of the following items is unknown or at precompile time, the text of the SQL , such as commands, and clauses, and so on, the number and data types of host variables, references to database objects, such as tables, columns, indexes, sequences, user names, and views. And we also use dynamic SQL to make your PL/SQL programs more general and flexible. So you can create a PL/SQL program that accepts different sorts of parameters to make them more flexible to run.

So let me give you an example. So what if I wanted to create-- let me create a table real quick to demo this-- create table demo. I'll have a column called ID, which is the number type, and I'll have a column called name, which is a varchar2, 25 bytes.

So what if I insert some data into the table? Let me do a commit. And what if I then wanted to create a subprogram to allow people to delete data out of not only the demo table, but maybe some other table as well? What if I created a procedure?

And I'll pass in a parameter for the name of the table. And this would be a varchar2 type. And I'll go in and I'll say, "delete from ptable," and then I'll end.

Now, that's going to cause a problem. And the reason why it's going to cause a problem is because what the database is going to try and do. It's going to try to pass this statement out, and it's going to check the syntax for validity. And it's going to try and resolve the table name according to what we've put here for our parameter.

And since we don't have a table called ptable, we're going to end up getting an error message that says, "table or view does not exist." So what we want to do is we want to avoid checking that table name at compile time. We would rather have that table name checked out runtime.

So what we're going to do in this case, we're going to put and execute immediate clause here. Execute immediate, that's what we call Native Dynamic SQL, or NDS, and it's appropriate for three out of four types of dynamic . And what I'm going to do is I'm going to concatenate the delete from syntax with the name of the table that's coming in through the parameter.

So we're going to hold off on this statement here. We're not going to check it for validity when we compile. So let me go ahead and recompile this object, and you notice this time it compiled successfully.

If I go over here to the procedure list, and let me just refresh it, and I've got my delete demo procedure. And you notice, it runs fine, or it compiled fine. There's no compilation error on that.

So let's try it. Let's see if it works. There is my demo table right now before I delete the row, and then let me go ahead and execute. And I'll pass in the table name demo. And you'll notice that it successfully executed.

So now, when we go in and select Start From Demo, you'll notice that the table is now empty. So that's what we call dynamic SQL. And that, as we were saying here, is that third point. Use dynamic SQL when one of the following items is unknown at precompile time, references to database objects, such as tables, or columns, or indexes, or sequences, or usernames, or views.

So here, they're showing you the potential flow of SQL , depending on the type of statement that they happen to be. And we point out that all SQL statements go through some or all of the following stages-- parse phase, bind phase, execute phase, fetch phase. Some stages are not relevant for all statements.

So the fetch phase happens when you have a select. We have to fetch the data. For embedded SQL statements, such as SELECT, DML, MERGE, COMMIT, SAVEPOINT, and ROLLBACK, the pass and bind phases are done at compile time. For dynamic SQL statements, all phases are performed at runtime.

So we have two different faculties for dynamic SQL. We have Native Dynamic SQL, or NDS, and that is when we use the execute immediate clause. And then we have a package called DBMS SQL. The DBMS SQL package is used in a type of dynamic SQL called type four, and that's where you're trying to write a select statement about something that you don't know anything about the structure.

You don't know how many columns or what their types are. You don't know how many parameters to provide or what their types are. And so in that situation, you would have to use the DBMS SQL package. For all the other types of dynamic sequence statements, we recommend that you use Native Dynamic SQL, because it's easier to use and performs better usually.

So that's what we're going to show you first. Native Dynamic SQL provides native support for dynamic SQL directly in the PL/SQL language, processes most dynamic SQL statements, except for type four, with the EXECUTE IMMEDIATE statement. It gives the following choices if the dynamic sequence statement is a SELECT statement that returns multiple rows. Use the EXECUTE IMMEDIATE statement with the BULK COLLECT INTO clause, and use the OPEN-FOR, FETCH, and Close statements. So we're going to show you some examples of how to use those.

Now, in using the EXECUTE IMMEDIATE statement, we're showing you a syntax slide here. You notice we have an INTO, and we have a USING. INTO is used for single row queries and specifies the variables are records into which column values are retrieved. USING is used to hold all bind arguments, and the default parameter mode is IN.

So here's an example of a procedure, called create table, and we want to provide the name of the table for one parameter, and a list of columns and their specifications, meaning column name, data type, constraints, default values-- all of those-- as the second parameter. Now, we need to do this using the EXECUTE IMMEDIATE clause. And when somebody wants to create a table, all they have to do is provide the name of the table and the list of column aspects, and it's going to allow them to go ahead and create that table. So there we are with the calling of the procedure.

We're calling create table. The first parameter is the table name. The second parameter is the list of columns with their data types and constraints, if any.

Now, here we are with a procedure called add row. We're providing the name of the table, and we have two parameters for two columns that we're inserting data into within the table that we list. So we're going to insert into the name of the table provided by the parameter.

And you notice in the values clause, we have these bind variables called placeholders. And the name isn't important. But in this case, we're using colon 1, colon 2 to represent the bind variables, and we're positionally matching those to the order that the parameters are listed. So placeholder 1 is going to get populated using the pid parameter. Placeholder 2 is going to get populated with the name of the p name variable, or parameter rather.

And then we have another example of deleting from a particular table. This one is a function that's similar to what I did with my procedure, but this one is returning how many rows are deleted from the table. And so we pass in the table name through our parameter, and then the function is returning how many rows were deleted.

Now, here is a dynamic SQL statement with a single row query. Here we have a variable that's initialized to a SELECT statement. And you notice that we're passing in a parameter through-- or and employee ID, rather, through a parameter.

So we initialize the statement with the SELECT, and then we're EXECUTING IMMEDIATE, the variable, and you notice the INTO v emprec using p emp ID. The font color maybe makes it not very visible, but we'll EXECUTE IMMEDIATE v statement into v emprec using p emp ID. And so that's where we're tying the parameter, p emp ID to the p emp ID bind variable. And then we're going to go ahead and use that get emp function, and we're going to go ahead and print out what that person's name is.

Now, you can't really store an anonymous block in the database, because an anonymous block does not have a name to call it by to invoke it. So here, we're creating a function that has an anonymous block initialized to a variable inside of it. And you notice, we're executing immediate the v PL/SQL variable using for the in value p emp ID, and out is going to the variable called v result. And then we're going to return v result. So what's going to happen is, we're going to pass in annual salary with the employee ID, and it's going to return that person's salary multiplied by 12.

Now, we can also use the BULK COLLECT INTO clause. We haven't really talked about that yet, but coming up in a later chapter, we're going to talk about the BULK COLLECT INTO clause. But just notice that we do have support for the BULK COLLECT INTO clause with Native Dynamic SQL.

So it is used instead of INTO in SQL statements retrieving data into PL/SQL blocks. The variable FOLLOW BY BULK COLLECT INTO should be capable of holding multiple rows, such as a collection or a cursor. This is going to improve the performance of the PL/SQL block with SQL statements receiving huge volumes of data.

The presence of BULK COLLECT INTO in the SELECT statement returns the results from the SQL to the PL/SQL engine in batches instead of one row at a time. So in the previous example, we were doing a single row query using dynamic SQL, where we're returning a single value into a variable. What we're talking about here is bringing back more than one row at a time, which is going to return the results from SQL in batches instead of one at a time.

So the OPEN-FOR clause is used to associate a cursor variable with a query. It allocates database resources to process the query. It identifies the result set based on the query. If the query has a FOR UPDATE clause, which, again, is a reminder that locks the rows that are part of the cursor, then the OPEN-FOR statement locks the rows of the result set.

So here is an example. We have it looks like four index tables. We have an open, where we're opening the emp CV, which is a ref cursor for select employee ID, last name, from employees. We're going to fetch the rows from the emp CV cursor variable. We're going to bulk collect that into the emp IDs and e names arrays.

Then we're going to close the ref cursor. And then we're going to print out how many are in the arrays. And you notice, 107 are in the collection.

We don't really talk about ref cursors in this class. It is in your appendix chapters, by the way, but let me tell you what a ref cursor is. A ref cursor is a cursor that can be open and shut for any SELECT statement.

Usually when you define an explicit cursor, it is bound to a specific table or to a specific SELECT statement. So cursor emp cursor is SELECT start from employees. So emp cursor would be the entire data set of the employees table.

But what if I wanted to be able to close that cursor and open it up with the different data set from a whole different table or maybe a different set of columns from the same table? Rather than all columns, I want to close it and open it for 2 columns instead of 11. So that's what a ref cursor gives you the ability to do. So I don't have to define more than one cursor in order to be able to work with different data sets. So if you're curious about that concept, take a look at your appendix chapter, and there is one on ref cursors.

So we have four different types of methods for dynamic SQL. Method four is where we need to use the DBMS SQL package. Method four is where we have a query with an unknown number of select list items or input host variables. Method one is a non-query without host variables. So a non-query, so it's not a select, but it might be an update or an insert, something like that. And we're going to use the EXECUTE IMMEDIATE without the USING and INTO clauses for that one.

Method number 2 is also a non-query with a known number of input host variables. We can use EXECUTE IMMEDIATE with the USING clause for that one. Method three is a query returning a single row, and that's similar to the example that we showed you earlier, where we have the EXECUTE IMMEDIATE clause with the USING and INTO clauses. And then method three is where we're returning multiple rows, and that's where we use the BULK COLLECT and OPEN-FOR clauses that we showed you in the previous example.

And then finally, method four, that's the situation where you would use the DBMS SQL package. So we're going to show you an example of using DBMS SQL. Jack is saying, hey, Alice, can you create a simple interface where I can just enter the table name, column names, and output I want to see in the user interface, and I get the job done on submission to the server? She says, yes, I'll be able to do that.

For the audience that is wondering how we write the query, the DBMS SQL package is the answer. So Alice is saying, any situation of uncertainty where you aren't sure about the table on which the query would execute, or about the number of columns you would retrieve from the table, or about the output, that's exactly what we call method four. So you can use the procedures provided by the DBMS SQL package.

You first construct the query based on user input with respect to the tables, columns, and so on, and then you execute the query. And the DBMS SQL package provides various procedures for the purpose. So DBMS SQL is used to write dynamic SQL in stored procedures and to parse DDL statements. You have to use that when you have an unknown number of input or output variables, also known as method four.

As I was saying earlier, in most cases, the EXECUTE IMMEDIATE clause or NDS is easier to use and performs better than DBMS SQL except when dealing with method four. So, as an example, you have to use the DBMS SQL package if you don't know the select list at compile time, if you don't know how many columns a SELECT statement will return, or what their data types will be. So we have a number of different subprograms in the DBMS SQL package.

Here, we have open cursor, parse, bind variable or bind array. Depending on the type of statement that you're using it with, you may or may not have to use all of those subprograms. So here is an example similar to when we use the EXECUTE IMMEDIATE clause for. We're creating the function to delete all the rows out of a table. We're passing and a table name.

Now, this is not type four, I want to point out, because this is not doing a select. This is actually doing a delete. But we're showing you that this one is technically more difficult than the version that we used with NDS to delete the rows out of my table. So let me remind you what mine look like. Execute immediate, delete from-- whatever the name of the table is.

Let me remind you what the book looks like. Passing in the table name, we have a variable called v cur ID. We have a variable called v rows delete.

We're initializing v cur ID to opening of the cursor, and then we use the parse procedure to pass in the v cur ID variable, deleting from the name of the table that we pass into the parameter, and we're using the DBMS SQL dot native subprogram with that. The v rows, del variable, is going to get initialized to the execution of the v cur ID. And then we're going to return however many rows are deleted. So you notice that this has a few more steps in it than the Native Dynamic SQL version that I showed you.

Here's another one where we're passing in a name at a table to insert a row, and we have three parameters to provide an ID, a name, and a region. And then we're initializing the V statement variable to an INSERT statement. We are passing in some bind variables. And then what we have to do is we have to associate those bind variables with the input parameters that we're supplying.

So the cid is going to be bound to the pid parameter. The c name is going to be bound to the p name parameter. And our idea is going to be bound to the p region parameter.

And then we'll go ahead and execute the v cur ID. And then we'll close the cursor, and then it'll tell us how many rows were added. So that brings us to our quiz.

The full text of the dynamic SQL statement might be unknown until runtime. Therefore, its syntax is checked at runtime rather than at compile time. And that is true.

So that is going to do it for the summary for this lesson. You should have learned about the execution flow of SQL statements, how to build and execute SQL statements dynamically by using NDS, and you should be able to identify situations when you have to use the DBMS SQL package instead of NDS to build and execute SQL statements dynamically. So we're going to give you the opportunity to practice using dynamic SQL in Practice 17.

You're going to create a package that uses NDS to create or drop a table and to populate, modify, and delete rows from a table. And then you're going to create a package that compiles the PL/SQL code in your schema. Well, that is going to do it for the demonstrations for Lesson 17.

## Practice 17-1: Using Native Dynamic SQL - New - 23m

I will now demonstrate practices for Lesson 17 using dynamic SQL. In this practice, you are going to create a package that uses native dynamic SQL to create or drop a table, and to populate, modify, and delete rows from the table. In addition, you create a package that compiles the PL/SQL code in your schema-- either all the PL/SQL code or only code that has an invalid status in the user objects table.

Before starting this practice, it is recommended that you run the cleanup_17.sql script. So I am going to start with the solutions which are on about page 5. And in this practice, we're going to create a package that uses native dynamic SQL.

We're going to create or drop a table, and populate, modify, and delete rows from the table using NDS. In addition, you create a package that compiles the PL/SQL code in your schema, and that's going to be either all the PL/SQL code or only code that has an invalid status in the user objects table. So we're asked to create a package called table package that uses native dynamic SQL to create or drop a table, and to populate, modify, and delete rows from the table. And this program should manage optional default parameters with null values.

So let's go ahead and create a package specification by using the signatures that you see on the screen for those five procedures. So that's going to be easy enough. I'll go ahead and copy those and put those into a new worksheet.

Nothing that we haven't done already. We have a package specification, we have a procedure called make, we have a procedure called add row, we have a procedure called update row, a procedure to delete row, and a procedure to remove-- or a procedure called remove. Now I'll go ahead and compile that.

And then next, we are going to create the package body that accepts the parameters and dynamically constructs the appropriate SQL statements that are executed using native dynamic SQL except for the remove procedure. The procedure should be written using DBMS_SQL package instead. So what we can do-- let's go ahead and erase the specification. I am going to refresh my packages.

And you'll notice that I have my package called table package. Next, what I want to do is go ahead and create the body. Now in my case, I'm going to go ahead and copy it out of the book. You've already created packages before, so what I'm going to do is just kind of focus on the new dynamic SQL components to show you what those are all about.

And there we go. So I have a procedure called execute. We're going to execute immediate p statement, which is coming in through the parameter.

We have a procedure called make where we're going to pass in a table name and column specs, and that's going to allow us to create a table using native dynamic SQL. And then we're going to create a procedure called add row which is going to allow us to insert into a table name provided through a parameter. And then we have a procedure called update row which is going to let us use dynamic SQL in order to update a table name passed in as a parameter.

And then you'll notice that we're checking to see if conditions exist. If we don't have any conditions for our parameter, then we're going to go ahead and allow it to be null. However, if we do supply values for the conditions, then we're going to use that to add on a where condition.

And then we have another procedure called delete row, which is allowing us to pass in a delete statement from a table provided through the parameters. And finally, a procedure called remove. Now this one is using the DBMS_SQL package.

And we're using the DBMS_SQL package to open the cursor to parse the statement, passing in the cur_id variable value, the statement which, in this case, is a drop table statement, and using the DBMS_SQL.NATIVE definition here. Now what this is going to do is to parse. The parse executes the DDL statement. And notice that no execute is going to be required for that one.

And let's go ahead and compile that package body. Oops, looks like I just highlighted just that part of my code by the way. So let me clear my error code and go ahead and recompile that. So page number 8, we are asked to go ahead and execute the make package.

And we're going to create a table called my contacts. And we have a list of parameter-- or a list of columns listed as well. Execute package name.make. My contacts is the name of the table.

And then it looks like we will have a column called ID and a column called name. And I'm just going to make sure that that's not wrapped around to avoid having an error. And let's go see if we created the table.

So there is the table called my contacts, and here are the two columns that were created based on our input parameters. Next, we're going to describe the table. You can do that as well by clicking on the table so you can see what the structure of that table looks like, like they're doing in step letter D.

And then in step letter E, we're going to go ahead and execute the add row package procedure to add some new rows. It looks like we're going to add four new rows of data. So I'll go ahead and just copy this out of the book. It looks simple enough.

We're going to add a row for Lauren, a row for Nancy, a row for Sunitha, and a row for Valli. And let's just double check the table to make sure we have the four rows added. It looks like we do.

We'll continue onto the next page. We're going to go ahead and query the my contacts table contents to verify the addition. So let's do that. We are going to execute table package dot delete rows.

And let's do the my contacts, and ID equal 3. So they want you to run a select statement first, and then we want you to delete from the my contacts table where the ID equals 3.

Select star from my contacts. Looks like we have an ID of 3, so it looks like this is the row that's going to get deleted. And let's go ahead and run it. Now this one gave us an error. And it's telling us delete rows must be defined.

So let's go back in and double-check the spelling of my sub-program. It looks like it's just delete row. We can verify that by expanding my specification. So it's just called delete row, so it looks like I mistyped the name.

[LAUGHS]

So let's try that again. And you notice that we are deleting from the my contacts table where ID equal 3. Next, we will go ahead and execute the update row procedure. And we're going to update Nancy Greenburg.

Now let's go in and see what ID equal to before we do that. It's just Nancy for ID number 2 currently. So let's go ahead and invoke the update row sub-program. And I'll tell you what-- I wanted to make sure I spelled that correctly.

So what's going to happen with line four is we're going to update the my context table, and set the name equal to Nancy Greenberg. So now when I query the my context table, instead of just Nancy, you'll see that we have Nancy Greenberg. Onto the next page.

In step letter J, we're going to drop the table by using the remove procedure. So let's go ahead and do that one. And let me just drop to a new line in my SQL developer session here. Execute table package dot remove. And we'll pass in the name of our table here, my contacts.

And that successfully completed. Let's go in and describe the table my contacts. And you notice that it tells us it does not exist, so our remove procedure has successfully executed. Continuing onto page 12, we want to create a compile_pkg package that compiles the PL/SQL code in your schema.

So let's do that. And this is going to be in our my connection schema. So this one is going to have a simple specification. I'll show you what it looks like here.

We have a procedure called make, and let's go ahead and compile that. Now in step letter B, we're going to create a package body. We're going to have an execute procedure which is used in the table package procedure in step one of the practice.

We're going to have a private function named get_type to determine the PL/SQL object type from the data dictionary. It's going to return the type name. We're going to use package for a package with a body if the object exists. Otherwise, it should return a null.

In the where clause condition, add the condition to ensure that only one row is returned if the name represents a package which may also have a package body. In this case, you can only compile the complete package, but not the specification or body as separate components. So that's going to be row num equal 1.

Then we want to create the make procedure by using the following information. The make procedure accepts one argument called name which represents the object name. The make procedure should call the get_type function.

If the object exists, make dynamically compiles it with an alter statement. So let's go ahead and take a look at this package body. I'll go ahead and copy that from the book.

This one is going to be a rather long package. I will open up a new worksheet. And then we will continue with the rest of the code on the next page. So let's take a look at what's happening here.

Now by the way, when I pasted this in my multi-line comments-- or my single line comments did not successfully paste in there. So I'm just going to go ahead and hand-type those in the code. And then I'll remove those orphaned comments from up above.

So let's take a look at the logic. Create or replace package body compile_pkg is. We have a procedure called execute, we have a parameter called p statement, and we're going to go ahead and print out what the statement is. And we're going to execute immediate the statement.

We have a function called get_type. We're going to pass in a name. We're going to return a VARCHAR2 type. And then we have a variable that is called v_proc_type.

Now notice in the comments, the row num equal 1 is added to the condition to ensure that only one row is returned if the name represents a package, which may also have a package body. In this case, we can only compile the complete package, but not the specification or body as separate components. So we're going to select object_type into the v_proc_type from user_objects where the object name equals the name coming in through the parameter, and the row num equal 1.

And we're going to return the proc type. And then the exception when no data found, then return a null. And then we have the procedure called make, and this is where we come in and actually create the alter statement that compiles our object.

And of course, we're passing in our proc type. Alter package, name of the package, compile for instance. And then we have our raised application error to handle the situation where somebody put in the name of a sub-program that doesn't exist. So let's go ahead and compile this one.

Oops, I did it again. I accidentally highlighted just one part of the code.

Let me go ahead and compile the whole package body. So next, what we're going to do is we are going to use the compile_pkg.make procedure to compile the employee report, the emp package package, and a non-existent object called emp_data. Let's go ahead and try all three of those.

And we'll do this in a new worksheet so we can show you the code a little better there. Let's try the first one. Successfully completed. The second one, it's going to compile.

And the third one actually is going to error out because emp_data is not a package that exists. So you see it's working successfully. OK, my friends, that is going to do it for the demonstrations for practice 15, or rather practice 17. I was reading the page number.

[LAUGHS]

So that's going to do it for the practices for lesson 17.
