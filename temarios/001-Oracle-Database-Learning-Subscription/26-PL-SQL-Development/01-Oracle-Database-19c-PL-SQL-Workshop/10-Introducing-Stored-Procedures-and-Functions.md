# 10: Introducing Stored Procedures and Functions

* Introducing Stored Procedures and Functions - New - 22m
* Practice 10-1: Creating and Using Stored Procedures - New - 8m

## Introducing Stored Procedures and Functions - New - 22m

OK, my friends, let's take a look at lesson 10, introducing stored procedures and functions. We are here, last chapter of unit 3, creating procedures.

OK, so after completing this lesson, you should be able to do the following. You should be able to differentiate between anonymous blocks and subprograms. You should be able to create a simple procedure and invoke it from an anonymous block.

You should be able to create a simple function. Create a simple function that accepts a parameter. And differentiate between procedures and functions.

OK, so what are subprograms? A PL/SQL subprogram is a named PL/SQL block that can be called with or without a set of parameters. A subprogram consists of a specification and a body. A subprogram can be a procedure or a function, or a trigger. Typically, you use a procedure to perform an action, and a function to compute and return a value.

So functions always have to return data. Procedures may return data but usually go out and do some sort of a task.

All right, now differences between anonymous blocks and subprograms. Anonymous blocks are unnamed. Subprograms are named. Anonymous blocks have to be compiled every time you run them.

Subprograms are compiled only once and stored in the database. Anonymous blocks are not stored in the database. Anonymous blocks cannot be invoked by other applications, because we don't have a name to invoke them by. Subprograms are named and therefore can be invoked by other applications.

Anonymous blocks do not return values. Functions have to return values. Subprograms are built to take parameters. Anonymous blocks cannot take parameters with the exception of cursors. You can define cursors with a parameter.

OK. I do want to point out that we are going to look in dedicated chapters, coming up in the course, at creating procedures and creating functions. So this chapter here that we're in is designed to kind of get you familiar with the concept of a procedure and a function. But we're going to talk more about procedures and functions coming up soon.

OK, the syntax. I'm going to show you how easy it is to create a procedure. Let me go out to my demo environment here. And what I'm going to do is, I'm going to change this into a procedure instead.

So I'm going to copy this, and I'm going to put that in another worksheet. And what I'm going to do is, I am going to put on a create or replace procedure insert_demo_proc. And in this one I'm going to put a couple of parameters in, one for the ID and one for the name.

We do have to give it data types. This one's going to be a number. This one's going to be a varchar2.

Now again, just as a reminder, we are not allowed to give a size to a parameter, so just the data type with no size. And then you can either use is or as, either one. No difference between the two other than just the spelling.

Now this one, because I'm using parameters, I'm going to cut this. And I'm going to just paste this down below, because I'm going to have an anonymous block to invoke my procedure. OK.

And I'm going to show you the benefits of using a procedure with an exception handler as well. So just so I don't have to take the procedure name as many times, I'm just going to copy and paste that procedure name.

OK, so this is going to be my anonymous blog that calls the insert_demo_proc four times. But let me finish up the coding of my executable section and set my procedure itself.

And I tell you what-- now usually what we like to do on procedures-- we usually like to put the name of the procedure or function in the end. This is not mandatory. You don't have to put the name of the subprogram right here on the end.

But it's nice to do that, especially when we're creating packages. Because you're going to end up having so many end keywords. It's going to be kind of hard to track what you're ending.

And if you remember, we've got end on a case. We've got end on subprograms programs. We've got end if. We've got end case. We have end on a case expression. So putting what you're ending is always a good idea, so you can make your code a little clearer to understand.

Now I am going to format this to make it look a little prettier. And I'm going to put down also a command called Show Errors. And what that's going to do is, if I have any compilation errors, it's going to show me my errors in the Script Output window.

Right now I don't have any errors, and so it's telling me that it was compiled. If I happen to have an error-- I'll cause an error to occur. You notice how it shows my-- well, not only do I get it in my Compiler log, but you notice that it also shows me in my Script Output that it compiled with an error, Encountered the symbol END when expecting one of the following. OK?

So anyway, I like to put the Show Errors there, just so I can see those errors explicitly. OK, so now that I've-- let me recompile it. OK, it's compiled. No errors.

Over here, by the way, in the Object Tree, there's my Procedure category. If I expand that-- let's refresh that. And you see that I've got my insert_demo_proc right there.

Now the OR REPLACE class is optional, by the way. And the reason why we put that in there is, because if you have created a procedure, and you wanted to make changes to the procedure, and if you had already granted that procedure to other people to be able to execute against it-- if you drop the procedure and recreate it, you're going to have to re-grant all the privileges to all the people that you've already granted it to. So the OR REPLACE allows us to edit a procedure or function or package or trigger, without having to re-grant privileges that we've already granted on that object.

So you've got the two decisions-- drop it, recreate it, re-grant it to people, or create or replace, make changes, recompile it. And nobody has to be re-granted permissions on it. So there we are.

Now let's go ahead and execute it. In the last chapter where I was showing you exceptions, we saw that when I did this in an anonymous block, the first two rows got inserted into my demo table, and then this one errored out. And it jumped to the exception section. And we didn't get to process this last row.

But now that I have embedded this inside of a procedure, I can call the procedure four times. I'm going to get an error back on one of those, OK? But the cool thing about doing that inside of my subprogram is, if I come in and select star from my demo table, you will notice that I got Gietz in my table as well.

So all three of the valid rows got inserted. The only one that did not get inserted is the one that caused the error in the first place. So you see how that's kind of convenient when you put the exception handler inside of your procedure, and then call your procedure over and over and over again.

All right, let me go back to the book and show you what the book is going to have to say about procedures. All right, we're creating a table called dept. Basically it's going to be a copy of the departments table.

We're going to create a procedure called add_dept. We're going to have a variable called v_dept_id. We're going to have a variable called v_dept_name.

We're initializing v_dept_id to 280. We're initializing v_dept_name to ST-Curriculum. We're going to insert into the dept table the values of the variables. And then we're going to print out how many rows were inserted.

We're going to go ahead and run the Create Table and the Create Procedure code. You see that our dept table was created and you see our procedure was compiled. And then we're going to invoke it.

So we can invoke the procedure inside of another PL/SQL block. Just put the procedure inside of BEGIN and END. So that's how we're invoking it, similar to how I invoked it from an anonymous block. And when we go in and run our SELECT statement, we see that that row got inserted.

All right, now a function. A function is different than a procedure. A function always has to return something. So it's got a couple of things that are different. I'm going to create a quick little function called get_emp, something like that. Let me show you how to do that.

Create or replace function get_emp-- I'll pass in an ID. And because these things have to return something, we have to give it a data type that it's going to return or a type that it's going to return. So I'm going to pass in an ID and I'm going to get a last name back out.

So you know, a last name is a varchar2 data type. And let's go ahead and do a variable, v_lname. Let's do a select. Select last_name INTO v_lname from employees where employee_id=pid. And then let's return the variable.

So a couple of things I want to point out-- we have to tell it what type it's going to return. It's going to return a varchar2. And then we have to have a return value-- so a return type and a return value.

The variable is going to be the return value. And we're populating the variable using the employee_ID. So let me compile this, and then let's go ahead and use it.

Now functions always have to return their data into something else. I'm not able to do this. I can't come in and say get_emp(100). This is going to actually error out if I tried to run it like this. This is the way we invoke a procedure. That's not the way we invoke a function.

And we get an error message, get_emp is not a procedure. What we have to do is, we have to capture that value into something else. We happen to have the package called dbms_output with a procedure called put_line, which allows input parameters.

So what we're going to do is, we're going to have the input parameter for put_line capture the return value from the function. And that's going to allow me to print out the last name of my employee.

Now we can also sometimes use functions in a Select statement. Select employee_ID and get_emp(employee_id). So I'm going to be pushing in the employee_id intop my function, and it's going to allow me to return my last names of my employees. So you notice how that's working.

So, you know, invoking functions is a little bit different than invoking a procedure, as you can see. Now we'll go over all the rules of using functions in Select statements in a later chapter. But just to keep it simple, the way that you invoke functions is different than the way that you invoke procedures, all right?

All right, so here we have a function called check_sal. Now this one is a Boolean type, so it's going to return a true or a false or a null. And basically what we're doing is, we're checking to see how somebody's salary stacks up to the average.

We have a department ID. We have an employee number. We have a salary. We have an average salary. We're initializing the v_empno to 205.

Select the salary and department into these two variables where employee_id equal 205. Then we're going to select the average salary into the average salary variable for that department.

If that person's salary is greater than the average salary, we're going to return a true. Otherwise, we're going to return a false. And in the event that we don't have employee 205, the No Data Found exception is going to return a null.

So now we're invoking it. And basically we're saying, hey, IF check_sal IS NULL THEN we're going to print out, "The function returned NULL due to exception." ELSIF check_sal is true-- and that's what that implies, by the way. ELSIF check_sal that means ELSIF true-- THEN salary is above average. ELSE, "Salary less than average."

Well, notice we're getting back salary greater than average. So it looks like employee 205's salary is greater than the average salary for the department.

Now instead of hard coding employee 205, we're actually going to put a parameter in here instead. And we're going to be able to supply the employee number when we run it. The same logic for the rest of this, right? It's just that when we run it, we're able to pass in the employee number.

If check_sal 205 is NULL then return this. ELSIF check_sal with 205, Salary above average. ELSE Salary less than average.

All right, so our quiz. Subprograms are named PL/SQL blocks and can be invoked by other applications. That is true. Are compiled only once-- that is true.

Of course, you can edit them and recompile them if you want. Or if you compile them and they error out, you will need to fix it and recompile it. But, you know, the point of letter B is that they're not compiled every time they're executed.

They are stored in the database. That is true. They do not have to return values if they are functions. That's false. Functions have to return values.

And they can't take parameters. That is true.

All right, so in this lesson, you should have learned how to create a simple procedure, how to invoke the procedure from an anonymous block, how to create a simple function, how to create a simple function that accepts parameters, how to invoke the function from an anonymous block.

So we are going to give you some practice here in lesson 10. You're going to convert an existing anonymous block to a procedure. You're going to modify the procedure to accept a parameter. And you're going to write an anonymous block to invoke the procedure. So that is going to do it for lesson 10.

## Practice 10-1: Creating and Using Stored Procedures - New - 8m

I will now demonstrate practices for Lesson 10, Introducing Stored Procedures and Functions. I'm going to go ahead and start with the solution. In this practice, you're going to modify existing scripts to create and use stored procedures. So in step number one, we're asked to open the sol_3.sql script from the /home/oracle/labs/plsf/soln folder. And we're asked to copy the code under task 4 into a new worksheet. Let me go ahead and do that.

Going to open up a new worksheet first. I'm going to go ahead and open up the solution that they're talking about there. plsf, labs, solution, lab, solution 3. And we're supposed to copy from task 4, which looks like this section here. And copy that into the worksheet.

OK, I'll go ahead and close that solution. And now in step letter a, we're asked to modify the script to convert the anonymous block to a procedure called greet. And we have a hint. Also remove the SET SERVEROUTPUT ON command. So let's go ahead and do that. And let's take out the DECLARE keyword and let's replace that with create procedure greet IS.

And I like to come down here and also put the name of this subprogram that we're changing down below. I like to go ahead and format that. There we go. OK. And now let's go ahead and go to step b, where we will run this so that it'll create the procedure. There we go, procedure GREET compiled. Let's just double check and make sure it's listed under the Procedures section. And there is our procedure called greet. All right.

So next in step letter c, we're asked to save this script as lab_10_01_soln.sql. So let me go Save. And let's do that back in the Labs category there. All right, lab_10_01_soln.sql. OK, now we're asked to click the Clear button to clear the workspace.

And create and execute an anonymous block to invoke the greet procedure. Now, let me just continue on to the next section. I'm just looking to see if we need to do that on a separate worksheet. Yeah, let's do that on a separate worksheet. I just want the worksheet to be empty, is what they're saying with clicking the Clear button to clear the workspace. Just make sure that your worksheet is actually clear.

And then let's do the anonymous block. Set serveroutput on. Begin. Let's call greet. And let's end it. And let's go ahead and execute it. And you notice down below that it says, hello world. Today is 24th of June of '20 and tomorrow's 25th of June of '20. It should look pretty similar to what we have on our screenshots here.

Now, in step number two, we're asked to go ahead and modify the 10_01_soln.sql script as follows. We're supposed to drop the procedure called greet. Let's do that. And then we're asked to modify the procedure to accept an argument of type varchar2 and call the argument p_name.

So I'll tell you what, let me cut that. Let me put that up at the top. So we're going to drop it before we recreate it. And this time, we're going to pass in a parameter, p_name varchar2. And then we want to print hello whatever our name is, instead of printing hello world.

So down below, we will say hello. And then we'll put in p_name. And let's go ahead and save it as 10_02_soln.sql. File, Save As, 10_02_soln.sql. And then we're asked to go ahead and execute the script to create the procedure.

And then back in our anonymous block, we'll go ahead and modify that to say greet. And I'll put my name in there. And let's go ahead and run it. And we see it says hello Brent. Today is 24th of June of '20. Tomorrow is 25th of June of '20. OK, so that is going to do it for the demonstrations for practice 10.
