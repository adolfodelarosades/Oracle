# 20: Design Considerations for the PL/SQL Code

* Design Considerations for the PL/SQL Code - New - 31m
* Practice 20-1: Using Bulk Binding and Autonomous Transactions - New - 23m

## Design Considerations for the PL/SQL Code - New - 31m

OK, my friends, let's take a look at chapter 20-- Design Considerations for the PL/SQL Code. We are here in lesson 20-- Design Considerations for the PL/SQL Code. The objectives for this chapter are, we're going to learn to write standard PL/SQL code. We're going to show you how to grant and control runtime privileges of subprograms, how to create and use autonomous transactions, how to use NOCOPY, PARALLEL_ENABLE, and DETERMINISTIC clauses for optimization, how to use result caching for optimization, and how to use bulk binding for optimization.

So we're going to start out with standardization of the code. Standardizing helps to develop programs that are consistent and promote a higher degree of code reuse. Also, helps to ease code maintenance and implement company standards across entire applications. Constants and exceptions are typically implemented by using a bodiless package, so that's going to be a packet specification without a body. And the recommendation is to start with the standardization of exception names and constant definitions.

So here, we have an example of creating a standardized error handling package that includes all named and programmer defined exceptions that we want to use in an application. So you'll notice that we've included some examples of two exceptions that we name ourself, and we bind those using the pragma exception at clause to error code 2292 and 2277. This allows us to only have to define the exception names once, and we could invoke these exception handlers in any subprogram that we want that has the visibility to the error package.

So consider writing a subprogram with common exception handling. The exception handling code should display errors based on the function's SQL code as well as SQL error message. And we should use those values for displaying the errors and also track runtime errors by using parameters in your code to identify the procedure in which the error occurred and the location, known as the line number, of the error, and the raise_application_error procedure with the appropriate error code and message as shown on the slide. Now, we also recommend standardizing constants. So here, we have another bodiless package that defines three constants that we can then use in any other subprogram.

Now, here, we have what's known as a local subprogram. We're creating a procedure called employee_sal, and down below, in the executable section, you'll notice that we're calling a function called tax. Now, this is not a standalone tax function, but is actually a tax function that we define in the declarative section of the subprogram. So you'll notice, up above, we're creating a function called tax in the declaration section of the employee_sal procedure, so that's called a local subprogram. And then when we invoke the tax function down below in the executable section, we're going to invoke the local subprogram version of the tax function.

Next up, we're going to talk about managing security for PL/SQL packages and subprograms. So we have the concept of definer's rights and invoker's rights. The default is definer's rights, so with definer's rights, the subprogram is going to execute with the access privileges of the owner of the procedure. With invoker's rights, the subprogram is going to execute with the privileges of the user who invokes the procedures. You can control access to privileges required to execute a PL/SQL subprogram by using definer's or invoker's rights.

So you'll notice, in this example, we're creating a procedure called add_dept. You'll notice that we have authid current_user, and what that's going to do is, when we grant the execute procedure on this procedure called add_dept to another user, it's going to resolve the department name of the table, the table called Departments. It's going to resolve that department's name not in this schema of the person who wrote the procedure, but it's going to look for that Departments table in the schema for the individual who invokes the add_dept procedure. So without the authid current_user clause, the Departments table would be resolved in the definer's schema, and so you'll notice that allows us to change where we're inserting our data-- which table we're inserting our data into.

So that's what we're talking about down below. When used with standalone functions, procedures, or packages, the names that are used in queries, in your DML, in your native dynamic SQL, and in your DBMS SQL package are going to be resolved in the invoker's schema. So the Departments table, as I was saying here, that's going to be resolved in the invoker's schema rather than the definer's schema. Calls to other packages, functions, and procedures are going to be resolved in the definer's schema.

So again, just to summarize, the definer is the individual who writes the procedure. The invoker is the person who executes the procedure. Also, when the invoker is a lower privilege user, then the definer can grant privileges to execute a subprogram or a PL/SQL package to the invoking user.

The SQL Grant command grants roles to PL/SQL packages and standalone subprograms. Create an invoker's rights unit and then grant roles using the invoker's rights unit. So the command that we're showing you here on the screen grants the read and execute roles to the scott.func function and the sys.package package. And you'll notice for granting read and execute to the function scott.func and package sys.package.

Next step, we have something called autonomous transactions. Autonomous transactions are independent transactions started by another [INAUDIBLE] transaction. They are defined with the pragma autonomous_transaction.

So you'll notice we have two different procedures listed on this screen. We have procedure proc1, which calls procedure proc2. Proc2 is what we call an autonomous transaction.

Now we have two components in that that makes it a autonomous transaction. We have the pragma autonomous_transaction clause, and we have a commit. The commit and the pragma autonomous_transaction are going to be required in order for this to be an autonomous transaction. So whatever happens in the autonomous_transaction is going to be committed. However, the main transaction will not be committed by the autonomous_transaction.

So I've created a demo for you. Let me go out and show you how this works. So I've created a table called Commit table. I've created a table called Non-Commit table. I've created a procedure called commitproc, which is my autonomous transaction with the commit inside of it. And I've created a procedure called noncommitproc, which inserts a row into the Non-Commit table and then invokes the autonomous transaction.

Now, normally, if this would not be-- if this commitproc procedure were not an autonomous transaction, because we have a commit inside of that block, that would normally also commit the insert here. But because this is an autonomous transaction, this commit is only committing this insert, not this insert. So let's go ahead and execute it and show you how it works.

Sorry about that. I'm going to have to recompile these two procedures. Let me get rid of my log and get rid of my two output windows down below here.

So now, if I execute my noncommitproc, you'll notice that successfully executed. Now, let's take a look at the Commit table, and you'll notice that we have 1,000 for the ID in that one. Let's take a look at the Non-Commit table. You'll notice we have a value of 1,000 in that table as well.

Now, if I do a rollback, it's only going to affect the Non-Commit table. So if I come back and take a look at my Commit table, you'll notice that it still has the 1,000 in it. But when I come down and take a look at the Non-Commit table, you'll notice that table is empty even though the commit was called here after we had inserted into the Non-Commit table. So that's how those work.

So in summary, autonomous transactions are independent of the main transaction. It suspends the calling transaction until the autonomous transactions are completed. These are not considered nested transactions, and they don't roll back if the main transaction rolls back. This enables the changes to become visible to other transactions upon a commit, and they're started and ended by individual subprograms and not by nested or anonymous PL/SQL blocks.

Similar example here in the book, if you want to study that. We have two tables. We're creating a procedure called logusage, which is the autonomous transaction.

We have a procedure called banktrans. The banktrans is inserting into the Transaction table, and then we're calling the logusage procedure. And when we execute the banktrans procedure, the logusage is always going to happen even if the insert into the Transaction table fails.

Now, let's take a look at some performance optimizations in PL/SQL blocks-- the NOCOPY clause, PARALLEL_ENABLE, RESULT_CACHE, DETERMINISTIC, and RETURNING. So the NOCOPY hint-- what that allows you to do is to pass the OUT and INOUT mode parameters by reference rather than by value. This enhances performance by reducing overhead when passing parameters.

So remember that, when you have OUT and INOUT mode parameters, it does pass data out of those parameters into another structure like a variable, and so in that case, we technically have two different copies of the data. We've got the copy in the parameter, and then we have the value that's passed to the variable. So if we add the NOCOPY hint, it's going to pass that value by reference rather than by copying it. So we're going to use up less memory as a consequence.

So let's show you how that works. I've got a get_employee procedure that has some outmode parameters. If I compile this, I'm going to get a warning that says parameter p_job may benefit from the use of the NOCOPY compiler hint. So right here, if I go ahead and take into consideration this recommendation here, when I recompile this procedure, you notice that I've solved that problem. And now I can benefit from using up less memory, and I can pass the value from the parameter into the variables that I pass this to by reference rather than by actual value.

So there are some effects of the NOCOPY hint. If the subprogram exits with an exception that is not handled, you cannot rely on the values of the actual parameters passed to a NOCOPY parameter. Any incomplete modifications are not rolled back, and the remote procedure call, also known as the RPC protocol, enables you to pass parameters only by value.

So the PL/SQL compiler can ignore the hint. We're showing you, here on this page, when we're going to ignore it. If the actual parameter is an element of an associative array; if the actual parameter is constrained, for example, a NOT NULL constraint; or if we have created a subtype on the parameter that has some sort of a scale constraint on it, like setting a specific size; and the formal parameters or records, where one or both records were declared by using percent row type or percent type, and constraints and corresponding fields in the records differ; or if it requires an implicit data type conversion; or if the subprogram is involved in an external or remote call.

Another topic-- we have the PARALLEL_ENABLE hint, and you notice it here in the definition of our function. So these can be used in functions as an optimization hint. It indicates that a function can be used in a parallelized query or parallelized DML statement.

Another performance directive is something called cross-session PL/SQL function result cache, and it works like this. Each time a result cached PL/SQL function is called with different parameter values, those parameters, as well as their results, are going to be stored in cache. Now, the function result cache is in a shared memory area called the system global area, and that's going to make it available to any session that runs your application.

Now, subsequent calls to the same function with the same parameters allow us to use the results from the cache rather than having to go in and recompute the return value. Performance and scalability are improved. This feature is used with functions that are called frequently and dependent on information that changes infrequently.

So we're showing you here where to put the RESULT_CACHE hint. Now, bear in mind, we're pulling our data from the Employees table, and that employees data may change because of transactions. So we can also include a RELIES_ON clause that points to the Employees table, and what that is going to do is, if we include the RELIES_ON clause pointing to the Employees table, when somebody makes a committed change to the data in the Employees table, it's going to invalidate the result cache. That's going to ensure that we don't pull back invalid data from the result cache, and in that situation, it will go in and recompute the return value.

So it would look like this. We would have a result cache listed. After result cache, we would have RELIES_ON. Inside parentheses, we would put the name of the table. So it would be RESULT_CACHE RELIES_ON Employees in order to do that.

And another performance directive, we can use the DETERMINISTIC clause with functions. Specify DETERMINISTIC to indicate that the function returns the same result value whenever it is called with the same values for its arguments. So think about it like this-- if I have a function that returns how many feet are in a mile, I know that, in one mile, there's 5,280 feet. I don't have to do that calculation. I have already done-- already prescribed that we have a DETERMINISTIC clause that one mile equals 5,280 feet.

So this is going to help the optimizer avoid redundant function calls. If a function was called previously with the same argument, the optimizer can elect to use the previous results. Notice that you shouldn't specify DETERMINISTIC for a function whose result depends on the state of session variables or schema objects.

Here is another performance directive. This improves performance by returning column values with the INSERT, UPDATE, and DELETE statements, and it eliminates the need for a SELECT statement. So let me show you what we're talking about here. So previously, we would have taught you to write your code like this. We would have gone out and updated the Employees table, and then we would have done a separate SELECT statement to go and grab that modified salary as well as the last name of the employee into the two different variables.

For me, this is like when I get told to go to the store. If I have to go to the store to get butter, and then if I come home, and I get told to go back to the store because we need milk, I don't want to have to make two trips to the store to get butter and milk. I would rather go in one trip and get both, and that's what we're doing up above. We're going out and updating the Employees table, and on the way back from updating the table, we are returning the last name in the salary into the variables. So I can do that all in one statement rather than having to do two statements, and that's what we're talking about with the returning clause.

Let's take a look a bulk binding-- final topic of the chapter. Now, bulk binding binds whole arrays of values in a single operation instead of using a loop to perform a FETCH, INSERT, UPDATE, and DELETE operation multiple times. Now, it kind of looks like a loop. You notice, it kind of looks like a FOR loop, but it's not a loop.

It says FORALL, not FOR. You'll also notice we don't have a loop. You'll also notice we don't have an END loop.

Now, what we need to do is we need to use collections of values. So you notice, in the values clause, we have a reference to a collection with a index, and those index values are from 1 to 1,000. So we're going to pass 1,000 values, held in a collection, to this SQL engine to get inserted into a table. The FORALL keyword instructs the PL/SQL engine to bulk bind input collections before sending them to the SQL engine. The BULK COLLECT keyword instructs the SQL engine to bulk bind output collections before returning them to the PL/SQL engine.

So I'm going to show you an example here, and this example-- now, I've already executed this. But we have two different tables-- one called Parts1, one called Parts2, and up here is where I created those two tables. And then you'll notice that I have a couple of collections here.

Now, I'm going to go ahead and do a loop to populate those collections, and then I'm going to do two different types of inserts. I'm going to do a standard FOR loop to insert into my Parts1 table, and then I'm going to print out how much time that takes. And then we're going to do a bulk bind to insert into the Parts2 table, and then we're going to get the time for that.

And when I ran this just to show you the difference in performance, the FOR loop took 4.1 seconds to insert into the Parts1 table. The FORALL, also known as the bulk bind, took 5/100 of a second in order to insert into the Parts2 table. So you see that the bulk bind was significantly faster. Let's see 5/100 of a second, so that would be-- what, 80 times quicker, it looks like, if my math is right, to do that bulk bind instead of the FOR loop.

So that's the example here that they're showing on the screen. They create the Parts1 and Parts2 tables. They create the two collections. And then they do a FOR loop, and then they do it FORALL or a bulk bind. And in their example, it looks like they're FOR loop took 0.62 and their book bind to 2/100 of a second.

Now, this is also a performance directive. What this allows you to do is to populate a collection directly rather than doing a loop to populate a collection. Back in the chapter where we taught you guys how to create records and how to create collections, we had you do a loop to populate the collection. And when we defined that type, remember that we did an index by PLS integer or index by binary integer when we defined the type? And we had to tell it how we were creating the index.

Well, with this method, we're going to select all of the rows in the Departments table for a particular location, and we're going to load those in one bulk process into the collection. And the index values are going to get populated automatically. It's going to start at 1, so the v_depts table index 1 is going to hold the first row from the Departments table.

And I think we have about-- oh, how many departments? Maybe 20 departments, so we're going to have index 1 through index 20, and we're going to be able to iterate through using that FOR loop in order to print out the department ID and department name held in that collection. So you see that's really easy to populate a collection if you go with that methodology.

Now, if you're using a cursor, the FETCH statement supports the BULK COLLECT INTO syntax as well. Open the cursor, fetch the entire data set from the cursor into the collection, so we no longer have to do a loop with the cursor to populate the collection. And here's an example where we're doing a bulk bind with a return and populating a collection all at once, so that's a really optimized statement. Going out and populating-- well, actually, going out with the bulk bind and updating the Employees table and changing people's commissions and returning the salaries into a collection called new_sals.

That brings us to our quiz. The NOCOPY hint allows the PL/SQL compiler to pass OUT and INOUT parameters by reference rather than by value. This enhances performance by reducing overhead when passing parameters. That's going to be true.

OK, my friends, so that's going to do it for my demonstrations for this chapter. Now, you should have learned how to do all of these things in this chapter-- how to create standard constants and exceptions, how to write and call local subprograms, how to control the runtime privileges of a subprogram, autonomous transactions, grant roles to PL/SQL packages and stored subprograms, use the NOCOPY hint, use PARALLEL_ENABLE, use RESULT_CACHING, use DETERMINISTIC, and use the RETURNING clause and bulk binding with DML. We are going to give you guys some hands on with practice 20. You're going to create a package that uses bulk FETCH operations, and you're going to create a local subprogram that performs an autonomous transaction to audit a business operation. So let's go ahead and have you do the practice for lesson 20, and that's going to do it for me on demoing this chapter.

## Practice 20-1: Using Bulk Binding and Autonomous Transactions - New - 23m

I will now demonstrate practices for Lesson 20-- Design Considerations for the PL/SQL Code. In the overview, we see that in this practice, you create a package that performs a bulk fetch of employees in a specified department. The data is stored in a PL/SQL table in the package.

You also provide a procedure to display the contents of the table. In addition, you create the add employee procedure that inserts new employees. The procedure uses a local autonomous subprogram to write a log record each time the add employee procedure is called, whether it is successfully adds a record or not.

Before starting this practice, execute the cleanup 20.SQLscript, which I have done. OK. I will start on these Solutions page, which is page five in my book. And, again, just to summarize, in this practice, we are going to create a package that performs a bulk fetch of employees in a specified department.

The data is stored in a PL/SQL table in the package. You also provide a procedure to display the contents of the table. In addition, you create the add employee procedure that inserts new employees. The procedure uses a local autonomous subprogram to write a log record each time the add employee procedure is called whether it successfully adds a record or not.

OK, so we're asked in step number one to update the package with a new procedure to query employees in a specified department. In the package specification, we're going to define a get employees procedure with a parameter called depth iD, which is based on the employees.departmentID column type. And we're going to define a nested PL/SQL type as a table of employees percent row type.

So let me go ahead and open up my package. And you notice that I have the specification for the emp package package. And I'll go ahead and define the type definition as instructed. There we go. Tab type is table of employees percent rotate.

A little further down, we're going to define a procedure called get employees, which has a parameter called p_dept_id, which is of the employees.departmentID% type. And I will go ahead and add that just before the admit department's procedure.

OK, now, I'll go ahead and compile my specification. And, of course, my body invalidates. So now in the package body, we're going to go ahead and add the collection called emp_table of the emp tab type. And we'll add that just after the forward declaration for valid departments.

OK. Actually, that isn't a forward declaration. We did a forward declaration on the function just below it. Ha, ha. So this is an array here. OK? All right. So next, what I'll do is go down and add the get employees procedure. Now, we are going to do this just before the init department's procedure.

OK, so this procedure is called get employees. We're passing in a p_dept_id, which is of the employees.department ID percent type. We're going to do a SELECT star BULK COLLECT into the collection from employees where the department ID equal the parameter coming in through the parameter or the value coming in through the parameter called p_dept_id.

All right, let's go ahead and compile the body and make sure that the body compiles successfully. Looks like we have successfully compiled it based on what it looks like over there in the object tree. Then in step letter C, we're asked to create a new procedure in the specification of body called show employees, which does not take any arguments.

The procedure displays the contents of the private PL/SQL table variable if any data exists. Use the print and place procedure that you created in the earlier practices. To view the results, click the Enable DBMS Output icon in the DBMS Output tab in SQL developer if you have not already done it.

OK, so let's go ahead and do that. We'll go back into the specification for emp package. And we will have the procedure called show employees just before the end of this spec. And we'll go ahead and compile it. Now, we'll go ahead and open up the body.

And at the bottom of the package body, we'll go ahead and add the procedure. And we'll add that just above the valid debt ID function, which, as you remember, we are alphabetizing our subprograms to make them easier to find. So that's why we're putting it here in this location. OK.

Now, this is a procedure called show employees. If the emp_table is not null, then we're going to go ahead and print it out. And then we're going to do a for loop. And we're going to print all of the values from the collection. So let me go ahead and compile it. And it compiles successfully.

Next, we'll go ahead and enable server output. Let me get rid of my log. OK. Now, I can go up. And I can view the DBMS Output panel right there. And what we're going to do is invoke the emp package get employees procedure for Department 30 and then invoke show employees. And then we're going to repeat that for Department 60.

So let me go ahead and demonstrate this methodology. And I missed seeing that last execute there it looks like. OK, so let's go ahead and execute get employees. And then we'll go ahead and execute show employees. And you notice that this includes all of these individuals in Department 30.

Next, we'll go ahead and execute get employees with Department 60. And then we'll go ahead and show employees for that department. And you notice that it shows us the five or so employees who work in Department 60. Now, your manager wants to keep a log whatever the add employee procedure in the package is invoked to insert a new employee into the employee's table.

So what we'll do is we'll execute this solution11.SQL script to create a log table called log newemp. This will also create a sequence called log newemp seq. So let me go in and run those pieces of code. And we'll go into the solutions. And we'll go into the solution11.SQL. And we will go ahead and run the create table log newemp.

It's on line 365 in my environment. And then we'll also create the sequence. All right, in step letter B in the emp package package body, modify the add employee procedure, which performs the actual insert operation. Add a local procedure called audit newemp as follows.

The audit newemp procedure must use an autonomous transaction to insert a log record into the log newemp table. We want to store the user, the current time, and the new employee name in the log table. We want to use log newemp sequence to set the entry ID column and make sure that you perform a command operation in the procedure with an autonomous transaction.

So let me go ahead and open up my package specification. Well, actually, my audit newemp procedure already exists. So I'm going to open up my package body. And we're going to modify the existing procedure called audit newemp. Now, these are alphabetical. So let me get to the audit newemp procedure.

And this is going to be inside of the procedure called add employee. And you have to be a little bit careful because we do have some overloaded subprograms. OK. So the local subprogram is going to go in the specification for the add employee procedure. And it's going to go just before this begin keyword.

And I'll go ahead and paste the definition of that procedure. I think what I'll do is I'll just put a line break here so that you can see that a little bit clearer. So from inside the add employee procedure, we're calling the audit newemp procedure. Or we're creating the audit newemp procedure.

OK, and then we will go ahead and compile this and just make sure that it compiles successfully. OK, I think we're good to go on that one. Let me just recompile it. And we'll take a look at the messages. And you notice it's compiled successfully.

Next, we'll modify the add employee procedure to invoke audit newemp before it performs the insert operation. OK. So in the package body, we're going to put a call to audit newemp just before the insert into the employees table.

OK, so in my case, it's on line 34. This is the same procedure where we added the audit newemp procedure, which is our autonomous transaction with our command. And then after the begin, you notice that we are adding in the audit newemp call to the local subprogram that we created up on line 21.

All right. Now, we'll compile that. And we see that that compiled successfully with no errors. And we'll go ahead and close both the package body and the package specification. I'm going to go ahead and close the solution as well and clear out the connection window.

Next, we're going to go ahead and add or execute, rather, the add employee package or add employee procedure inside of the emp package. And this should cause lines to be written to the log. So let me execute the first line. And now, this is telling us that it's an invalid salary. It looks like I have a trigger, which was not cleaned up when I ran the cleanup script.

So let me just go in and turn off that trigger. And I'm just going to refresh my triggers. OK, this is the check salary trig. So let's go ahead and disable that trigger. And I'm just going to ensure that my update and salary trigger is also disabled.

OK. So I have another trigger called saltrig. And this is going to get inserted into a salary log. So I'll go ahead and keep that one. But let's go back and re-execute the add employee package or the add employee procedure, rather. OK, that's successfully completed. And then we'll go ahead and execute the add employee procedure again with Clark Kent. And we see that that successfully completed.

And so our log tables should have two records in that. So what we'll do is select from the table called log newemp. And you notice that I have multiple records inside my log. Now, this one here, this was inserted when my salary trigger kicked in. So you notice that that is also in my log table, so because I ran an error based on that trigger executing.

Now, that's from a different chapter where we added that. And I didn't disable it. But I don't think you'll run into that problem, because you probably don't have that trigger enabled. But at any rate, we should have a row in the log table for Max Smart. And we should have a row in the log table for Clark Kent.

All right. Next, we're asked to go ahead and execute a rollback statement. OK. Then I'm going to go and select from the log newemp table again. And you'll notice that this did not affect the entries into my log table. Now, the reason why it did not is because we have populated this table by using an autonomous transaction.

And since it's an autonomous transaction, we preserve the records in the log table. Now, if we were to go and look for these employees in the employees table-- OK, let's go do that from step letter E.

OK. You'll notice that we don't have those in the employees table. And that's because, although I initially populated my employees table with the rows for Kent and Smart, because they did a roll back, those rows were removed from the employees table.

But because of our autonomous transaction, as stated in the last step, the two employee records are removed from the employees table. The two log records remain in the log table because they were inserted using that autonomous transaction, which is unaffected by the rollback performed in the main transaction. OK?

All right, my friends. So that is going to do it for the demonstrations for Practice 20.
