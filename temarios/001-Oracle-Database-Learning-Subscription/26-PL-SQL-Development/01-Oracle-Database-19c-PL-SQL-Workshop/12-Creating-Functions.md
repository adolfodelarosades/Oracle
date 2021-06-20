# 12: Creating Functions

* Creating Functions - New - 25m
* Practice 12-1: Creating Functions - New - 23m

## Creating Functions - New - 25m

OK, my friends. Let's take a look now at Lesson 12, Creating Functions. We are here in Unit 4 working with subprograms, Lesson 12, Creating Functions. Now after completing this lesson, you should be able to differentiate between a procedure and a function, describe the use of functions, create stored functions, invoke a function, remove a function, and explain the basic functionality of the SQL Developer debugger.

Now the SQL Developer debugger, we actually don't do any labs on that one in this particular chapter. But, in the next chapter, we have a dedicated chapter devoted to the SQL Developer debugger. So in order to create and invoke functions-- what are functions? Functions are like procedures in that they are named PL/SQL blocks.

They can accept input as parameters. They process the input and return a value. And that's one of the requirements of a function that's different than a procedure. Functions always have to return a value. Functions are stored as a database object. It also allows us to modularize our applications.

And the way that we invoke functions is slightly different than procedures. We can invoke functions as part of an expression. So the syntax for a function has to have at least one return statement. Now we have to have a return type where we describe the type of the data that's going to be returned, whether that's character, or number, or a Boolean type, or other types that are available. And, also, they have to have at least one return statement that defines the value that's going to be returned.

So here we have Jack and Alice. Jack is saying, hey, I could update the database with the promotions and salary raise. Thanks, Alice. Now I need your help in calculating the tax applicable for each employee. And Alice says, sure, tell me what the formula is for the calculation.

And Jack says, hey, I'm going to email you the formula. It's a bit complicated. The code you write should help me in arriving at a value based on input. It should be good to use in mathematical formulas. I may have to calculate taxes in many places. So Alice has got it.

So we want to explore the differences between procedures and functions. Procedures, as I mentioned earlier, are executed in a little bit differently than functions. Procedures are executed as a PL/SQL statement, where functions are invoked as part of an expression. Procedures do not have a return clause in the header. Functions have to have a return clause in the header. And that is what describes the type of data that we're going to return.

Procedures can pass values by using output parameters, but functions have to return a single value. Procedures can contain a return statement without a value. And what happens if you have a return statement in the executable section of a procedure, what it's going to do is it's going to return control back to the calling environment. Functions, on the other hand, have to have at least one return statement where we define what value is going to be returned.

Procedures cannot be invoked from SQL expressions. However, functions can be invoked from SQL expressions, including SQL expressions like a select statement, as long as they follow the rules. So we're going to talk about that a little bit more here in a few pages. So similar need to procedures, we create functions. We compile them to see if they have warnings or errors. If we don't have warnings or errors, we can go ahead and execute those.

However, if the functions do contain warnings or errors then, of course, we would have to correct the errors, or make note of the warnings to see if we want to go in and change the logic to take into account the warning that we're getting. So, in order to invoke a stored function, I think I'm going to show you this live. Let me go in and show you some examples. Excuse me. OK.

So we have a function called get_sal. Here I have my return type. Down here I have my return value. So the type that I'm going to return is going to be a number. And it looks like it's going to be a salary that I actually return. So I'm going to create the function. And we can invoke the function either as an input parameter to another subprogram.

So, for instance, the PUT_LINE procedure has an input parameter. And we're capturing the output of the function for the input of the PUT_LINE procedure. And it's going to allow us to print out what the value is of the salary, which we see as 24,000. OK. Or we can pass that value to a bind variable.

So we're going to create the bind variable right here. And then we're going to assign the return value from the function to the bind variable. And then we can go ahead and print the value out using the Print command. And we see that that bind variable has been assigned the value 24,000. Or, we can use that in a another subprogram or anonymous block.

So here we have the sal variable. We're initializing the sal variable with the return of the function. And then we're going to print out what that initialized value is for the variable. And, again, we see that we get 24,000 back for that. OK. Or, subject to restrictions, we can use that function inside of a SELECT statement.

So you're going to notice when I go in and run this in a SELECT statement that I'm going to get back the salaries for all of the employees in the IT Programming department, which is that Department 60, by the way. So, lots of different ways to invoke the functions.

So that's what they're showing us here, invoking a stored function by passing that to another parameter-- or passing that into another parameter, or getting the results using bind variables, also known as Host variables, or returning the value into a local variable, or using it in a SQL statement. And as I mentioned, that's subject to restrictions. You know, you've got to make sure that the SQL engine understands the data type that's going to be returned.

Now, we can also use the function Wizard in SQL Developer in order to create the function. Right-click the Function category, select New Function from the pop up our wizard is going to pop up, and allow us to supply all of the parameters to create the function. And then, that code is going to get returned automatically into a compilation window. And all we have to do is go in and edit the executable section from begin and end, where it's got a placeholder that says return null for that location. OK.

Functions in SQL expressions. So, sometimes, you are going to want to be a little cautious of using a function in a SQL expression. Not only can we use functions and selects, but, bear in mind, we can also use functions with other DML keywords, like inserts, updates, and deletes. So here we're showing you, as I showed you, that we can use that tax function here inside of a SELECT statement. And we have some recommendations here on where those can be used.

So user defined functions act like built-in single row functions and can be used in the select list or clause of a query, in conditional expressions of the where and having clauses, in the order by and group by clauses of a query, in the values clause of an insert statement, in the set clause of an update statement.

But, as I was saying, you know, we do have some restrictions when calling functions from SQL expressions. Here are some of the rules. User defined functions that are callable from SQL expressions must be stored in the database. They can only accept in mode parameters with valid SQL data types and PL/SQL specific data types. And they can only return valid SQL data types and PL/SQL-specific data types.

Now when calling functions in SQL statements, you have to be the owner of the function. You have to have the execute privilege, and enable parallel-- enable option in function specifications. Now as I was saying, sometimes we have some other things we have to consider. A subprogram may have side effects when it performs one of the following operations-- if it updates the zone out or in out parameter, if it modifies a global variable, if it modifies that public variable in a package, if it updates a database table, if it modifies the database.

So we're going to show you what a side effect is here. So on this page, you're actually creating a function called dml_call_sql, or dml_call_sql. And you'll notice that the function is actually going to insert data into the employees table. And when it's done inserting data into the employees table, it's going to return the parameter input plus $100.

Now, if we call that function from an UPDATE statement, what you're trying to do is you're trying to do an insert through the function at the same time you're trying to do an update in the employees table. So right here is my function that's doing the insert. And I'm calling that from a statement that has an update. And we're going to get an error message in this case. It's going to say, hey, the employees table is mutating the trigger. A function may not see it.

So let me go ahead and demonstrate this one for you, so you can see what this looks like. So I am going to create that function, dml_call_sql. And then what I'm going to do is I'm going to call that from the UPDATE statement. And I'm going to be doing an insert and an update at the same time, and is going to tell me, you know, hey, it's mutating. The trigger function may not see it. So, you do want to be cautious when creating functions that you don't violate one of these guidelines.

So functions called from a SELECT statement cannot contain DML statements. Remember DML stands for Data Manipulation Language, so we can't have inserts, updates, deletes, and merges. Functions called from an UPDATE or DELETE statement on a table cannot query or contain DML on the same table. And SQL statements cannot end transactions with a commit or rollback. Calls to any subprograms that break these restrictions are not allowed in the function.

Now as far as passing parameters to functions, functions accept named parameters, positional parameters, and mixed parameters. Now that wasn't always the case. Previously, in prior versions of Oracle, for instance, back in Version 10g, you could only call a function by using positional notation for a parameter passing. So, you know, in more recent releases, such as Version 12c and 19c, we are now able to accept named parameters, positional parameters, as well as mixed parameters.

And let's see what is Alice saying? Alice is saying, let us see a variant of the tax function. This new function would accept the employee ID and non-taxable allowances as input parameters, and calculate the tax application, or the tax applicable rather, for the employee. The non-taxable allowances per month has to be deducted from the salary, and also has to be calculated on the remaining amount. OK.

So here we have some examples of the ability for doing both named and mixed notation from SQL. We have two parameters. It looks like the second one has a default of 500. So in the first example, where we're calling tax new with just the value of 100, positionally that's going to map to the p_id parameter.

In the next example, we've got positional notation for both parameters. In the third example, we've got named notation for both parameters. In the final one, we have named notation for just the first parameter, and the second parameter is going to get the default of 500. So all of those would execute successfully. And, you know, that hasn't always been the case.

Similar to procedures, if you wanted to look at the source code, you can look in the data dictionary view called User Source. In this case, we're selecting the text column from User Source where the type equal function and order by line. Now, you'll also probably want to filter it on the name of the function. So let me demonstrate what I'm talking about there.

I'm going to go ahead and create the tax function here. And then what I'll do is go and look at user_source. Now if I just go in and select text from user_source, where the type=FUNCTION ordering by the line, you notice I get FUNCTION job_id-- or sorry-- FUNCTION get_job, FUNCTION get_sal, FUNCTION tax_new. OK. I can't really tell what code goes to what function.

So what I would want to do is I would come in and I would say, and name=tax, for instance. And look, I'll tell you what, I got an error. Let me try that again. And I guess it's called tax_new, sorry about that. Tax_new-- helps if I have the right function name. There you go.

So you'll notice that now I'm seeing the header part of my function, the return type, the variable, here is the executable section. OK. And so, you'll notice that that is actually the user_source. OK. All right. So, you know, just be careful when you look at user_source, make sure that you're only looking at the source code for your particular subprogram. If you just do the type of function like we're showing you here on the screen, then, of course, you're not going to be able to really see the source code in a logical arrangement. All right.

We can also click on the function in SQL Developer, and that will also allow us to see the syntax for what created the function. And we can all also go in and edit that function, and recompile it, if necessary, assuming that we have the permissions to do that.

And then, similar to dropping other objects in the database in order to remove stored functions, you can use the DROP statement, DROP function, whatever the name of the function is, or you can right-click the function in SQL Developer, and select DROP from the menu, and click Apply on the pop up. And, you know, those are the ways that you can drop those functions. All right.

Which of the following statements are true about PL/SQL stored functions? Can be invoked as part of an expression? Must contain a return clause in the header? Must return a single value? Must contain at least one return statement? Does not contain a return clause in the header? Letter E, does not contain a return clause in the header, we know that's false, because we have to tell it what type is going to be returned.

It must contain at least one RETURN statement. That's true. OK. That's the value that is going to be returned. So letter D is true. Letter E is false. And if letter E is false, that means letter B must be true. Must contain a return clause in the header, that is true. Must return a single value, that is true.

And then letter A can be invoked as part of an expression. That kind of sounds optional. They need to be invoked as part of an expression. Right. We have to either initialize those into another variable, or provide them as input to another subprogram through input parameter. So I would say, what is true, I would say letter B is true, letter C is true, and letter D is true. OK.

So in this lesson, you should have learned how to differentiate between a procedure and a function. You should have learned how to describe the uses of functions, how to create stored functions, how to invoke a function, how to remove a function. And I didn't really show you the basic functionality of the SQL Developer debugger, so let me show you a little information on that. And then, in the next chapter, we'll go in and have you guys do some hands-on with the debugger.

But if I go in to my FUNCTION, and let me refresh my FUNCTION list here. Here's my tax_new function. And it looks like, by the way, it's got a bunch of other lines of code in there that I don't need. It's causing it to compile in an error.

I think I accidentally hit the wrong button on my worksheet. I ran it as a script, rather than as a statement. And it compiled my tax_new function with all of that other code that was on the same worksheet. So let me just recompile that. OK.

Well, this is the debugger right here. And I wanted to point out that under the Compile button, we actually have a Compile for Debug. And what this allows you to do is it allows you to run your code and investigate what's happening in your code. So for instance, if you have some records that are getting populated, you can see the values as they get populated into a record.

If you have a loop happening, you can go in and see the loop iterate as it loops one time, two times, three times, four times. And so, you know, we'll give you some hands-on on using that debugger. But, in the book, they did have a placeholder in there for showing you that, you know, I was going to show you that we have a debugger. So I've got to do that. So I thought I'd better do that before we wrap up the chapter. And next chapter, we'll talk more about the debugger. OK.

So, we're going to have you do a practice on functions. You're going to create stored functions to query a database table and return specific values. You're going to create stored functions that are going to be used in a SQL statement.

You're going to create stored functions to insert a new row with specified parameter values into a database table, create stored functions using default parameter values, and invoke a stored function from a SQL statement and from a stored procedure. All right. So that is going to do it for Lesson 12.

## Practice 12-1: Creating Functions - New - 23m

I will now demonstrate practices for Lesson 12, Creating Functions. In our overview, we notice that we will create, compile, and use the following. We will create a function called get job to return a job title, a function called get annual comp to return the annual salary computed from an employee's monthly salary and commission passed as parameters, and a procedure called add employee to insert a new employee into the employees table. Notice, before starting this practice, you should execute the cleanup_12.SQL script.

Now, I'm going to go ahead and start with the solutions. And what we're going to do is create n invoke, the get job function, to return a job title. Let me open up a new worksheet here. And we're going to create and compile a function called get job to return a job title.

Now, notice there is this solution3.SQL script, just in case you want to go ahead and run it from the solution. Otherwise, you can go ahead and type it yourself. Or if you happen to have the activity guide open on the student desktop, you could actually select the code from the guide, and copy it, and paste that into your SQL developer connection-- whatever you prefer.

So I went ahead and copied the definition into my SQL workshop. Now, let's take a look at the code. Create or replace function get job.

We have p job ID in mode, jobs.jobIDpercenttype. We're returning the jobs.IDpercent-- or jobs.jobtitlepercenttype. And then we have a variable called v title, which is of the jobs.jobtitlepercenttype.

We're going to select the job title into the variable where the job ID equals the parameter provided through p job ID. We're going to return the v title variable as the return value from the function. So let's go ahead and compile, and you notice that the function get job was compiled successfully.

Now notice, if you encounter an access control ACL error while executing this step, there are some commands that you may need to follow in order to be able to execute that step. You notice I didn't have any troubles myself, so I'm going to go ahead and continue on to the next step. Letter A, create a varchar2 host variable called b title. Allow a length of 35 characters, invoke the function with the job ID of SA wrap to return to value in the host variable, and then print the host variable to view the results.

I'm going to go ahead and just double-check that my function is compiled over here with no errors. I'm going to clear my connection, and then I'll go ahead and create my variable, variable b title. And that's going to be varchar2 with the size of 35.

And then I'm going to execute b title with a colon in front of it. And I'll invoke my function get job, and I'll pass in SA_REP as the value. Be careful about the case sensitivity of that parameter input. SA_REP should be uppercase.

And then let's go ahead and print the value held in our bind variable. Let's go ahead and run it, all three lines. And you notice that our b title says, "sales representative."

Next, we're asked to create a function called get annual comp to return the annual salary computed from an employee's monthly salary and commission passed as parameters. I am going to go ahead and open up a new worksheet for that. And the get annual comp function should accept parameter values for the monthly salary and commission. Either or both values passed can be null, but the function should still return a non-null annual salary.

And we're asked to use the formula listed on the page in order to calculate the annual salary. So I think what we'll probably have to worry about is some people don't make commissions, and so we'll have to worry about nulls in the commission column. So we'll most likely use the NVL function for this.

Create or replace function, get annual comp. We have a parameter called p sal, which is an employees.salarypercenttype, and one called p com, which is an employees.commissionpercenttype. And the return type for this function is going to be a number.

We're going to do calculations with numbers. So we want to return a number. And then we're going to use that formula that they gave us, but we're also going to use the NVL function.

In the event that somebody doesn't have a salary or in the event that somebody doesn't have a commission, we're going to use a 0 instead as a calculation. So we'll do an NVL function multiplied by whatever comes in through the p sal parameter. And if it's a null, we're going to use 0 instead. And we're going to multiply that by 12. And then we're going to add the commission calculation.

Again, if somebody doesn't make a commission, or if the p com parameter is null, we're going to treat that as a 0 instead. And then we're going to multiply that by the p sal times 12. And then what I'm going to do is just make sure that I have enough parentheses. And I tell you what, let me just wrap that around.

So there's those parens. This is the paren the matches that. We need-- I've get two there. I've got two there.

And this one here goes to there. OK, it looks like I have enough. And then let's go ahead and end it.

I am going to right-click and format this. Let's go ahead and compile it. And it looks like we do have an extra paren some place-- line four character position 81. I'll to you what, let's open that up in the function category so we can see it a little better.

And let's see. I think I just forgot my return keyword. I was so focused on the computation that I forgot my return keyword.

So this is the return type. This is the return value. And let's go ahead and recompile that, look at my message.

OK, this time it compiled successfully, no errors. I'm going to go ahead and clear out my messages log again. Let me erase my worksheet.

Now, in step letter B, we're going to use the function in a SELECT statement against the employees table for employees in department 30. So for this one, I'm just going to copy the code out of the book. We're just running a SELECT. And the only difference on this one is we're passing in the function that we just created, putting in two parameters.

Salary is going to provide the first parameter, commission percent is going to provide the second parameter. And when we run it, our new function is being used in order to calculate the annual compensation. So it looks like that one works successfully.

So on to number 3. We are going to create a procedure called ad employee that inserts a new employee into the employees table. The procedure should call a valid dept ID function to check whether the department ID specified for the new employee exists in the departments table.

So we're going to create a function that's a Boolean function called valid dept that's going to validate whatever department ID comes into our code to see if that department exists. So let's go ahead and do that. Create a replace function valid dept.

We're going to have a parameter called p dept ID. That one's going to be an in mode, and it's going to be the departments.departmentIDpercenttype. We're going to return a Boolean type.

We have a variable called v dummy, which is a PLS integer type. And our executable section starts with the word "begin." And basically, we want this to run. So we're going to ensure that the SELECT statement runs and returns a true if the provided department ID is a valid department. So as long as this selects a valid department, we're going to return a 1 into the variable called v dummy, and as a consequence of this successfully running, it's going to run line 9, which means it's going to be a true department.

And then we'll have an exception. When we don't find the rows, when no data found, then we're going to return of false instead. So if the department exists, return true. If the department doesn't exist, return a false instead. I will go ahead and compile it.

Next, I need to create the add employee procedure to add an employee to the employees table. The row should be added to the employees table if the valid dept ID function returns a true. Otherwise, alert the user with an appropriate message.

So they do give us the code for creating the procedure. So I think I'll go ahead and copy the procedure code here. You guys already know how to create a procedure, because you did that in the last chapter. And then I will copy the rest of that from the next page.

So let's just take a look at the create or replace definition. Add employee. We have a first name parameter, a last name parameter, an email parameter. We have a job ID parameter.

We have a manager ID parameter. We have a salary parameter. We have a commission percent parameter, and we have a department ID parameter.

So there are about 11 columns in this employee's table. So there we go. Now, here's where we're doing our insert.

We're basically saying, if this condition is true, if when we check the department ID in the valid dept ID function, then as long as that's true we're going to do the insert using all of those parameter values. Otherwise, if it returns a false, that's what we're doing with the ELSE clause, we're going to raise an application error, which tells us it's an invalid department ID. So let's go ahead and compile that procedure.

And I tell you what, take a look at the error message. It must not like my copy and paste out of the book, huh? [LAUGHS] P manager, ah, you know what? Missing some commas, looks like.

P job comma p manager-- and I see what happened here. It looks like some of the code got kind of wrapped around here. Let's double-check our parameters. First name, last name, email, job ID, default to sales rep, manager ID, default is manager 145, salary default is 1,000, commission 0 default, department ID. OK, so that looks like what the problem is. It looks like when I copied and pasted it something got pasted out of order.

And now, let's see, valid dept ID. It's complaining about my function. It's called valid dept is what I called my function, valid dept. There we go.

Let me look on the previous step and see what they wanted us to call that. Oh, they did want us to call it valid dept ID. So just to make sure that I am being consistent with your book, I guess I better copy that code. And I'll create a function called valid dept ID.

For some reason, I thought we were calling it valid dept. So I'll compile that code. And then what I'll end up doing is I'll end up dropping the valid dept function so we don't have a conflict.

Let's try that again, valid dept ID. Let's compile the procedure at employee. This time it compiled successfully-- no errors. It looks good.

And let's go ahead and continue on to step letter D, where we're going to invoke the add employee procedure. So let me just open up a fresh worksheet here. Execute add employee, Joe Harris, and Joe Harris is going to be the email. And then we're going to go ahead and accept some default values it looks like, because we're going to change to name notation. P dept ID is going to be set to the value of 80.

Get that so you can see what I'm doing here. Execute add employee, Joe Harris, Joe Harris for the email. And then we're naming the parameter that we want supplied with the next value, which is p dept ID. Let's go ahead and execute it.

And I'll tell you what, let's see what happens. I'll tell you what, let's do that all on one line again here. I keep trying to wrap that so you can see all of the code, but execute doesn't like you to wrap the code, as you can see.

So it's successfully completed. Let's just go in and look in the employee table and see if we have that employee called Joe Harris. There is Joe Harris.

So we have some defaults set up-- hire date, salary, commission, job ID. It looks like all of those defaulted. And there's our department 80 that got inserted. So that is going to conclude the demonstrations for Practice 12.
