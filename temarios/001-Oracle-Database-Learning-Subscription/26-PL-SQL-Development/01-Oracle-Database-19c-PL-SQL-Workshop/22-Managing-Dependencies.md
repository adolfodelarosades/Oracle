# 22: Managing Dependencies

* Managing Dependencies - New - 28m
* Practice 22-1: Managing Dependencies in Your Schema - New - 14m

## Managing Dependencies - New - 28m

OK, my friends, let's take a look at lesson 22 on managing dependencies. Here we are, very last chapter of the last unit number 6 on managing dependencies. The objectives-- after completing this lesson, you should be able to track procedural dependencies, predict the effect of changing a database object on procedures and functions, manage procedural dependencies, and manage local and remote dependencies.

So first up on the agenda, schema object dependencies. So what are dependencies in a schema? So a dependency refers to a situation where one schema object depends on another object for its definition. Some examples are-- there is a dependency between a view and the set of tables on which it is defined. And there is a dependency between the procedure and the tables on which the procedure is defined.

Now, if I go out to my database, and if I click on my EMPLOYEES table, for instance-- we've gone in and we've created several different objects that refer to the EMPLOYEES table. So we actually have a Dependencies tab right here that we can click on. And that's going to give us a list of all of the objects that refer to the EMPLOYEES table.

Now, all of these objects may have other objects that refer to them. So maybe my procedure called SAL_STATUS actually has another procedure that calls it. And so we might have this complex set of dependencies, where SAL_STATUS is dependent on the EMPLOYEES table. But then the procedure that calls SAL_STATUS might be indirectly dependent on the EMPLOYEES table as well.

And so we've got directly dependent objects, and we've got indirectly dependent objects. So this list here that you're seeing, this only shows directly dependent objects on the EMPLOYEES table. So we will show you how to get a list of indirectly dependent objects as well.

OK, so as an example, they're going to create some views in the HR schema. They create a view called COMMISSIONED, which is a query against the EMPLOYEES table. And then they create a view which is also dependent on the EMPLOYEES table. Now, when you go into the USER_OBJECTS view, you can see that both of those objects are marked as a status of VALID, meaning that when we created the two different views, they were dependent on the EMPLOYEES table, and that dependency is VALID.

OK, now let's go into the EMPLOYEES table and modify one of the columns. Now, notice how one of those views is marked as INVALID. And that's because the EMP_MAILS view is dependent on the EMAIL column from the EMPLOYEES table. And so after the EMAIL column in the EMPLOYEES table is modified, the status of the EMP_MAILS view has become INVALID because it's dependent on something that's changed in the EMPLOYEES table.

So we've got this concept of an object can be a dependent of another object, and that object is a referenced object by a dependent object. So in the last example that they were showing us here, the EMPLOYEES table would be the referenced object. The views called COMMISSIONED and EMP_MAILS would be the dependent objects.

So we have the USER_DEPENDENCIES view, where you can go in and query the USER_DEPENDENCIES view in order to see what are dependents on the objects that we have in the WHERE clause. So we're looking up dependencies on EMPLOYEES and also on a view called EMP_VW.

And you notice that it shows us the list of objects which are dependent upon-- in this case, we only get a list of objects that are dependent on the EMPLOYEES table because the view itself does not have any dependent objects on it. And by the way, what we're seeing here is what I'm seeing here when I click on the Dependencies tab. That's where that query comes from.

Now, when you go in and query an object status, every database object has one of the following status values-- it's either VALID, which means the object was successfully compiled by using the current definition in the data dictionary. Or COMPILED WITH ERRORS-- that means the most recent attempt to compile the object produced errors. That could be a coding error, for example.

INVALID-- the object is marked INVALID because an object that it references has changed. Only a dependent object can be invalid. Or UNAUTHORIZED-- an access privilege on a referenced object was revoked. So only a dependent object can be unauthorized.

So I created a view on a table in my schema. The table happened to be in another schema. The owner of that table revoked the permissions. So all of a sudden, my view would be unauthorized because the permissions were revoked.

They also have categories of dependencies. We have local dependencies, where both the referenced and dependent objects are on the same database. Oracle is going to manage them automatically.

There are two types of dependencies in local dependencies using the internal tables-- direct dependencies and indirect dependencies, as I was starting to talk about. We also have remote dependencies. That's where the referenced and dependent objects are on different nodes across the network. Oracle database is going to use different mechanisms to manage remote dependencies depending on the objects involved.

So let's take a look at direct and indirect dependencies. When a view is defined on a table, there is a direct dependency of the view on the table. Direct dependents are invalidated only by changes to the referenced objects that affect them.

So in the example, we have a table. We created a view on the table. Then we went back to the table and changed the EMAIL column. And it invalidated the view because that view is a dependent of the table.

And then we have indirect dependencies. This is where we have another object that is not directly dependent on a table, for instance, but indirectly dependent on the table because of its relationship to the object that is directly dependent to the table. So what they're saying here is, consider a PL/SQL program unit dependent on a view, which in turn is dependent on a table. The PL/SQL program unit is indirectly dependent on the table.

Indirect dependents can be invalidated by changes to the referenced object that do not affect them. The PL/SQL unit may be invalidated if there is a modification to the table. So if we go in and modify the table, the view and the PL/SQL unit might become invalid.

OK, so how do we display direct and indirect dependencies? There is a script called utldtree.sql. And this script creates the objects that let you display direct and indirect dependencies. This is where that script is in our labs. This script is in the DBA directory.

So I'm going to show you how to do this. What it does is, this script creates four objects. It creates a table called deptree_temptab. It creates a procedure called deptree_fill. It creates two views, deptree and ideptree, where we go in and select and format dependency data from the populated table.

So let me show you how this works. So I am going to go and open up my plpu, labs. And we've got the utldtree.sql script.

What I'm going to do is, I'm going to run this in ORA61 under my connection. This is your success message, by the way. When it says "View IDEPTREE created," that means it ran.

And then up at the top of the script, by the way, it gives you some examples of how to use this. So I'm going to copy lines 15 and 16 and again copy that into Myconnection worksheet. And what I'm going to do is, I'm going to change the name of the table to EMPLOYEES, and the name of the schema is ORA61. And I'm going to go ahead and run the EXECUTE.

And then I'm going to run this SELECT from the deptree. Deptree is short for dependency tree, by the way. And it's going to show me all of my objects that are dependent on the EMPLOYEES table if it is a level 1 object. That means it's directly dependent on the table.

Let me go in and create something else. I will create something that calls get_employee. Let me do that-- create procedure execute_emp. And we'll call that is, begin. And we'll pass in-- let's do get_employee.

And this one has a parameter. So let's see what this one has. I forget my parameter list-- P_EMPID. I get back P_SAL and P_JOB. So I'm going to have to have a couple of variables here-- v_sal number and v_job varchar2 25. And we'll do v_sal and v_job. And then we'll do an end.

OK, simple procedure. And oh, I forgot I also need to do employee ID. So I need three parameters for that one. OK, this one, PLW, it's a warning, so I don't have to worry about that one.

OK, let's go ahead and re-execute the deptree_fill procedure. And let's go ahead and select from the deptree view. And that was a procedure called execute_emp. There we are.

So you notice how I have a nested level of 2. So this is an indirectly dependent object on the EMPLOYEES table. Everything that's a level 1 is directly dependent. Level 2, indirectly dependent.

Now, if you'd rather see this a little bit different, there is a view called ideptree. And that stands for indented dependency tree. And that'll give you a more visual look.

That looks kind of like an org chart, right? Here is my base object. Everything that is indented one tab level is directly dependent on that object. Anything that's indented further is indirectly dependent.

So that allows me to visualize how my dependencies are organized upon my EMPLOYEES table. So in the event that I'm planning on making changes to the EMPLOYEES table, I probably better go in and see what other objects might get affected. And this allows me to do that.

OK, so that's what the utldtree.sql script does. We run the utldtree.sql script. Then we execute the deptree_fill procedure with the parameters. And then we select from the deptree view.

Now, fine-grained dependency management-- so what this is talking about is, starting in 11g, we rewrote the dependency mechanisms, and things become invalid less often. So that's what they're talking about here. It's only going to make an object invalid if it truly should affect it. So if we create a view on a table, and then we go and add a new column to the table, the view is not going to become invalid because the view never referenced that column in the first place.

So they're showing us an example of this. They create a view on the EMPLOYEES table, actually two views on the EMPLOYEES table. Both of those objects are marked as VALID. We changed the EMAIL column, which one of the views is dependent on. And that becomes invalid.

But as I was saying, starting with 11g, dependencies are now tracked at the level of element within the unit. Element-based dependency tracking covers dependency of a single-table view on its base table and dependency of a PL/SQL program unit-- specification, the package body, or the subprogram-- on other PL/SQL program units, tables, and views. So in a nutshell, things become invalidated less often.

To show you this, we are creating a table and then a view based on that table. That view is marked as VALID. We add a new column to the table. The view is still marked as VALID.

Now, here we actually go in and modify one of the columns that was referenced by the view. That's still going to make that column invalid-- or that view invalid. Because that view was dependent on that column.

Here we create a package, we create a procedure. We recompile the procedure, or the package rather. And it looks like procedure p is packaged at proc_1. We compile everything. And the procedure p is not marked as INVALID because it never referenced the unheard_of procedure originally. So it would still be marked as VALID.

OK, guidelines for reducing invalidation. To reduce invalidation of dependent objects, add new items to the end of the package. Then when you recompile the package, everything is revalidated. Reference each table through a view because of the fine-grained dependency management. They're going to be invalidated less often if you reference each table through a view.

Now, object revalidation happens automatically when an object is referenced. Now, an object does have to be validated before it can be used. So revalidation may not happen automatically if the object is compiled with errors, if the object is an unauthorized object, if the object is an invalid object, or if something is a remote dependent object. So Oracle does not manage dependencies among remote schema objects other than local procedure-to-remote procedure dependencies.

So we have different mechanisms for managing remote procedure dependencies. We have timestamp checking, and we have signature checking. Timestamp is the default. Let's show you what that is all about.

Now, by the way, if you wanted to change the behavior, you can either do a system-level change or a session-level change. Or you can change this in your init.ora parameter, your parameter list. ALTER SESSION SET REMOTE_DEPENDENCIES_MODE equal TIMESTAMP or ALTER SESSION SET REMOTE_DEPENDENCIES_MODE equal SIGNATURE. If the REMOTE_DEPENDENCIES_MODE is not specified either in the init.ora parameter file or by using the ALTER SESSION or ALTER SYSTEM DDL statements, TIMESTAMP is the default.

So let's show you what timestamp means. We have a procedure that is a remote procedure called B that compiles and is validated at 8:00 AM. We have a local procedure called A, which is dependent on the remote procedure called B.

When we compile local procedure A, it records the timestamp of B. So the timestamp of B is 8 o'clock. The time stamp of A is 9 o'clock. Everything is marked as VALID.

Then the remote procedure B is recompiled and validated at 11:00 AM. Now, when we go to execute procedure A, it still thinks that the timestamp for the compilation of B should have been 8 o'clock. And that's where it discovers that the timestamp has been changed, and that it's no longer 8 o'clock for the timestamp. So local procedure A is invalidated, and it'll raise an exception.

So if you don't want to use timestamp, you can use signature checking. The signature of a procedure is the name of the procedure, the data types of the parameters, the modes of the parameters. The signature of the remote procedure is saved in the local procedure. When executing a dependent procedure, the signature of the referenced remote procedure is compared.

So revalidating your PL/SQL program units-- you revalidate a PL/SQL program unit by recompiling it. There are two ways of recompiling. Implicit runtime recompilation-- that's only done when there are local dependencies, and that's done automatically. Or you can use explicit recombination using the ALTER statement-- ALTER procedure, ALTER function, ALTER trigger, ALTER package-- and then compile the object.

Now, you might get unsuccessful recompilation in some cases. For instance, when the referenced objects are compiled with errors. Or if those objects are dropped or renamed.

Or if the data type of the referenced column is changed, or that referenced column is dropped. If a referenced view is replaced by a view with different columns. If the parameter list of a referenced procedure is modified.

You'll get successful recombination if the referenced table has new columns, if the data type of the referenced columns has not changed. If a private table is dropped but a public table that has the same name and structure exists. Or if the PL/SQL body of a referenced procedure has been modified and recompiled successfully. So you can minimize dependency failures by declaring records with the %ROWTYPE attribute, declaring variables with the %TYPE attribute, querying with the SELECT star notation, including a column list within INSERT statement.

Now, with packages, if you have a standalone procedure, and you're calling that from inside of a package, if you go in and change the standalone procedure, the package is going to become invalidated. Or vise versa, if you have a standalone procedure that invokes something from a package, and the package definition has changed, the procedure will be invalidated. So what we want you to do is to maybe consider, instead of having that standalone procedure, maybe adding that standalone procedure as one of the subprograms in your package body. And then when you recompile the package body, it recompiles everything and revalidates everything. And that would solve that problem.

OK, that brings us to a quiz. "You can display direct and indirect dependencies by running the utldtree.sql script, populating the DEPTREE_TEMPTAB table with information for a particular referenced object, and querying the DEPTREE or IDEPTREE views." And that's going to be true. OK, so that's going to do it. The summary is, you should have learned how to track procedural dependencies, how to predict the effect of changing a database object on procedures and functions, how to manage procedural dependencies, and how to manage local and remote dependencies.

So we do have a final lab for you, practice 22. You're going to use the DEPTREE_FILL and IDEPTREE to view dependencies. You're going to recompile procedures, and functions, and packages. OK, so that will do it for the chapter.

This will be the final chapter for the course. And we hope that you enjoyed this course. And let us know if you have any questions, OK? Thank you very much.

## Practice 22-1: Managing Dependencies in Your Schema - New - 14m

I will now demonstrate practices for Lesson 22 on managing dependencies. In the overview, we see that, in this practice, you use the deftree field procedure and the ideftree view to investigate dependencies in your schema. In addition, you recompile invalid procedures, functions, packages, and views. Note that, before starting this practice, we recommend that you run the cleanup22.sql script.

I will start down here at the solution page 5, and what we're going to do is create a tree structure showing all dependencies involving your add employee procedure and your valid dept ID function. So what I'm going to do is just double check and make sure that I have my add employee procedure, and you notice I do, right there. And I'm also going to check to see if I have my valid dept ID function, and it looks like I have that as well.

Now, we had created those back in practice 12, and so if you didn't actually create those, then we provide the syntax for you there on the page to go ahead and copy and paste in to create those objects. Next, we want you to load and execute the utldtree.sql script, which is located in the home Oracle labs PLPU labs directory, so let me go ahead and locate that. There you are-- home Oracle labs PLPU labs utldtre.sql. We'll go ahead and open it, and then we're instructed to go ahead and execute that in our My Connection window by running it as a script.

And we get back the messages that the ideftree view was created, and that's the final message. So let's just compare that to the book, and it looks like it has completed successfully. If you end up seeing a number of error messages, you can go ahead and ignore those error messages as long as you see that these structures were actually created.

So coming up now on page 12, everything up until page 12 was just showing you the screenshots of the utldtree.sql script and showing you it executing. So we're going to go with letter B on page 12, where we're going to execute the deftreefill procedure for the add employee procedure. So let me go ahead and open up a new worksheet, and I will execute the deftreefill procedure. And we are going to reference a procedure.

The user-- this is going to be Ora61 for me, and then the name of the procedure is add employee. And let's go ahead and execute that, and it tells us the PL/SQL procedure was successfully completed. So let me just scroll over and make sure that you can see all of the parameters there. Next, we are instructed to select star from ideftree, and there you go. The dependencies are showing just procedure ora61.addemployee.

Next, we're asked to go ahead and execute the deftreefill procedure again, and this time, we're going to do that for the valid dept ID function. So let's go ahead and paste that there. Again, we're going to use the user of Ora61.

So user is actually a function, and you could either hard code the user name, like I did the first time, or you could go ahead and use the user function, which is going to capture what user you're connected as. So whatever method you prefer will be fine. And then what we'll do is, again, select from the ideftree view, and this time, notice that the procedure ora61.addemployee is a dependent of the function ora61.validdeptid.

So continuing on with step number two, we are going to dynamically validate invalid objects. We're going to make a copy of our employees table called emps, so let me go ahead and just copy that real quick. And I'm going to right click my tables and just refresh so that I can see my emps table there. Next, what I'll do as I will alter my employees table, and I'll go ahead and add a new column to that.

Now, because the emps table was created as a copy of the employees table, and then we added the new column to the employees table, the emps table no longer matches the structure of the employees table. So let's go in and check and see whether or not we have any invalid objects. Select object name, object types, and status from user objects where the status equal invalid, and you notice that I happen to have quite a few different objects which are marked as invalid.

Now, step letter D. In the compile package, which we created in practice 17, we're going to add a procedure called recompile that recompiles all invalid procedures functions and packages in your schema. We're going to use native dynamic SQL to alter the invalid object type and compile it. So I'm going to go ahead and bring up the package called compile package that we created. There we are. And I'm just going to make sure that we have a procedure called recompile.

So I'm going to just put the signature of that inside of my specification. I will recompile my spec, and then what I'll do is I'll open up the package body, which is now invalidated. And I will make sure that I add the procedure called recompile, and I'll add that on about line 41.

And let's go ahead and recompile our package body just to make sure we don't have any errors. And next, we're going to execute the compile package recompile procedure. Now, before I do that, let's just remind you of all of the objects which are invalidated.

So next, what I'll do is I'll go ahead and execute the recompile procedure inside the package that we just created, and then we'll go back and look at user objects to see if we have any invalid objects. So it looks like just my demo package body is invalid, so let's go take a look at that one. And I think what we'll do is just go ahead and recompile that and see if we have any errors or warnings. Looks fine. And we'll go back in and run our import, and it looks like we no longer have any invalid objects.

So how do we do that with the recompile subprogram? Well, let's go back in and look at the package body. We'll look at the logic, procedure recompile is. We're selecting the object name and object type from user objects, where this status is invalid and the object type is not equal to package body. So that's why my package was not revalidated, was because we explicitly were not looking for package bodies.

And then we're going to do an alter object type object name compile, and we're going to loop until we go in and recompile all the objects except for package bodies. And you saw in my output when I did that, that I had gone in and executed the compilepackage.recompile procedure, and it went in and ran all of these compilations. OK, my friends, so that is going to do it for the demonstrations for practice 22.
