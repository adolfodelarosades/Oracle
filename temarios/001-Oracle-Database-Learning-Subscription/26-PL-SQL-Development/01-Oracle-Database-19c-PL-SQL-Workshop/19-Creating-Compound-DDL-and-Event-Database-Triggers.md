# 19: Creating Compound, DDL, and Event Database Triggers

* Creating Compound, DDL, and Event Database Triggers - New - 14m
* Practice 19-1: Managing Data Integrity Rules and Mutating Table Exceptions - New - 14m

## Creating Compound, DDL, and Event Database Triggers - New - 14m

OK, my friends, let's take a look at lesson 19, creating compound DDL and event database triggers. We are here in unit 5 working with triggers in lesson 19. After completing this lesson, you should be able to describe compound triggers, describe mutating tables, create triggers on DDL statements, create triggers on system events, and display information about triggers.

So what is a compound DML trigger? So what if you wanted to create a before statement trigger, an after statement trigger, a before row trigger, and an after row trigger all on one object? And what if you wanted those all tied to the same set of events?

Well, you could create four separate triggers, or you could create a single trigger on a table that allows you to specify actions for each of the four timing points. So instead of having four triggers, I could have one sugar that has four timing points inside of it. Now you don't have to have all four. You can have any combination of them.

You could have a before each row, an after each row, and an after timing point. Each timing instance has an executable part and an optional exception handling section. And all of the timing instances access a common PL/SQL state.

So if you wanted to have something like an index by table or other type of collection, all of the timing points could access the common PL/SQL state. So when working with compound triggers, the compound trigger body supports a common PL/SQL state that the code for each timing point can access. The compound trigger common state is established when the triggering statement starts and destroyed when the triggering statement completes.

A compound trigger has a declaration section and a section for each of its timing points. The section of each timing point may also have an optional exception handling section. So some examples of why to use compound triggers. You can use compound triggers to program an approach where you want the actions you implement for the various timing points to share common data.

Or maybe you want to accumulate rows destined for a second table so that you can periodically bulk insert them. Or maybe you want to avoid the mutating table error. And that's the example that we're going to show you by the way. So when you create a trigger, if you want this to be a compound trigger, it does have to have the compound trigger keywords in it.

And we're going to show you some examples coming up here in just a minute. Now a compound trigger has to be a DML trigger defined on either a table or a view. If you have an exception that occurs in one section, you have to handle it in that section. You can't transfer control to another section.

A timing point section cannot handle exceptions raised in another timing point section. Old and new qualifiers cannot appear in the declaration in a before statement or an after statement section. Because remember, those are kind of tied to statement level triggers, and old and new are not used with statement level, so they have to be in the for each row sections.

And only the before each row section can change the value of the new qualifier. So I'm going to remind you of what a mutating table is. We looked at this when we looked at functions. We had a function that did an update, and we're calling that function from an insert statement, and that caused a mutating table error.

So that's what they're saying here. A mutating table is a table that is being modified by an update delete or insert statement, or a table that might be updated by the effects of a delete cascade constraint. The session that issued the triggering statement cannot query or modify a mutating table.

This restriction prevents a trigger from seeing inconsistent data. This restriction applies to all triggers that use the for each row clause. So if you're using views that are being modified by the instead of triggers, those are not considered mutating. So technically, the views themselves aren't always changing-- it's actually the base tables that are being changed with those.

So here is an example. We have a trigger that is called check salary. Before we update the salary or job, or before we do an insert of a new row on the employees table, we're again to check the job ID to see if it's the president or not.

If the new job ID is not AD_PRES, then we're going to go in and make sure that somebody's salary is within a tolerable range. We have a v_minsalary variable, we have a v_maxsalary variable. We're selecting the minsalary into v_minsalary, we're selecting the maxsalary into v_maxsalary for the job ID that's coming in.

And if the new salary is less than whatever the current minimum is or if the new salary is greater than the current maximum salary for that job, we're going to throw an error that says out of range. So when we try to update the employees to a new salary, it's going to take a salary and see if it's out of range. But that throws a mutating table error. We're updating the data. We can't query the same data that we're trying to update.

And so we're going to solve this problem with a compound trigger. So we put in the words compound trigger, and we're going to create some collections. And we have some collections that hold the minimum salaries and maximum salaries.

We have another collection of department IDs. We have another collection that holds department minsalaries and maxsalaries. And on the next page, we have a before statement section in the compound trigger, and we're using the before statement to go ahead and collect the minimum and maximum salaries into the minimum salaries and max salaries collections, and also into the department ID collection.

Now notice that we're grouping by the department IDs, so each department ID will have a minsalary and a maxsalary based on that group by clause. And then what we're going to do is we're going to initialize the department minsalaries and department maxsalaries collections using the department ID as the index and initializing that to the minimum salaries and maximum salaries for that department. so that's the before statement trigger-- populating a bunch of collections with the minimum and maximum salaries for each department.

Then what we're going to do is after each row, we're going to check the new salary. And if the new salary is less than the minimum salary looking at the department ID index value-- department 90, for instance, minimum salary would be $17,000. So if somebody is getting inserted into department 90 and their salary is less than $17,000, or if their salary is greater than the maximum salary for department 90 which happens to be $24,000, then we're going to raise an error that the new salary is out of acceptable range. So we're looking up those salary ranges in our collections that we populated with the before statement section of the compound trigger.

Schema triggers-- so we can create triggers on DDL statements. We can create triggers on create statements-- or create events rather-- alter events, and drop events. So here, we have a trigger that is preventing people from dropping objects. Before drop on or ora61.schema, raise application error-- you cannot drop an object.

So that one is a schema level trigger based on DDL events. Database triggers-- we might want to capture when somebody logs on, or when somebody logs off, or when somebody shuts down the database or starts up the database, a specific error, or any error that's raised. So notice the different database events-- after server error, after log on, before log off, after startup, before shut down.

So for example, we have a trigger called log on, or called log on trig, specifically. And this one is after somebody logs on the schema, we're going to capture the user that logged on, the time and date when it occurred, and the action of logging on into a log trig table. And then before we allow them to log off the schema, we have another trigger. Before log off on schema, we're going to insert into the log trig table the user, the sysdate, and the action of logging off.

Guidelines for designing triggers. You can design triggers to ensure that whenever a specific event occurs, any necessary actions are done. Of course, don't create triggers which duplicate the function of the database.

Don't create triggers which are recursive. So don't create a trigger which causes another trigger to fire, which causes another trigger to fire, which causes another trigger to fire, or which causes-- don't create a trigger that causes another trigger to fire, which in turn causes the original trigger to fire. So just be careful about how they're related.

And like I was showing you in the last chapter, you can create stored procedures and invoke them in a trigger if the PL/SQL code is very lengthy. That brings us to our quiz. Which of the following statements are true for a trigger?

A trigger is defined with a create trigger statement-- that is true. A trigger source code is contained in the user triggers dictionary view-- that is true. A trigger is explicitly invoked-- that's false.

[LAUGHS]

A trigger is implicitly invoked by DML-- that's true. Or by other events that they're defined on, Whether that's a database event or error. Commit, savepoint, and rollback are not allowed when working with a trigger-- that's true as well.

So you should have learned about compound triggers, mutating tables, triggers on DDL statements, triggers on system events, how to display information about triggers. And we're going to have you do a practice. You are going to create advanced triggers to manage data integrity rules.

You will create triggers that cause a mutating table exception, and you'll create triggers that use package state to solve the mutating table problem. So let's go ahead and have you do the practices for lesson 19, and [INAUDIBLE] the demonstration for lesson 19.

## Practice 19-1: Managing Data Integrity Rules and Mutating Table Exceptions - New - 14m

I will now demonstrate practices for Lesson 19, Creating Compound DDL and Event Database Triggers.

So in the overview, we see that in this practice you're going to implement a simple business rule for ensuring data integrity of employee salaries with respect to the valid salary range for their jobs. You create a trigger for the rule and during this process your new trigger causes a cascading effect with triggers created in the practice section of the previous lesson. The cascading effect results in a mutating table exception on the jobs table. You then create PL/SQL package and additional triggers in order to solve the mutating table issue. Before starting the practice, you should execute the cleanup 19 dot sql script.

OK. So I will start with the solution file on page 6, where we're going to manage data integrity roles and mutating table exceptions. So the employees are going to receive an automatic increase in salary if the minimum salary for a job is increased to a value larger than their current salaries. Implement this requirement through a package procedure called by a trigger on the jobs table. When you attempt to update the minimum salary in the jobs table and try to update the employee salaries, the check salary trigger attempts to read the jobs table, which is subject to change, and you get a mutating table exception that is resolved by creating a new package and additional triggers.

So we're going to have you update your M package package that you last updated in practice 9 by adding a procedure called set salary that updates the employee salaries and a procedure called set salary that accepts two parameters, one for the job ID for those salaries that may have to be updated, and the new minimum salary for the job ID. So what we're going to have you do is to go ahead and open up the solution, and we'll have you create that package with those changes. And it's going to be your solution 10. And we'll go ahead and create the package specification as well as the package body. So let me copy these into a new worksheet.

And here's our new set salary procedure, OK? Set salary. Passing in a job ID and the p minimum salary.

We have a cursor where we're selecting the employee ID for the employee's table. And then we're running through the cursor through a cursor for loop. We're updating the employee's table, setting the salary equal to the p minimum salary where the employee ID equals the employee ID coming from the record.

All right. So let me go ahead and create the package spec as well as the body. Looks like I just had part of it highlighted, potentially. There we go. We compiled the package specification as well as the package body.

Now, they're showing you the procedure called set salary here that I was showing you in the code. So that's in your specification. And then there is that procedure that we just pointed out in the code called set salary.

OK. Next, in letter b, we're going to create a row trigger named update min salary trig on the jobs table. That invokes the set salary procedure when the minimum salary and the jobs table is updated for a specified job ID.

So let me go in and create the trigger. Create or replace trigger update min salary trigger. After update of min salary on jobs, for each row, we're going to call the set salary procedure and we're going to pass in the new job ID and the new minimum salary. OK. And that compiled successfully.

Next, what we'll do is we will write a query to display the employee ID last name, job ID, current salary, and minimum salary for employees who are programmers. So their job ID is IT PROG. And then we're asked, then update the minimum salary in the jobs table to increase it by $1,000. And they're going to ask us what happens.

So let's go in and do the select. so it looks like our salaries fall between $9,000 and $4,200. Let's go in and update the jobs table and try to add $1,000 to the minimum salary, which is $4,200. And we end up getting the mutating table error.

So why do we get this? The update of the min salary column for the job IT PROG fails because the update min salary trig trigger on the jobs table attempts to update the employee salaries by calling the set salary procedure. The send salary procedure causes that check salary trig trigger to fire, which would cause this cascading effect. And the check salary trig trigger caused the check salary procedure, which attempts to read the jobs table data. While reading the jobs data, the check salary procedure encounters the mutating table exception.

So starting in set number two, we're going to resolve the mutating table issue by creating a jobs package package to maintain in memory a copy of the rows in the jobs table or a copy of the rows in the jobs table. We're going to modify the check salary procedure to use the package data rather than issue a query on the main table that is mutating. Therefore, we can avoid the mutating table exception. However, you must create a before insert or update statement trigger on the employees table in order to initialize the jobs package package before the check salary trigger is fired.

So let's go ahead and create that package. Here is our jobs package. Procedure initialized. We have function get min. salary, function get max salary. Procedure set min salary, procedure set max salary.

Basically, we're going to-- we're going to use this package in order to get the minimum maximum and salaries. And then we're going to get a function that's-- or create a function to get the minimum salary and a function to get the maximum salary, and a procedure to set the min salary and a procedure to set the max salary. And we're storing these things inside of an index by table. So let's go ahead and create that package body.

OK. Next, what we're going to do is we're going to create a procedure called check salary that then uses the v min sal and v max sal variable values. All right. So let's go ahead and do that.

And we've created our procedure called check salary. And check salary is going in, as I was saying, to check the values coming from the collections instead. And we're using those to populate our variables.

OK. So next, what we want to do is go in and-- no, I already did this step here, the check salary on step letter c, by the way. So we're now here on step letter d. We're going to implement a before insert or update statement trigger called ENIT JOB package TRIG that uses the call syntax to invoke the initialize procedure to ensure that the package state is current before the DML operation is performed.

So let's go ahead and create that trigger. OK. Create or replace trigger ENIT JOB package TRIG before insert or update on jobs call the jobs package dot initialize subprogram.

OK. Let's go ahead and test our code. We'll try it with a select. We'll try it with an update. We'll try it with another select. And I'll run each of these in a separate-- I'll run each of those separately is what I should say there.

We'll run this one first. Select employee ID, last name, salary from a place where the job ID equal IT PROG. There we are. Values range from $4,200 to $9,000.

Let's update the jobs table and try and add the $1,000 for IT programmers. You notice one row is updated. And that does give us the ability to go in and around our select statement. So in this case, we did go in and increase somebody's salary by $1,000.

OK. So that is going to do it for the demonstrations for lesson 19.
