# 14: Creating Packages

* Creating Packages - New - 25m
* Practice 14-1: Creating and Using Packages - New - 23m

## Creating Packages - New - 25m

OK, my friends, let's take a look at Lesson 14 on Creating Packages. We are hear in Unit 4, Working with Sub-programs, Lesson 14 Creating Packages. And you'll notice that we have another chapter after this one on Working with Packages in Lesson 15.

So after completing this lesson, you should be able to describe packages and list their components. You should be able to create a package to group together related variables, and cursors, and constants, and exceptions, procedures, and functions. You should be able to designate a package construct as either public or private, invoke a package construct, and describe the use of a bodiless package.

So the benefits and the components of a package. Now you've already been using a package up to this point. DBMS_OUTPUT is an Oracle-supplied package, one of over 200 different Oracle-supplied packages. And PUT_LINE is a procedure in the DBMS_OUTPUT package that enables displaying messages to the output buffer. DBMS_OUTPUT also has other procedures such as PUT_LINE and PUT, and GET_LINE and GET_LINES.

So what is a package? A package is a schema object that groups logically related PL/SQL types, variable sequences, and subprograms. A package is compiled and stored in the database where many applications can share its contents.

So these are the advantages of packages. Easier maintenance because they're grouped together. Whenever you create a package, it's recommended that you put all of the related modules inside the same package. And that way, if you need to make a change to the logic, all of those objects are in the same package and you can more easily maintain all of those different related components.

Now that also ties into modularity because each of those individual components forms a module or a unit of work. And because all of those are organized inside of a package structure, it allows us to design our application easier, break down large tasks into a bunch of smaller tasks, and group them all together into a package.

We get better performance because there's only one copy in memory for all users, once it's invoked. And also we have the ability to hide information, because we have the ability to keep the package body private if we need to. And the interface is through the package specification. And therefore, since the public interface is through the package specification, people don't get direct access to the package body. And so, we can hide logic and we can also obfuscate the logic as well to even hide information further.

So how do you create PL/SQL packages? Well, packages will always have a specification. And they will usually also have a body. You have to create and compile the specification first, and that's the public interface. And then the package body is created and compiled afterwards.

Now the specification itself is nice and short and condensed. It contains the names of the objects, the parameters that you need to supply for those objects, and anything else that you need to be made public. And then the body has the logic or the implementation as we're saying here.

So here we have a diagram that is pointing out the package specification. Now in this example, we have a variable declaration in the specification and we have the declaration of a procedure called A. And so, if somebody were granted the permissions to the package, they would be able to execute against the procedure. And they could also interact with the variable that is defined in that specification.

Now the package body is the private area. That is where we might initialize the variable. And we might use that variable inside of the definition of procedure A.

Now notice that we also have a procedure called B that is defined. Now procedure B is not listed in the package specification. So procedure B is considered a private subprogram because we cannot invoke it from the package specification. However, we can use procedure B in the logic of the package body.

And that's what we're pointing out here is that the package has both public components, which are the components in the specification, and private components, which are only listed in the package body. A developer can access the functionality of a package through the API of the package, which is the specification.

So in working with packages, we will create the package specification and body. And then we will invoke the package subprograms. We are going to also show you how to display package information through user source or through SQL Developer. And then we're also going to show you how to drop either the package and the body or just the body. And we'll show you how that works.

So I think what I'll do is do some demonstrations. Let me do that. And then we'll come back and take a look at the book.

So what I'll do is I will create this specification. So I'm going to create or replace package. And I'll call it demopkg.

And what I'll do, I'll have two different procedures in here. I will have a procedure called update_sal. And what I'm going to do is I'm going to pass in two parameters, pid, which is a number, and psalary, which is a number as well. And all I need to do is just put what we call the signature of the procedure at this point.

And then what I'll do is I'll create another procedure called get_emp. And in this one, what I'll do is I'll have an input parameter pid number, and then I'll have a pname, which is an OUT mode parameter which is a varchar2. And then that's all I need from a package specification, OK?

I will go ahead and format that so that it looks nice and organized. And I'll go ahead and compile the package specification. Now that I've done that, I'll go over here to the Packages section, and you notice that I have the package spec.

Now this is what I usually use when I create my body. Now the body is going to be dependent upon the parameter definition. And so I usually will use the wizard to go ahead and create the body because what it's going to do is it's going to copy the definition from my package specification. And it's going to copy it into a body, OK?

Now if you wanted to write the package body yourself, all you have to do is come in here and say, create or replace package body. And then you have to complete the coding logic of these two different procedures and then compile that. And it would create the body for you.

But what I like to do is I like to right click my package specification. And I like to come down here to the option where it says Create Body. And what it will do is copy into a compilation window the rough structure, if you will, for the package body.

Now you notice what it did is it basically shows me what elements that I need to replace inside of my procedure. So right here it's got a comment on the TODO, and it says, "Implementation required for procedure DEMOPKG.update_sal." So that's kind of a reminder. Right here in place of the null and in place of that comment, I'm going to come in and I'm going to say, "update employees set salary=psalary where employee_id=pid." And that's really all I need for that particular procedure.

Now the get_emp, that's going to be a little bit more complex. I'm going to have to do a select statement, select last_name INTO pname from employee where employee_id=pid.

All right. And now, all I have to do is compile the package body. And oops, misspelled employees, by the way. So it should be plural. There we go. Let me recompile that. OK, so I think we're good.

And now if I expand my package specification, you notice that I have this specification. And then indented slightly further, we have the package body. And if I expand that, you see the subprograms listed in both the specification and the body.

So now in order to execute my package, what I will do is I'll come in and I'll say, "begin demopkg.update_sal." And I'll do 100 for the employee ID and I'll do $1 for the salary. And then I'll end it. So it's package name dot procedure name. And then when I execute that, it tells me that the procedure successfully completed. And when I go and look at the employees table, and if I go look at employee 100, you should see that that individual makes $1 now.

So I really easily created a package. Now in this class, what we're teaching you to do is to create the procedures and functions as standalone objects first. And then when it comes time to do it in labs, you are going to end up copying and pasting the definition of your standalone subprograms into a package.

I just want to point out that that's usually not the way that you create a package. If you know you're going to create a package, you would just create the procedure and the function inside of the package, rather than creating it as a standalone and then copying it into a procedure, or into a package, rather. OK?

So let me go back to the book and show you what the book is talking about. Now the package specification, I created subprograms. But you could also create types. You could also define variables as well. And I don't know if you noticed this. Let me go back to my demo.

But when I created my package, you'll notice that I listed the name of the package in the END. And you notice that I also listed the name of the procedure in the appropriate END for the procedures. That helps you keep track of what you're ending, otherwise you're going to have too many End keywords. And so you know, it becomes difficult to remember what you're ending if you don't put the names there. It's an optional step, but that's considered preferred practice.

All right. So they're showing you creating a package specification using SQL Developer. You could do that as well. You could just right click Packages. Select New Package. Give it a Name. Click OK. It creates the empty package specification and then you go in and add in the signatures for your different subprograms. And then when you compile that, you'll see it over in the object tree.

And then as I did, people usually right click the specification and then tell the wizard to create the body. And that way you don't forget any of the ENDs. And it saves you a lot of typing honestly. And it helps to make sure that you don't make any mistakes on redefining the specification components.

So here's an example of a package specification. Now this package is called comm_pkg, and it's got a public variable called v_std_comm, which stands for commission, by the way. And it's initialized to 0.10. And then we have a procedure called reset_comm, which stands for reset commission. And we're going to be able to pass in a new commission through a parameter. So that is the specification. We've got a public variable and we've got a public procedure.

And then we create the package body. Again, just like when you create procedures and functions, you have the option of including the OR REPLACE option. That is going to allow you to edit an existing package body, if it already exists. Or you can also use CREATE OR REPLACE with the package specification as well.

Whatever you put in the package body that you have not listed in the package specification are considered private, and are not visible outside of the package body, and are also not able to be invoked from outside of the package body. Anything that you put in the specification is going to be visible in the package body.

So here is the package body for the comm_pkg. We have a FUNCTION called validate. And basically what it's going to do is it's going to check to see whether somebody's commission falls between 0.0 and whatever the current maximum commission is from the employees table. I happen to know that the current maximum commission in the employees table is set to 0.4. So basically, we're checking to see whether it's between 0.0 and 0.4.

And then we have a procedure called reset_comm where we pass in a new commission. We're invoking the validate function to see if that new commission coming in falls within that tolerable range of 0.0 and 0.4. Basically the IF statement says, IF true, THEN reset the v_std_comm variable. And then ELSE, RAISE_APPLICATION_ERROR, so raise an exception if it's a bad commission, if it doesn't fall between those tolerable ranges.

Now, the FUNCTION called validate, that is only listed in the body, and the body itself can only use that validate function. I would not be able to call the validate function from outside of the body. But once it's defined, I can use it any place else in the rest of the package body.

Now in order to invoke the package subprograms, again, you can do it from another anonymous block. You can do it from another subprogram. In this case, we're invoking a function within the same package called validate, as we were saying. And the validate function we can't invoke from outside the package.

But they're showing you how to invoke the package from SQL*Plus. EXECUTE comm_pkg.reset_comm (0.15). And then how to invoke that from a different schema. We have to put schema name dot package name dot subprogram name. So in this case, "scott" would be the name of the schema that owns that particular package.

You can also right click your package specification. Assign a value to the Parameters and click OK. And it would go ahead and run your package specification using SQL Developer. It would only run the components that you decided to run, by the way.

Now sometimes we create a package specification that does not need any other logic assigned to it. So therefore, we would not have to have a body. That's what we call a bodiless package.

We have some examples here. We have a package called global constants, basically, is what that stands for. And we've got four different constants that are converting miles to kilometers, kilometers to miles, yards to meters, and meters to yards.

Now we don't need to do anything else with those particular constants. We can't change them. And we don't need any other logic to make them work. So we don't have to have a package body. And we can go ahead and use those as-is by invoking them in another subprogram, or if it were a function, or some other element that didn't need a body. We would be able to just execute as-is.

So you'll notice that they EXECUTE DBMS_OUTPUT.PUT_LINE. They're taking 20 and multiplying that by the package name, global_consts, dot constant name, which is c_mile_2_kilo. We're basically converting 20 miles to kilometers.

And then notice we have another example. We're creating a FUNCTION as a standalone function that uses those package constants to figure out the calculation. So we're pass in a value to the parameter. And then we're going to multiply whatever value is times the package dot c_meter_2_yard constant. And that would allow us to convert, in this case, when they execute it, converting one meter to a yard.

So in order to view the packages you can use the Data Dictionary. Now you can look at the user_source view. And in this case, you would filter on the name of the package and the type package. And that will allow you to see the package specification. In order to see the package body, you have to put the type is "PACKAGE BODY," and then you'll see the package body. Make sure you put the ORDER BY LINE, otherwise you won't see the code in the correct order.

Or you can view these in SQL developer. To view the package specification, just click on the package name from the tree. To view the package body, click on the name of the package body in the tree, and it will open it up.

Now how do we get rid of packages? In order to drop the package specification, we would say, "DROP package_name" or the PACKAGE. Not only will that drop this specification, but that will also drop the body. We can't have a body without a specification, so if we drop the spec, then the body goes away with it.

Now we do have the ability to just drop the package. And in that case, "DROP PACKAGE BODY", whatever the name of the package is.

So the Guidelines for Writing Packages. Develop packages for general use. Define the package specification before the body. The package specification should contain only those constructs that you want to be public. You should also place items in the declaration part of the package body when you must maintain them throughout a session or across transactions. And the package specification should contain as few constructs as possible. "Keep it simple" is the rule.

All right. Quiz. The package specification is the interface to your applications. It declares the public types, the variables, the constants, the exceptions, the cursors, and subprograms which are available for use. The package specification may also include PRAGMAs, which are directives to the compiler. And this is true. That is true.

OK, so in this lesson, you should have learned what packages are and be able to list their components. You should have learned how to create a package to group related objects together, including variables, cursors, constants, exceptions, procedures, and functions. You should know how to designate a package construct as either public or private, how to invoke a package construct, and also you should know what a bodiless package is.

So we are going to have you create packages in Lesson 14. So we'll have you go ahead and do that. You are going to create packages and invoke package program units. And this will do it for the lecture for Chapter 14.

## Practice 14-1: Creating and Using Packages - New - 23m

I will now demonstrate practices for Lesson 14 Creating Packages. In the overview we see that in this practice you create a package specification and a body called job package, which contains a copy of your add job, update job, and delete job procedures as well as you get job function. You also create and invoke a package that contains private and public constructs by using sample data.

Now, notice that before starting this practice you should execute the cleanup 14 dot SQL script. I will start with the solutions. And in the solutions it tells us to create a package specification and body called job package containing a copy of your add job, update job, and delete job procedures as well as your get job function. So you're going to use the code from your previously saved procedures and functions when creating the package. You can copy the code in a procedure or function and then paste the code into the appropriate section of the package.

In step A we're asked to create the package specification including the procedures and function headings as public constructs. Now, there is a reference to the solution file. So if you would rather create that from the solution file, you can go ahead and do that. But I'll go ahead and create this by writing it in my SQL Developer.

So I will create or replace the package. And it's going to be called job_pkg. And then I'm going to have a procedure, and that's going to be called add_job. And we're going to have some parameters in that. So I will have a p_jobid which is going to be a jobs.job_id percent type. We will have a p_jobtitle, and that's going to be a jobs.job_title percent type. OK, and let me just wrap that around so you can see the procedure definition.

Next, I'm going to create a procedure called delete job. And for that one we're going to have a p_jobid which is of the jobs.job_id percent type. And then we will have a function called get_job.

And that one's going to have a parameter called p_jobid. And that's going to be an in mode parameter of the jobs.job_id percent type. And for this one, we're going to return the jobs.job_title percent type.

And then finally, we will have a procedure called update job. And for that one we will have a parameter p_jobid, which is an in mode parameter of the jobs.job_id percent type, and the p_jobtitle, which is an in mode parameter of the jobs.job_title percent type. And then we'll go ahead and end our jobs package.

So I'm going to go ahead and right-click that and Format. And then I'm just going to browse it and make sure that it didn't make any logical mistakes. And jobs.job_id percent type, jobs.job_title percent type, p_jobid of the jobs.job_id percent type, a function called get_job and then we're going to return the jobs.job_title percent type, and then a procedure called update job where we're passing in the job ID and p_jobtitle of the jobs.job_title percent type.

OK, so I am missing a closing paren, it looks like, after my jobs.job_title. So let me go ahead and put that in there. And let me go ahead and re-beautify that, there we go. And I'll go ahead and compile this.

Now, I'm actually getting a warning message because I've enabled warnings in my SQL Developer tool. Let me go in and turn those off. I'm going to go to Tools, Preferences, and I'm going to go to PL/SQL Compiler. And I'm going to change that to disable.

And then let me re-compile that, and that should take care of that warning that I'm getting down below that looks kind of like an error. Let me just clear that and recompile. And you notice that I no longer get that warning message.

OK, in letter B we're asked to create the package body with the implementations for each of the sub-programs. Again, there is a solution that you can run to go ahead and do that. But what I'm going to do-- I'm going to go into my packages, and I'm going to refresh my packages. And I'm going to right-click my specification. And I'm going to create the body using the wizard.

Next what I'll do is I will go ahead and put in the rest of the logic in my package. So here on my add_job, here where it says null along with that comment, I'm going to go ahead and just copy that insert statement along with a commit from the code in the book. And we'll just make sure that that makes sense. Insert into the jobs table job_id, job_title values p_jobid and p_jobtitle, making sure that my parameters are spelled correctly, looks good.

Now on the delete job I'll go ahead and do the same thing. I will do a delete statement along with an exception handler. And I'm going to go ahead and put that in place of my implementation. And you notice that I'm deleting it from the jobs table where job_id equal to p_jobid. And then if we don't happen to find that job ID, then we're going to raise an exception, looks good.

Now with the function get_job what we'll do is we will select the job title into the v_title variable where the job_id equals the p_jobid. And we're going to return the job title through the variable called v_title. And then finally on the update job procedure we're going to update the jobs table, set the job_title equal to the p_jobtitle where the job_id equals the p_jobid. And for this one we're also going to put an exception handler. And what that's going to do is raise an exception if we don't happen to find that job ID.

OK, so I think that should do it for that particular package body. And I will compile that. And I tell you what. It looks like maybe I'm missing a couple of components here, looks like I'm missing the v_title variable.

So the v_title is in the function. So I'm actually going to come in and define that here. And that's going to be the jobs.job_title percent type. And let's go ahead and re-compile that. And it looks like we have successfully compiled the package body.

OK, next page, page 7, we're going to delete the following standalone procedures and functions that you just packaged by using the procedures and functions nodes in the object navigation tree. So let's go over to my procedures category. And I've got an add_job procedure that I'm going to right-click and drop. I'll go ahead and say apply. We'll do the update job procedure as well. And we'll do the delete job procedure also.

And the reason we're deleting these is because we don't have to maintain a standalone copy as well as a copy inside of the package. And so that's why we're doing that in this case. Now we're also going to drop the function called get_job.

OK, so next in letter D, we're going to invoke the add_job procedure by passing the values IT_SYSAN and Systems Analyst. So let's go ahead and do that. I'm going to go ahead and close my package body. I'm going to clear out my specification. And let me close out my log, and we'll clear out the script output page.

And we'll go ahead and execute the job package dot add_job. And we'll do IT_SYSAN, and we'll do Systems Analyst. And we'll go ahead and execute that. And it tells us it successfully completed.

Next in letter E, we're going to take a look at the jobs table to see the result. So what I'll do-- I'll just click on the jobs table, and then I'll click on the Data tab. And you see that I've added that row to the jobs table. If you prefer, you can run the SELECT statement that the book is showing you there.

Now, continuing on to step 8, we're going to create and invoke a package that contains private and public constructs. So let's do that. We're going to create an add employee procedure, a get employee procedure-- and both of those are going to be public constructs-- and then we're going to do the valid_deptid function as a private construct.

Now, if you prefer, you can run the solution. Or you could hand-type it. Or you could go ahead and copy out of the book as I'm doing and paste that into your SQL worksheet.

If you do copy, just make sure that it makes sense to you. Here we have a package called emp_pkg. We have a procedure add_employee that has these parameters. And we have a procedure called get_employee that has these parameters.

Let's go ahead and compile it, and then we'll go ahead and create the package body. Now, if you're going to copy and paste out of the book, just notice that the package body is spread across a couple of pages here. And what we're going to do is make sure that the logic makes sense for you. And again, if you prefer, you could go ahead and run this solution from the solutions file that they're talking about there.

So just make sure it makes sense. Here is our function. And basically what we're doing is we're checking to see whether or not a department ID that we pass in is a valid department. So this is what we were talking about as far as a private construct.

I've only created the valid_deptid function inside of the package body. If I go to my packages-- and let me just refresh, and you'll notice I have my emp_pkg package. You'll notice that I have two public constructs as we were talking about, one called add_employee, one called get_employee. But the function, in this case, is going to be private because I've only listed it in the body. And we're either going to return a true if it runs and finds a valid department-- if we don't find the valid department, however, we're going to return a false through the exception handler.

Next we have the add_employee procedure. And what we're going to do in that case is we're going to call that private sub-program. And we're basically going to check to see whether or not the department ID that's coming into the parameter is a valid department ID.

If it's a valid department ID, then we're going to go ahead and do the insert. And we're going to end up using a sequence for the employee ID. And we're going to use parameters for the other values with the exception of the hire date which we're using the SYSDATE function.

Now, we also have a RAISE_APPLICATION_ERROR that is going to allow us to handle when we get an invalid department ID. Next step after that, we have a procedure called get_employee. And that's where we're selecting the salary and job and populating those into two outmode parameters. And we'll go ahead and compile that, and it looks like everything successfully compiled.

Now coming up on the next page, page 10, we will go ahead and invoke the emp_pkg.add_employee procedure, execute emp_pkg.add_employee. We're going to pass in the name Jane. We're going to pass in the name Harris for the last name. And then the job ID-- or the email, rather, is going to be JAHARRIS. And the parameter called p_deptid is going to be assigned the value of 15.

And we'll go ahead and execute that. Let me clear out my script output below first. And in this case, let me just make sure that it didn't wrap that around to the next line. It's causing an error, right? Execute emp_pkg.add_employee Jane Harris JAHARRIS p_deptid 15. OK, I think that'll work a little better now. Again, remember that the execute does not like you to wrap that.

Now in this case, it tells us, hey, you have an invalid department ID. Department ID 15-- we don't actually have a department ID of 15. Now what we'll do is we will go ahead and invoke that.

This time we will use department 80. And we're going to use David Smith for the values. And by the way, rather than using the execute keyword, I'm going to do this as an anonymous block so it fits on my screen a little bit better.

So we're going to do David Smith, and the email is going to be DASMITH. And this time we're going to use department 80. And department 80 happens to be a valid department. So when I execute this-- you just wrap that around so you can see those parameters. When I execute this one, since I'm using a valid department, it's going to go ahead and add the employee to the table.

So coming up on the next page, page 11, we're going to go into the employees table, and we're going to verify that the new employee was added. You can either run the SELECT statement that is shown in the book, or you can click on the employees table and click on the Data tab, and we should see that we've added David Smith.

All right, my friends, well, that is going to do it for the demonstrations for practice number 14.
