# 9: Handling Exceptions

* Handling Exceptions - New - 32m
* Practice 9-1: Handling Predefined Exceptions - New - 9m
* Practice 9-2: Handling Standard Oracle Server Exceptions - New - 5m

## Handling Exceptions - New - 32m

OK. Well, let's look at chapter 9 on handling exceptions. We are here in unit number 3, Working with PL/SQL Code, lesson 9, Handling Exceptions.

OK. So after completing this lesson, you should be able to do the following-- define PL/SQL exceptions, recognize unhandled exceptions, list and use different types of PL/SQL exception handlers, trap unanticipated errors, describe the effect of exception propagation in nested blocks, and finally customize PL/SQL exception messages.

OK, so what is an exception? We have two different types of exceptions. We have implicit exceptions, which can happen when Oracle recognizes that some sort of an issue has occurred. And that's what we're seeing here in this case. We are selecting the last name into the v_lname variable from employees where the first name equals John, and then trying to print out John's last name. But we happen to have more than one John.

And so because a SELECT statement is only allowed to return a single row at a time and we're trying to pull back too many Johns, we're going to get this exception that gets populated-- or the gets propagated up to us automatically. And in this case it tells us, 'exact fetch returns more than requested number of rows'.

So why is this a problem? Let me show you why this is a problem. I'm going to create a quick, little demo table. Let's see. I'll do an ID column, which is a number. I'll make that a primary key. I'll do a-- we'll do a last_name, which is a varchar2(25).

OK, so I'll create the table. And we see it over here now as a demo table. And then let me try and populate that using a PL/SQL block.

OK. Now, my column happens to have a primary key, which does not allow duplicate values. So I'm going to insert 1, and then I'm going to insert 2, and then it's going to attempt to insert a duplicated primary key. Now, the problem with exceptions is that, if you don't handle them correctly, everything you're doing in the block is going to fail.

So let me go ahead and run this, which is going to cause an error. And the error is a unique constraint error, as we expected. But two of those are valid inserts. Only one of those is not a valid insert. But still, because one of them failed, they all failed, and no rows got inserted into the table.

So if I would have done an exception handler, if I would have come in and said, exception when dup_val_on_index then do something, right? Let's print out a message to the user. Let's come in and say, 'Hey! You have a duplicate id!' Something like that, OK?

And this time when I do my executable, I do get my message, 'Hey! You have a duplicate id!' But you notice that we have what we call a "graceful termination." I have successfully handled my exception. And because I have gracefully terminated my block, the rows that were valid went into my table and only the one that errored out didn't go in there.

Now, as soon as you hit the row that caused the exception, it's going to jump down to the exception section, and it's going to do whatever you told it to do during the exception section, and then it's going to exit out of the block. So let me do a rollback to undo those two inserts. And I just want to show you what happens if I have another insert after the one that causes the error.

So this one is valid. This one is valid. This one errors. This one is valid. But what's going to happen is, as soon as it throws the error, it's going to jump down here, and it's going to bypass Gietz. So we will notice that although Gietz is a valid row, a valid insert, Gietz does not get in the table because of the way that we've actually coded this.

Now, when we get into procedures a little bit later, what I will do is I'll show you how to do this in a procedure instead. And all of the valid rows would get inserted, and only the row that wasn't valid would get omitted. So stay tuned. I'll show you how that works when we get into the procedures chapter, all right?

Now, this is a type of exception handler that we call Oracle predefined exception handler. There are 20 of these. And what predefined means is that we've already predefined the name to handle them. When duplicate value on index, when dup_val_on_index, then do something, OK?

Now, besides Oracle predefined exception handlers, we've got-- let me list out the three types on another page here. So those are the three types that we have-- predefined, non-predefined, and user-defined. Predefined and non-predefined, those are ones that Oracle is going to recognize as an error, and it's going to automatically throw out the exception at you and abruptly terminate your code.

The difference between predefined and non-predefined is the predefined, that's where the names are predefined-- NO_DATA_FOUND, DUP_VAL_ON_INDEX, ZERO_DIVIDE, TOO_MANY_ROWS, OK? All of those names are predefined. Non-predefined names are not predefined. However, the error code and message are defined. We just don't have a name to handle them by, and that's why they're called non-predefined.

And then user-defined, these are exceptions where Oracle does not recognize as an error. Oracle doesn't recognize it as an error. Updating a row that doesn't exist, Oracle is not going to throw an error at you. Trying to delete a row that doesn't exist, Oracle is not going to give you an error for that one either. So we might want to define those on our own as user-defined exceptions.

All right, so let's go back to the book. So they are going to handle this one with one of the predefined exception handlers, WHEN TOO_MANY_ROWS. So a SELECT statement that returns more than one row can be handled using the TOO_MANY_ROWS exception handler. And notice their error message-- Your select statement retrieved multiple rows. Consider using a cursor. [CHUCKLES] Cursors can handle multiple rows, a standard SELECT can't, right?

All right, so an exception is a PL/SQL error that is raised during program execution. An exception can be raised automatically by the Oracle server that's called implicitly or explicitly by the program. An exception can be handled by trapping it with a handler or by propagating it to the calling environment.

OK, so this flowchart is telling us what happens if we trap the exception or whether we have not trapped it. So an exception is raised. And is the exception trapped? Nope. Let's terminate abruptly. Whatever you are doing doesn't get processed as a consequence, and we pass the exception upward, we propagate the exception.

However, is the exception trapped? Yes. We execute the statements in the EXCEPTION section and we terminate gracefully. Any valid work that was done up to that point in time can be saved in that case.

All right, so predefined, non-predefined, user-defined, these are the different exception types. As I was mentioning, predefined and non-predefined are implicitly raised. User-defined, you have to raise them yourself.

All right. Now, it's recommended that you include more than one exception handler. You should include an exception handler for every type of exception you're expecting to get based on your code. We have one that should always be used at the end called WHEN OTHERS. And if some other error occurs besides what you have in the other exception handlers, that's going to kind of capture the ones that you haven't trapped explicitly. And you notice, in this syntax slide, it's here at the end. WHEN OTHERS should always be the last exception handler.

So the guidelines for trapping exceptions. The EXCEPTION keyword starts the exception-handling section. Several exception handlers are allowed. Only one is going to be processed before leaving the block. WHEN OTHERS is the last clause.

OK. Now, trapping non-predefined exceptions, that's what we call internally predefined exceptions. Let me show you what those are all about. I'm going to do a demonstration. Internally predefined, also known as non-predefined. Let me do this-- begin, insert into departments, values(900, 'Contracts', null, null).

Now, I'm trying to put a null into two columns. And when I run this, you'll notice that that worked successfully, OK? Let me roll it back. What if I tried to do a NULL here as well?

That's the name of the department, in that case. I'm trying to put a NULL for the name of the department. Now, that's going to cause a problem, because we have a NOT NULL constraint on the department_name column. And it says, hey, you cannot insert NULL into the department_name column in the Departments table.

Now, Oracle doesn't have a predefined exception handler called "you can't insert null" or something like that. So what we have to do is we have to create our own name to handle it by, if we want to trap it.

Now, this is our actual error code right here. So what I need to do is I need to define my own exception, my own name-- declare, e_oops. [CHUCKLES] We'll call that an exception. So that's the name I came up with, e_oops, OK?

And then I'm going to use a PRAGMA clause, And I'm going to associate the name that I came up with with the Oracle error code. So I basically defined my own name to handle it associated with this error code, right there.

So what I'm going to do now is I'm going to say, exception, when e_oops then-- do some sort of handler on it-- then 'No nulls for deptname'. So now, instead of getting this abrupt termination of my code, I get the nice, graceful termination, along with my error message, No nulls for the deptname.

So imagine that this was a parameter-based subprogram, and we're allowing people to supply values for the different parameters. And what if we don't want people to be able to put a NULL in certain places, and we want to handle the exception? [CHUCKLES] So that's what we're doing there.

Now, that's going to look pretty familiar, because we're using the same error code in the book. They call their exception e_insert_excep. It's an exception. We associate the e_insert_excep exception name with the error code. And then when that error occurs, then we're going to print out an 'INSERT OPERATION FAILED' message. So you can do that with any of the-- with any of the non-predefined error codes.

So to trap the predefined exceptions, you should reference the predefined name in the exception block. There is a list of some of the 20-- NO_DATA_FOUND, TOO_MANY_ROWS, INVALID_CURSOR, ZERO_DIVIDE, DUP_VAL_ON_INDEX. Your book, your student guide, should have a full list of those 20. If not, it's in the Oracle documentation. And then here they're showing you, WHEN NO_DATA_FOUND, then do this. WHEN TOO_MANY_ROWS, then do this. WHEN OTHERS, then do this.

Now, we also have a couple of functions that you can use for returning the code in error message. Let me show you that. Let me do my SQLCODE function, and let me run it and show you what that looks like. So there is my SQL code, OK? And then let me do my SQL error message. And let's run that and show you what that looks like. So here's the error message that's associated with that error code, 1400.

So if you wanted to capture unexpected errors, right, hey, when something unexpected happens, I want to capture those error messages into a log table, that's what the book example is showing you. Hey, when something unexpected occurs, WHEN OTHERS, let's roll it back, let's initialize SQLCODE and SQL error message returns to our variables. And then let's use those variables in an INSERT statement to populate an error table.

So we know who did it with the user-- the timestamp based on the SYSDATE. The error code is going to be whatever code came back through SQLCODE function. And the error message is going to be whatever error message was associated with the SQLERRM.

And by the way, you wouldn't be able to use these functions directly in an INSERT statement, so this is the method that I would use. I would initialize those functions to a variable, and then you can use the variable any way you want with populating an errors table like this.

All right, user-defined exceptions. So let me give you guys a demonstration on this one. Let me do a delete-- begin, delete from employees where employee_id=99.

I mentioned this earlier. We don't have anybody that's an employee 99, that they start at 100. So if I were running a process that doesn't do anything, I would probably want to know about it. Right here, it just tells me, hey, we did it. But I can't really tell how many rows were affected.

So what I'm going to do is I'm going to cause an abrupt termination. Let me show you how to do that first. If sql%notfound-- do you remember those implicit cursor attributes? If sql%notfound, then raise-- or let's do this, then pragma-- umm-- I'm thinking about another demo that I'm going to do next. Sorry about that. [CHUCKLES]

Then let's use the raise_application_procedure. I'm going to raise an error code with an error message. Raise_application, uh-- sorry, it's called raise_application_error, OK? It is a procedure. [CHUCKLES]

OK, so you notice what happened. Now I get an error report. And you notice how that looks like an Oracle error code, -20999. Nobody with that id! That's the error message that I came up with there. So Oracle allows you to use -20000 to -20999 for your own error codes. So feel free to use anything in that range.

So this caused an abrupt termination, just like the server caught it. And whatever I was doing would get rolled back. So now, what if you wanted to do something different? What if you wanted to define-- maybe you wanted to have it handle these is an exception handler instead.

Let's do that, declare, e_no_id exception. Let's do this. If sql%notfound then let's go ahead and raise e_no_id. And now that I've raised it, I can come in here and have an exception section, and I can say, when e_no_id then send a message back to the user. So this way it'll be a graceful termination, and I'll know about it, because it'll send my message upward.

Or I could, instead of that, I could use my raise_application_error procedure, -20500, 'No ID exists for that employee!' So now I'm going to get an abrupt termination in my code. And you notice how, again, it looks consistent with Oracle capturing that.

So you can either put the raise_application_error in the exception section, you can put the raise_application_error in the executable section. You don't have to raise an abrupt termination if you don't want to. You can have a graceful termination with a message. It's entirely up to you.

OK, so that's what they're going to show us in the book. Name the exception in the DECLARE section, define the condition when the exception must be raised in the executable section, and then handle the exception.

So here's where they're talking about the RAISE statement. It stops the normal execution of a PL/SQL block or subprogram and transfers control to an exception handler and explicitly raises predefined exceptions or user-defined exceptions.

So there we are. We have an e_invalid_department EXCEPTION. We're going to update the departments, set the department_name equal to testing, where the department_id equals 500. If we don't find that department 500, we're going to go ahead and raise the exception. And when that exception occurs, then we're going to get the message, 'No such department id'.

Now, what if you have a block inside of a block? We can actually define an exception in an outer block that we refer to in the inner block. That's what we're showing you here.

Here's our PRAGMA EXCEPTION_INIT in the outer block, where we're defining an exception handler for -2292, call it e_no_rows, OK? And then in the nested block, we're raising that in the event that we don't find those rows. And then we're handling that, potentially, in a different block.

OK, here's where they're talking about the raise_application_error procedure. You can use this procedure to issue user-defined error messages from stored subprograms. You can report errors to your application and avoid returning unhandled exceptions. Again, we can use these in two different places, as I showed you, in the executable section or in the exception of section. And it returns error conditions to the user that looks like Oracle did it, that is consistent with other Oracle server errors.

So we're using the RAISE_APPLICATION_ERROR against -20202, and we're using that for 'Department number doesn't exist'. And in this case, it's in the executable section. But again, you can use that in the exception section if you prefer.

OK, quiz. You can trap any error by including a corresponding handler within the exception-handling section of the PL/SQL block. That is true.

OK, you should have learned how to define PL/SQL exceptions, add an EXCEPTION section in the PL/SQL block to deal with exceptions at run time, handle different types of exceptions-- internally defined exceptions, which are non-predefined exception handlers, predefined exceptions, user-defined exceptions. You should have learned how to propagate exceptions in nested blocks and call applications.

We are going to have you practice this in lesson 9. You're going to create and invoke user-defined exceptions, and you're going to handle named Oracle Server exceptions. All right? So that's going to do it for chapter 9.

## Practice 9-1: Handling Predefined Exceptions - New - 9m

I will now demonstrate practices for lesson 9, handling exceptions. Notice in this practice, we will write a PL/SQL block that applies a predefined exception to process only one record at a time. The PL/SQL block selects the name of the employee with a given salary value.

We also have a second practice, as well, and we'll be doing that separately. And in that one, we're going to write a PL/SQL block that declares an exception for the Oracle server error ORA2292, which is an integrity constraint violation exception. So we'll be doing that under a second recording.

OK. So I'm going to start out with 9-1, on handling predefined exceptions. Again, just to summarize, in this practice, you write a PL/SQL block that applies a predefined exception to process only one record at a time. The PL/SQL block selects the name of the employee with a given salary value. In number 1, we're asked to execute the command in the lab 6-1 SQL file to recreate the messages table.

So let me go ahead and open up 6-1, or 6 1, rather. And that's going to drop the table and then recreate it. So we'll go ahead and run that against the MyConnection connection. It dropped the table, then it created it. And let's go ahead and close that.

Next, in number 2, in the declarative, we're asked to declare two variables, one called v_ename of type employees.last_name, and vm_sal of type employees.salary. And we're asked to initialize the vm_sal variable to $6,000. So let me go ahead and open up a new worksheet, and we'll go ahead and do that.

DECLARE v_ename employees.last_name%type. And then vm_sal of the type employees.salary%type. And we're asked to initialize that to 6,000.

In step number 3, it says, in the executable section, retrieve the last names of employees whose salaries are equal to the value in the vm_sal variable. If this salary entered returns only one row, insert the employee's name and the salary amount into the messages table. It tells us not to use explicit cursors. So let's go ahead and do step number 3.

We'll select last_name INTO v_ename from employees where salary=vm_sal;. And then insert into messages(results) values v_ename concatenated to a hyphen concatenated to v_emp_sal.

And now in number 4, we're asked to go ahead and create an exception section, because if the salary entered does not return any rows, we want to handle that exception with an appropriate handler, and we want to insert the message "No employee with a salary of" whatever that salary is. So let's go ahead and do that.

exception when no_data_found then insert into messages(results) values 'No employee with a salary of' concatenated to the vm_sal. That's a number, and since we're putting this into a single column with the string, we're going to go ahead and convert that to a character type.

And then step number 5, if the salary entered returns multiple rows, we want to handle that exception with the appropriate exception handler and insert the message, "More than one employee with a salary of" whatever the salary is into the messages table. So let's do a WHEN too_man_rows THEN insert into messages(results) values 'More than one employee with a salary of '.

Continuing on to the next page, number 6, looks like we want to handle other exceptions with an appropriate exception handler, and the message should say something like, some other error occurred. So let's go ahead and do that. WHEN others THEN insert into messages-- I see a typo there, by the way, up above.

OK. So let's go ahead and go on to step number 7. Display the rows from the messages table to check whether the PL/SQL block has executed successfully. So I guess that means we have to execute the PL/SQL block and then check the messages table to see what happened. So $6,000. It executed successfully. Let's check the messages table. More than one employee with a salary of 6,000.

So now in step number 8, change the initialized value of vm_sal 2,000 and re-execute it. Let's go ahead and do that, and then we'll take a look at the messages table again. And this time, it says, No employee with a salary of $2,000. OK, and then on to page six. Actually, it looks like that's going to do it, so that'll end demonstrations for practice 9-1.

## Practice 9-2: Handling Standard Oracle Server Exceptions - New - 5m

I will now demonstrate practice 9-2, Handling Standard Oracle Server Exceptions. So in this practice, you're going to write a PL-- PL/SQL block that declares an exception for the Oracle server error or a 2292, which is an integrity constraint violated child record found exception. The block tests for the exception and outputs the error message. I'll go ahead and start with the solution page.

And we see that in the Declarative section, we're asked to declare an exception called e_childrecord_exists. We're going to associate the declared exception with the standard Oracle server error 2292. So let me go ahead and demonstrate that. I'm going to go ahead and open up a new worksheet. And we will set serveroutput on.

And we'll do a Declaration section, e_childrecord_exists. And that's going to be an exception. And then we'll use the Pragma exception init clause in order to tie that exception name to the minus 2292 error code. OK.

Next, in number two, in the Executable section, we're going to display deleting department of 40, and include a delete statement to delete the department with department ID 40. So let's go ahead and do that. Begin dbms_output.put_line Deleting department 40. And then the delete statement. OK.

And then, number three, we're asked to include an Exception section to handle the e_childrecord_exists exception, and display the appropriate message. Let's go ahead and do that. Exception when e_childrecord_exists, then dbms_output.put_line cannot delete this department. There are employees in this department. Child records exist. All right.

Cannot delete this department. There are employees in this department. Child records exist. All right. I think that looks good. So then, we're going to go ahead and run it. And you see that we get the message, deleting department 40, cannot delete this department. There are employees in this department. Child records exist. OK, my friends. Well, that's going to do it for the demonstration of 9-2.
