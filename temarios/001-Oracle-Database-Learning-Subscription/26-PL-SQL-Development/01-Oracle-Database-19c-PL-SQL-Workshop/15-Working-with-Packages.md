# 15: Working with Packages

* Working with Packages - New - 37m
* Practice 15-1: Working with Packages - New - 37m

## Working with Packages - New - 37m

OK, my friends, let's take a look at Lesson 15 on working with packages. We are here in Unit 4, Working with Subprograms. We are in Lesson 15, Working with Packages.

So after completing this lesson, you should be able to overload package procedures and functions. You should be able to use forward declarations. You should be able to create an initialization block in a package body, and also manage persistent packaged data states for the life of a session.

Overloading package subprograms, what is that? So here we have Jack that says, hey, Alice. Can you help me with this task at hand? I want to calculate the tax of all employees in the company.

And then he thinks about it and he says, wait, not all employees, but only employees of a single department. And then he says, well, well, maybe I want to be able to do a single employee as well, or I think I might need all of those options. Can you help? And Alice says, sure, I'm happy to help.

So what we can do when you create a package. You can create more than one version of a subprogram. Basically, what you can do is create two or more subprograms with the same name.

Now, in order to do this, it requires that these subprograms' formal parameters differ in number, order, or data type family. It enables you to build flexible ways for invoking subprograms with different data. It provides a way to extend functionality without the loss of existing code. So that means you can add new parameters to existing subprograms. So you can overload local subprograms, package subprograms, and type methods, but you can't overload standalone subprograms.

Now, you have already at this point been using overloaded subprograms if you've ever written any SQL. Let me show you what I mean. So if I wrote a SELECT statement and I use the to char function with the salary column, the to char function, that is a function that takes a number and converts it to a character. And I can tell it's a character, because it's left justified in the column.

It's taking an input parameter that's a number type. But I could also use to char against a date. And if I did that, you'll notice that I've got a different version of to char that takes two parameters. And the first one happens to be a date data type.

And so the to char function, there's at least four different versions of the to char function. Now, the to char function is built inside of a package in the database, called standard. And so in the standard package, we have the ability to create multiple different versions of different subprograms. And you have the same capability if you have the ability to create packages.

So let me show you what I'm doing here in my demo package. So I have a procedure called get emp, and with the get emp procedure, I'm passing in an employee ID, and I'm getting the name back out. Well, what if I wanted to be able to get an employee by their first name?

What I might end up doing is I might create another procedure, called get emp. Now, in order to do this, you either have to have a different number of parameters or they have to differ in the data types positionally. So what I could do is I could say, pf name, and that one's a var chart 2 data type, and then the second one will be a p name, which is an out mode parameter, which is a var chart 2.

And let me format that so it looks a little better. There you go. So I have two procedures, both called get emp.

Both of them have two parameters. But in my case, the first one is a number in one version, and the second one is a var char 2 in the other version. So I'm not going to have any problems with compiling this, because I'm following the rules.

Now, notice that did invalidate my package body, because the specification in the body, they need to have the same components in it. If I put it in the spec, I have to put it in the body as well. So I'm going to go down and edit the body next, and I'm just going to end up pasting the definition of that procedure. And then I'm going to paste the definition of my other procedure.

They're going to be pretty similar to each other. It's just that one of them, I provided the employee ID, and the other one, I provide the first name. So I'm going to do where first name equal pf name instead.

Now, in this one, I'm going to do an exception here. Exception, when too many rows, then I'll put a message out here to the user that says, hey, more than one person with that name, please search by ID instead-- something like that. And let me make this formatted again, make it look pretty, and then I'll compile the body.

Now, it looks like a compilation error. So let me see what's happening here. Oh, you know what? I forgot my is keyword. That's what happens when you copy and paste.

[LAUGHS]

There we go. So it compiled successfully. And now, I've got two versions of get emp.

Now, let's invoke them. Let's see if they work correctly. Let's see. Let's do declare v val number begin demo pkg.getemp.

I will pass in-- I guess this is going to have to be a var char, because I'm returning a name to do an out mode. And I'll pass in 101, and v val, and then I'll go ahead and use my put line procedure to print out who that is. And when I run it, you notice I get back the user name, Kochhar.

So I'm using a numeric for this one. And now, just to make sure the overloaded version works, I'll put it in her name, Nina. And you'll notice that I get back Kochhar again, and that's because I can search for Nina either by ID or by first name.

And now, let's check our exception handler. We'll put in a name, like John. And this time, I expect that we're going to get an error.

Well, my exception handler error. It says, "More than one person with that name. Please search with ID instead." And you notice that it's successfully completed.

So you can do overloading, as we were saying. So you are going to do that in your labs. You're going to be going in and copying some existing subprograms into your packages, and then you're going to create a second version of those inside of your packages.

Now, let's get back to the book and show you what the book is going to say about it. Here we have two different procedures, both called add department. One of those allows you to provide the department number. The other one does not.

So this one has three parameters. This one has two. And you'll notice that when we go to create the logic, the one that takes three parameters allows us to provide the department number and an INSERT statement into the departments table. The one that does not allow you to provide the department number uses a sequence to populate that value instead. So depending on whether you supply two parameters or three parameters, you are going to either get the first one to execute or the second one to execute.

Now, I should mention this. You'll want to be careful when you have overloaded subprograms. Let me show you what I mean.

So what if I set up a default? What if in my package specification I set up a default on the ID, and what if I set up a default on the name? Let's compile that, and let's go and do the same thing in the body.

And I tell you what, I'm going to just-- you see the error message, "Default value of parameter pid and body mismatch that of spec." So I got this when I put in the wrong procedure.

[LAUGHS]

So this one's going to be-- I wasn't paying attention to the type. That one should be numeric. And this one down here should be Nina. I forgot all about that other subprogram.

[LAUGHS]

I tell you what, this is one of those occurrences where I to-- guess I did put it up here in this one, didn't I? Sorry about that. So this get emp has a default of 100. This get emp has a default of Nina.

That's compiled. Let's compile the body again. There we go. So now, they're exactly the same.

So now, what happens, if I wanted to provide the name notation, let's do p name initialize to v val. I just want to double-check and make sure that that was the name of my parameter right-- p name, yeah, p name, and p name here as well. So now what's going to happen-- using the wrong assignment operator there. Sorry about that.

So now what's going to happen, because I'm not providing a value for the first parameter and both of those have a default setup, now Oracle is not going to know which one to go with. So that's going to cause a problem when I try to execute this. It's going to say, "Too many declarations of get emp match this call."

So that means that your signatures are now not unique enough because of the defaults to where Oracle knows which one to invoke. So you have to be a little bit careful of that when you have overloading. I just wanted to point that out.

If I remove this default, and if I remove that from this definition, now it's going to know which one to go, because only one of those has a default. And it's going to go with 100. Whoops, let me execute that again. There you go.

So it's going to go with the default in this case. So I thought it was worth mentioning, because you may not be aware of that kind of a situation. You may not know what that error message means when you get that. And since they're starting to talk about defaults here on these parameters, you'll just want to be aware of that situation.

So restrictions on overloading, you cannot overload standalone subprograms. You also cannot overload subprograms where the parameters differ only in the mode-- in, out, in, out. You also cannot overload subprograms whose parameters belong to the same family, respectively, and functions which return only in the return type but not the formal parameters.

So if you have a different function return type, that's not different enough. The parameters have to be different. And same family-- one's var char, the other one's var char 2-- same family, that's not going to cut it. So this is where they're telling us about that standard package that I was talking about, and this is the built-in package that has the to char function, the to number, the to date, all of those different definitions. So it defines the PL/SQL environment and declares types, exceptions, and subprograms, which are available automatically to every PL/SQL subprogram or every PL/SQL program.

So here's where they're showing you the signatures for the to char function, and this is really where you can see how we've overloaded those. To char function has a date parameter, or a number of parameter, or a date and a var char 2 parameter, or a number and a var char 2 parameter. So notice, that they say, most built-in functions in the standard package are overloaded.

So to char is not unique. Most of the other ones are overloaded as well, like the case expression, for instance. Now, a PL/SQL subprogram with the same name as a built-in subprogram overrides the standard declaration in the local context unless qualified by a package name. So if you built your own to char function, for instance, your local context version is going to override the declaration of the one built into the standard package, unless you put standard dot prefix.

Package Instantiation and Initialization-- packages are stored as schema objects. Packages are instantiated when referenced. And what that means is that the variable values that are initialized to the different subprograms, those are going to be assigned when referenced. Each application which references the package has its own instance, and the package is initialized whenever instantiated.

So let's show you an example of this. Here, we have a package specification. And remember that we told you to keep the specification simple. So we have a variable called v tax, which we have not initialized.

So we want you to initialize your variables. And so what we're doing is we're putting what we call an initialization block at the end of the package body, and that is going to run as soon as the package is referenced. And in this case, it's going to populate the value of the v tax variable. That runs first, and then anything that uses that v tax variable is going to be able to use whatever that rate value is that it's populated into.

Now, that initialization block has to be at the very end of the package body. And you are not allowed to put your own end on it, because the end taxes that you see here, that's the end of the package body. So the end of the package body is what ends your initialization block. So make sure that you don't put your own end after the initialization block.

And you can have as many of those-- you would have one begin keyword with as many SELECTs as you needed to initialize all of the variables that you wanted to initialize. And then the end of the package body would close out that initialization block. You will be doing that in labs, by the way.

Now, if you've created a function inside of a package, it's going to follow the same rules that you learned about with standalone functions. We can access those just like in Oracle-supplied packages. It's going to be package name dot function name. The package specification in the body should be compiled before using them in SQL statements in the current schema, and you have to identify the functions with the package name. So let's show you an example.

We have a function called tax inside of a package called taxes package. And when we want to use that function inside SQL, you notice we put the package name dot function name. And we're able to go ahead and execute that in the SELECT statement.

Managing Persistent Package State in a Session-- the package state, as we call it, refers to the values of the variables, the constants, and the cursors, which are part of the package. When a package is instantiated, its state is initialized. So when you call the package, its state is initialized.

The state of the package may change during application execution. A package without any members, that hold, a value is called a stateless package. Now, we can also put in the clause SERIALLY REUSABLE, and that allows your packages to manage memory better for scalability.

So we have different memory architectures. We have system global area. Now, that is a shared memory structure, and that has information of one database instance. All server and background processes use it. So system global area, that is your-- or SGA, as we call it, that is your memory that is allocated for your instance.

The user global area, so that is the memory area associated with a specific user session connecting with the database instance. And then we have the PGA, the Program Global Area. This is an unshared memory region that contains data and control information exclusively for use by an Oracle process. One PGA exists for each server process and background process.

So think about it like this. The system global area, that has elements that are potentially shared. And then the PGA, that is a memory area for your session, if you want to think about it like that.

So when we reference-- when we create a package and grant people the ability to execute against the package, there's only going to be one copy of the package in memory for all users. But even though we're all using the same elements inside of the package, because we have this PGA, we're allowed to have our own value associated with a variable in our session that is going to be different than a value assigned to a variable in another session or other object. So the serial reusable packages, what we're talking about here is what I was just talking about. The package state of a package is stored in the user global area for each user. Everybody has their own unique value stored in their own area.

The package state of a serially reusable package is stored in the system global area, which is the sharable area. So storing the package state in the UGA can limit the scalability of an application. So let's take a look at the persistence data packages. Let's show you what it behaves like by default.

We have two different users, one called Scott, and one called Jones. They are both using the same package that we were talking about in the last chapter, and that's the package called column package. And remember, that has a public variable called reset com. Or sorry, not a public variable, but that's got a subprogram called reset com.

Now, the public variable is called v standard com. You'll notice that both Scott has access to the standard com and Jones has access to the same variable, called v standard com, because they're using the same package. Well, Scott executes the reset commission subprogram and sets the commission at 0.25. So you'll notice that the public variable is set to 0.25 for Scott.

Now, when we took a look at that package in the last chapter, I mentioned that in order to have a valid commission, we check it to see if it falls between valid ranges. And a valid range is between 0.0 and 0.4, because it's based on what's currently in the table. Well, notice what Jones does. And by the way, that's where they're pointing out the 0.4 here.

They're saying, hey, you can go ahead and reset that variable as long as it falls between 0.0 and 0.4. But Jones puts a new employee into the table, an employee called Madonna, and sets the commission for Madonna to 0.8 in the table. So 0.8 becomes Jones' maximum commission value, which is different than Scott's maximum commission, right?

Now, Jones does not commit that. So Scott cannot see that new employee. So Scott's maximum commission is always going to be 0.4. But since Jones is the one that did the insert, Jones is able to use up to 0.8 for commissions. And in fact, Jones goes in and executes the com package and sets the commission to 0.5, which is valid for his session.

Scott goes in and tries to set the commission to 0.6, but that doesn't fall within his tolerable ranges. So he gets an error, "bad commission." Now, at 11 o'clock, Jones does it roll back. That rollback is going to undo that insert that he did at 9:30.

So his maximum commission drops back to 0.4. He then exits, and he comes back in, and he executes the commission package and sets a commission to 0.2. So what this is designed to show you is that although there are two users that are both using the same package, and the same procedure, and the same variable, they can have different values, because their values are stored in UGA, and they can have their own values associated with it.

Now, what we were talking about on the previous page, if you don't want it to behave like that, you can do a PRAGMA SERIALLY REUSABLE in the package specification. And those values will not be persistent for the life of the subprogram call in that case. So we're going to show you an example.

So what if I have two different subprograms that are both interacting with the same cursor? The default behavior is, when one subprogram executes against the cursor and uses up the first three rows, then the next subprogram is going to recognize that we've already used up three rows out of the cursor. It's going to be able to reference the same cursor pointer.

I'm going to demonstrate this. I am going to open up the code examples for Lesson 15. And I will copy this example. I'm going to modify it a little bit just so it'll make more sense for you.

And let me put this in a new worksheets and let me get rid of all of those extra comments there. And what I'm going to do, I'm going to create another function. And we'll call this next one. And then down here, the function next, I'm going to call this one next one as well.

Let me create the package spec. Let me create the package body. I'm going to go ahead and open up the cursor, and I'm going to pass in-- I'm going to consume the first three IDs out of the table.

Now, my pointer now points to the next row after 102. So if I use my other function, called next one, is going to start over at 100, or is it going to start over-- or is it going to start at 103? Default behavior is that it understands that the pointer has already advanced from 100 to 102. And when I execute that again with the other subprogram in the same package, you notice it starts at 103.

Then if I go back to the original next function, it's going to recognize that next one has consumed the next three rows, and it's going to start over at 106-- 106, 107, 108. So you notice how both subprograms in the package body are able to interact with the same cursor, and they're able to reference where that cursor pointer is pointing at. So that's what we call persistent state of a package cursor. And so you could put a PRAGMA SERIALLY REUSABLE clause in there in the specification if you didn't want the cursor pointer to be able to be referenced by the second subprogram, and in which case I could go ahead and revisit the same rows in the cursor.

Overloading subprograms in PL/SQL enables you to create two or more subprograms with the same name. That is true. It requires that the subprogram's formal parameters differ in number, order, or data type family. That is true.

It enables you to build flexible ways for invoking some programs with different data. That's true as well. It provides a way to extend functionality without loss of existing code, that is, adding new parameters to existing subprograms. And that's also true. So all four are true.

So you should have learned about overloading, forward declarations, initialization blocks, and managing persistent packaged data states for the life of a session. So we are going to have you do Practice 15, where you're going to work with packages. You're going to use overloaded subprograms.

You'll create a package initialization block. You're going to use a forward declaration. So let's go ahead and have you guys do the practice, and this I'll do it for the demonstrations for Chapter 15.

## Practice 15-1: Working with Packages - New - 37m

I will now demonstrate practices for Lesson 15, Working With Packages. In the overview, we see that in this practice you modify an existing package to contain overloaded subprograms, and you use forward declarations. You also create a package initialization block within a package body in order to populate A PL/SQL table. Now, we do recommend that you run the cleanup15.SQL script before you begin. And what I'll do is-- I have been doing in the past-- I'll go ahead and start with the solution, which in my case, is on about page 7.

And we see that in this practice you're going to modify the code for the emp package package that you created in the last chapter, and then you're going to overload the add employee procedure. You're going to create two overloaded functions, called get employee, in the emp package package. You also add a public procedure to emp package to populate a private PL/SQL table of valid department IDs, and modify the valid dept ID function to use that private PL/SQL table and the contents in order to validate department ID values. You also change the valid dept ID validation processing function to use the private PL/SQL table of department IDs. Finally, you reorganize the subprograms in the package specification and the body so that they're in alphabetical order.

So in number one, you're going to modify the code for the emp package package. So I'm going to go ahead and go into my packages, and I'm going to go ahead and click on my specification. I'm going to add a new procedure, called add employee, that accepts the first name, the last name, and the department ID for my parameters. So what I'll go ahead and do is go in and add this definition into my package specification, and I'll go ahead and add that right after my other add employee subprogram.

So right here on about number 11, line 11, I'll go ahead and place that definition of that overloaded add employee procedure. You'll notice they're the same name, but the parameter lists are different. Now, next, on page 8, we'll go ahead and compile this by clicking on the Compile button and just check to see if it compiled with any errors. It looks like it compiled successfully.

So next, what we'll do is we'll go into the package body. And you'll notice that the package body is invalidated there. So that's what I'll do next.

I go ahead and click on the Package Body. Just make sure it says package body right there. And what we're going to do is we're going to put in the logic for that overloaded add employee procedure.

What we want to do is format the email address in uppercase characters using the first letter of the first name concatenated with the first seven letters of the last name, and the procedure should call the existing add employee procedure to perform the actual insert operation using its parameters and formatted email to supply the values. And then we'll click the Run Script button to create the package body and compile the package. So as I'm scrolling in through the code in the solutions, you'll notice that we add that new overloaded add employee procedure.

Here's where we're editing the email. The parameter called p email is going to be initialized to the first character of the first name concatenated to the first seven characters of the last name. It's going to be in uppercase. And then we're going to call the other add employee procedure in order to handle those other input parameters.

So I will go ahead and copy that logic, and we will add this just above the get employee procedure. So we'll go ahead and do that on about line 38. And then we will go ahead and compile it and make sure it compiles successfully.

Next, we'll close it, and we'll go ahead and invoke the add employee procedure. And we'll use the name Samuel Joplin. So let me go ahead and demonstrate that.

We will execute the emp package package and the name of the procedure, which is the add employee. And we use Samuel Joplin in department 30. And I'm going to clear out my messages log, and I will go ahead and execute, and it looks like it has successfully completed. So next, what we'll do is we'll double-check the employees table, and we'll click on the Data tab. And just make sure that you see Samuel Joplin, and make sure that that email address is created according to our needs.

So number two, in the emp package package, create two overloaded functions called get employee. In the package specification, we'll add a function, called get employee, that accepts a parameter, called p emp ID based on the employees.employeeIDpercenttype, and the function should return the employees percent row type, and then a second function, also called get employee, that accepts the parameter called pfamilynameofemployees.lastnamepercenttype. So you'll notice that with these two functions they have different types for the parameters. Now, they both return the same type, but the parameters are going to be different types.

So let's go back to the package specification. We'll go ahead and click on that, and we're going to go down and add the two function signatures. And we're going to add that just before the end of the package specification, just before the end emp package. And we'll go ahead and compile.

It compared successfully. The body did become invalidated. And next, what we'll do is we will go into the package body and add the implementation for both of those get employee functions.

So this one here, we're going to provide the employee ID, and we're going to return the record from the function. So we're going to return the whole row for whatever employee ID we pass in through the parameter. And again, on this one we'll add that just before the end of the package body. And let me go ahead and copy the second get employee function.

So let's just double-check and make sure that the functions make sense. Here's the first one. We're passing in the employee ID. We're going to return the employees percent row type.

We have a record based on the employees percent row type. We're selecting a row into that record from the employees-- where the employee ID matches the input parameter. And we're going to return the record. So that one uses the employee ID.

And then the next version uses the family name instead. Otherwise, the logic is really similar. So let's go ahead and compile it, and make sure that the package body compiles successfully. It looks like it compiled fine.

And then what we'll do is add a procedure, called print employee, to the package that's going to accept the employees percent row type as a parameter. And the procedure displays the information for an employee on one line by using the DBMS output package. So what we're going to do is we're going to add the procedure called print employee. Our input parameter is a parameter that is of the employees percent row type, and we'll add that to the specification.

And I'll add that just before the end of my package again. Make sure that that procedure, called print employee, makes sense to you. Procedure print employee, a parameter called p req emp of the employees percent row type. Let's compile it.

And then in the body, we will go ahead and complete the logic. We're going to pass in the record as an input parameter, and then we're going to print out from the record all of the pieces of data stored inside of the fields. So let me go ahead and copy the first part of that procedure into my package body. And again, I'll do that towards the end of the package body.

And then really simple to go ahead and print that out using the DBMS output package. There we are. Print employee, we have a record that's coming in through the parameter, and then we're going to go ahead and print out all the pieces of data from the record.

So let's go ahead and compile that body. And make sure that it compiles successfully. Next, what we'll do, step letter G, we'll go ahead and use an anonymous block to invoke the get employee function using employee 100 and a family name of Joplin. And we'll use the print employee procedure to display the results for each row returned.

Make sure that you use the server output on command. So I'll go ahead and copy that, and we'll do that into the new worksheet. So we're going to use print employee. We're going to pass in employee 100, and then we're going to use print employee by passing in the last name instead. And when we run that, you'll notice that we get Steven King based on the employee ID coming in, and then we're getting back Samuel Joplin based on the name Joplin going in.

So onto step number three. Because the company does not frequently change its departmental data, you can improve the performance of your emp package by adding in a public procedure. We're going to call this init departments. It's going to populate a PL/SQL table of valid department IDs. So we're going to create a collection.

We're going to modify that valid dept ID function to use the private PL/SQL table in order to validate the department ID values. So in the package specification, we're going to create a procedure called init departments, and we're not going to have any parameters for that one. So that's going to be really easy-- procedure init departments for the specification. And we're going to do that one just before the print employee procedure.

Now, in step letter B, in the body we're going to implement the init department's procedure, which, by the way, means we're going to compile the package specifications so that we can go add it to the body. We're going to create the index by table named valid departments, which is going to contain Boolean values. So what we're going to do is we're going to define the index by table, and we'll do that in the package body just before we create the valid dept ID function. We have type Boolean tab type is table of Boolean index by binary integer, and then here is our index by table of the Boolean tab type.

Next, we'll use the department ID column value as the index in order to create the entry in the index by table to indicate its presence and assign the entry a value of true. Enter the init department's procedure declaration at the beginning of the package body, and that's going to be right after the print employees procedure. So we'll go ahead and do that procedure, init departments, copy, and we'll do that right after the print employees subprogram. So we will do that right here, line 90 in my case, and that's where we'll add the procedure.

Now, in the body, we're going to create an initialization block that call the init department's procedure. And that's going to go just before the end emp package part of the body. So we'll go ahead and begin, and we'll invoke init departments, and we'll do an end.

And let's take a look at the rest of the code. So there is our procedure, init departments, and then that one is going to loop. Valid departments initialize to the department ID come in from the record, and then we're going to call the init departments procedure.

We'll go ahead and compile the body. And it looks like I ran an error. So let's just take a look at what's happening here.

Let me recompile. And we encountered this symbol and on line 100. That's what it's complaining about. So let me just go back and compare, double-check my specification, by the way.

There's my init departments procedure. Let me recompile that. That's what we're talking about there.

And then the package body, and let's just scroll on down to the end of the package body. So that is going to be emp package. I'll just double-check to make sure I've got the right components here-- add employee, insert into employees, procedure get employee, function get employee, function get employee.

Here's the function get employee that they're talking about there, procedure print employee, and right after that we have our procedure, init departments. Begin for req and select department A from departments, and loop in. I think that looks good. And then we'll call the begin.

Now, I tell you what, I see what the problem is. So up in the code, I thought they had you add another end. Let me see where that was.

No. I guess I misread the book. So I knew what the problem was.

So this is an initialization block. And so within initialization block, you're not allowed to use it's own end keyword. Instead, we'll use the end from the package body to terminate that initialization block.

So it looks like that's what the error is going to be. So let's just go ahead and recompile it. For some reason, I thought the book told me to put an extra end there. And I thought that was going to be for a learning experience, by the way.

Sometimes we'll have a compile and throw an error on purpose just to have a teachable moment. And so there you go. You see that compiles successfully.

Next, we're going to change the valid dept ID validation processing function to use the private PL/SQL table of department IDs. So we will go ahead and locate the valid dept ID function. It's going to be at the very top, by the way, and there it is right there.

So we want to use this valid departments index by table in this function. So we're going to go down, and we're going to put the return valid departments stat exists along with the input parameter value for the index. So rather than do this, select one, and do v dummy from departments, where department ID equal p dept ID. We are going to paste this little chunk of code.

Function val dept, valid dept ID rather, passing in the p dept ID, returning a Boolean. We have the v dummy variable still. Here, we're going to do the begin, and then we're going to return whether or not that department exists. So let's go ahead and compile that, and it looks like it compiled successfully.

Next, in letter B, we're going to test our code by calling the add employee using the name James Bond. So let's go ahead and do that. We'll go ahead and execute the emp package package. The name of the subprogram is going to be add employee, and we're going to add in James Bond.

We're added department 15. Now, we know department 15 is not a valid department, so I'm expecting we'll get an exception in this case, which we do-- invalid department ID. So in step letter C, we will insert a new department. And we'll actually add department 15 for the department ID and security for the department name. Let's go ahead and do that.

We'll just go ahead and add that missing department. Insert into departments. Value is 15, and security, and we'll make that a committed change. And next, we'll go ahead and call the add employee procedure again with James bond and department 15.

And let's go ahead and run it. And you notice that we still get an invalid department ID. So the insert operation to add the employee fails with an exception. Department 15 does not exist as an entry in the PL/SQL associative array, and that's because we have not executed the init departments procedure in order to add that new department to our index by table.

So that's what we're going to do next. Execute the emp package and it departments, and that's going to populate our index by table with the new department of value. And then we'll go ahead and try with James bond again there in step letter F.

Let's see. Raise the output. And this time, you notice that it succeeded. And here is where they're telling us, that in the book it says, the row is finally inserted, because the department 15 record exists in the database, and the packages PL/SQL index by table has been invoked, which refreshes the package state data.

Step letter G, we're going to go ahead and delete that employee that we just added. And so let's do that. Delete from employees where first name equals James and last name equals Bond, and delete from departments where department ID equal 15, and commit. And then let's go ahead and call the init departments so that we can update our list of valid department IDs.

Now, on page 33, we're going to reorganize the subprogram so that they are in alphabetical sequence. So let's go ahead and do that. Let's go back to the package body.

And I think what I'm going to do is put a little line break in between these different set programs so that I can visually see where the end of each subprogram happens to be a little easier. And here's my function. There's my procedure.

So init departments H, I, J, K, L, M, N, O P, so this one's going to have to go. Let's cut it, and let's put that before the print employee. So I think that's going to alphabetically be correct-- G, H, I, J K, L, M, N, O, P. Yeah.

Let's take a look at the get employee, get employee, add employee, add employee. So those should be towards the top. Valid dept needs to go at the bottom. So let's cut that one, and let's move that clear to the bottom of the list of subprograms.

And then what I'm going to do, I'm just going to collapse all of these different subprograms just to make sure that there are in alphabetical order and to make it easier to look at them. And there we go. Add employee, add employee, get employed, get employee, get employee, init departments, print employee, and finally, valid dept-- so everything is alphabetical.

And let's go ahead and compile this. And you'll notice we get an error message that says, "Valid dept ID not declared in this scope." So what that means is that we have no visibility on that subprogram, because that's a private subprogram. The val dept ID function is only in the package body.

So what we can do is we can add a forward declaration in our package body. I'm going to copy that, and I'm going to add this just after my index by table definitions. And that's going to be my forward declaration for the valid dept ID function. And let's go ahead and compile the package body. And this time, it compiles successfully.

Now, if I expand my package body, you'll notice that I have the forward declaration here. And then you notice that I'm actually using the valid dept ID later on further down. So we've taken care of that scoping problem. We've added this element to the top of the package body, which then allows us to be able to successfully compile our package body.

OK, my friends, so I am going to go ahead and close my package body. I'm going to go ahead and close my package specification. It looks like everything is compiled successfully, and I think I'm going to go ahead and close out my extra worksheets. OK, my friends, so that is going to do it for the demonstrations for Practice 15.
