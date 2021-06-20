# 18: Creating Triggers

* Creating Triggers - New - 34m
* Practice 18-1: Creating Statement and Row Triggers - New - 17m

## Creating Triggers - New - 34m

All right. Let's take a look at lesson 18 on creating triggers. We are here in unit 5, working with triggers, and we have two lessons in this unit. Lesson 18 is on creating triggers. Lesson 19 is on creating compound, DDL, and event database triggers.

OK. The objectives-- after completing this lesson, you should be able to describe database triggers and their uses, describe the different types of triggers, create database triggers, describe database trigger-firing rules, remove database triggers, and display trigger information.

Understanding the usage of triggers. Here we have Jack is saying, hey, Alice. I have a situation where I have to keep track of the amount of salary increase given to an employee whenever it is given. I can request the managers to update a certain table whenever they give a hike, but usually they forget about this. Can you automate this some way?

Alice says, I can definitely create something for this requirement. So friends, let's get to work. We have triggers in PL/SQL that can help us in creating something that the HR manager has asked for. First, let's look at some concepts.

So what are triggers? A trigger is a PL/SQL block that is stored in the database and fired or executed in response to a specified event. The Oracle database automatically executes a trigger when specified conditions occur. A trigger can be defined on the table, on a view, on a schema-- schema owner-- or the database, meaning for all users.

Why do you use triggers? So we might use a trigger for logging events, to gather statistics on table access, to modify table data, when DML statements are issued against views-- those are called instead of triggers, by the way-- and we might use them to enforce referential integrity constraints when child impairment tables are on different nodes.

Maybe to prevent DML operations on the table based on application requirements, to prevent invalid transactions, to implement complex business rules. Really, the list is endless on why do we want to use triggers.

So we have different trigger event types. You can write triggers that fire whenever one of the following operations occurs in the database-- DML statements tied to DELETE, INSERT, or UPDATE; DDL statements tied to CREATE, ALTER, and DROP; or database events, such as SERVERERROR, LOGIN, LOGOFF, STARTUP, and SHUTDOWN.

So available trigger types. We have simple DML triggers. We have before, after, and "instead of" triggers. Remember, "instead of" triggers are for views. We have compound triggers. And we're going to take a look at compound triggers in the next chapter. We have system triggers, which are DDL event triggers and database event triggers. We're also going to look at system triggers in the next chapter, as well.

So a trigger event type determines which DML statement causes the trigger to execute. The possible events are going to be INSERT, UPDATE, DELETE, and you can also tie it to updating of specific columns. Now, the trigger body determines what action is performed, and is a PL/SQL block or a call to a procedure.

So how do we create triggers? Well, I think what I will do is go in and give you a demonstration, and then we'll come back and take a look at the book. So what if I wanted to capture when somebody changes a salary? What if I wanted to capture that information in a log table of some sort?

So first, I would have to create the log table. So I'll create the table, salary_log. And I'll have whodidit, and that's going to be a varchar2 type. And I'll have a whendidit, and that'll be a timestamp type. And I'll keep track of the oldsalary-- that'll be a number-- and a newsalary, which will be a number, and emp_affected. And I'll do that as a number. That'll be the employee.

So that is going to be my create table. And next, I want to create a trigger on my employees table. So I'm going to create or replace trigger, and I call it saltrig.

And what I'll do is I'll say after insert or update of salary on employees, and then I'm going to make this a row-level trigger by saying for each row. So every time a row gets changed, I'm going to fire my trigger, assuming it's an insert or an update of the salary. So if a new row gets inserted, I'm going to track it. And if somebody updates the salary, I'm going to track it.

And what I'll do is I'll insert into the salary_log table. And I'll do the user function to capture the user that did it. I'll do sysdate to get the timestamp. I'll do colon old.salary. We call those qualifiers, by the way. Whenever you use a row-level trigger, you can use those old or new qualifiers. They will capture the former value or the new value. And then I'm going to do new.employee_id.

OK. So let me go ahead and create the trigger. My trigger is created. And now, let's go ahead and test it. update employees set salary=1 where employee_id=100. Whoops. I accidentally recompiled that trigger again, so let me recompile that again. And I forgot to put my PL/SQL delimiter there, so when I ran the update, it reran the create or replace trigger. There we go, 1 row updated.

So let's select * from salary_log, and you'll notice that it captured ORA61 did it. This is when they did it. OLDSALARY was $1. NEWSALARY was $1. And it was employee 100 that was affected. It didn't change by much, did it? Let's change that to 24,000. He'll be a lot happier with that salary. OK, 1 row updated. And you notice that it changed from $1 to 24,000 now.

One thing-- we're not allowed in a trigger to have a commit or a roll back. So the entry into my log table is going to be based upon whether or not I commit what happens to my changes. So if I come in and do a commit, then that row is going to be made permanent or those rows are going to be made permanent in that log table.

If I would have done a rollback on changing the salary, then it would have rolled back the entries in the log table, as well. So if I compiled that trigger with a commit, it'll let you compile it like that and you wouldn't know that it's going to cause an error until you go to make the change, and that's where you're going to get the error.

And that's where it says, hey, you cannot commit a trigger. So just be careful of that, since it does not throw an error when you compile it if you put that in there.

All right. So let's go back to the book. So the timing-- you saw me use an AFTER timing, after the row is changed or after the row is inserted. And the event is tied to an INSERT and an UPDATE of salary, in my case. It can also be tied to DELETE and UPDATE, as well.

You can create triggers by using SQL Developer. Right-click Triggers and click New Trigger. You get to choose what Table it's based on, what Schema it's in, the Timing, the Events.

Down here is where they have the Old and New, which are valid only for row-level triggers. Here, I've got a tick in the box for Statement Level, so that's going to run either before a statement executes or after a statement executes. Row-level triggers fire for every row that's affected. Statement-level triggers only fire once before a statement or once after a statement.

So here is where they're talking about the trigger execution time. You can specify the trigger timing as to whether to run the trigger's action before or after the triggering statement. BEFORE means to execute the trigger body before the triggering DML event on a table. AFTER, we execute the trigger body after the triggering DML event on the table. And "INSTEAD OF," execute the trigger body instead of the triggering statement. This is used for views that are not otherwise modifiable, and we'll show you an example of that.

Here we have an example of a trigger that checks whether or not you're inserting data into a table during business hours. If you're not doing it between business hours, the trigger is going to fire and it's going to not allow you to insert into the employees table. You notice the timing is before the insert. So if you get an error before the insert, you're not going to be able to do the insert, so you've got to be careful about the timing.

So if we're trying to do something on a Saturday or Sunday, or if we're trying to do something outside of 8:00 to 6:00 PM, we're going to get the error message. You can only insert into the employees table during normal business hours.

What if we wanted a different message for every type of DML? Custom error messages-- we'll show you how to do that here in just a minute. But here, we have somebody inserting into the employees table and it looks like they were not within the appropriate hours so they get back the error message. Whoops. This says, you may insert into employees table only during normal business hours.

OK. So this is what I was talking about. What if I wanted a custom error message, depending on whether they were deleting, or inserting, or updating? So here we're saying, hey, this is before an insert, or an update, or a delete. Again, the timing is before, and it's a statement-level trigger because we don't have the for each row.

And so if we were trying to DELETE, we're going to get a delete error. If we're trying to INSERT, we're going to get an insert error. If we're trying to UPDATE the salary, we're going to get an update salary error. If we're doing any other update, we get a general update error, where the employees table can only be updated during normal business hours.

What if you have multiple triggers that are fired by the same event and they are the same type of trigger? You can put either a precedes or a follows in your syntax so that you can control the order of the firing of your triggers. If you leave out the proceeds or follows, you may have a trigger that fires before another trigger this time, but the other trigger might fire first before the other one the next time.

So you do have to be careful about the trigger firing order in some cases, and so just keep that in mind when you have multiple different triggers tied to the same event.

What if you've written some logic in another language, like C or Java? Well, you could actually call those programs through a trigger. So here, BEFORE INSERT ON EMPLOYEES, we're calling a program called log_execution, which might be written in C, for instance. No semicolon is needed at the end. What it does is it passes control to that program and then that program finishes the execution.

Row-level triggers-- if we want them to be affected for every row that's modified, we have to add the for each row clause. Otherwise, it's a statement-level trigger. Statement-level triggers fire once, even if no rows are affected. Row-level triggers do not fire if the triggering event does not affect any rows.

So here we have Alice saying, in a situation where I have to log insertion of every row while inserting a bunch of 100 rows, I will use a row-level trigger. While creating the trigger, I add FOR EACH ROW in the syntax. Or in a situation where I have to check the date and time of insertion and then allow it if it is in a valid range, I will use a statement-level trigger instead.

Here we are. CREATE OR REPLACE TRIGGER restrict_salary. BEFORE INSERT OR UPDATE OF salary ON employees. FOR EACH ROW. So if the NEW.job_id is not AD_PRES or AD_VP, and if the NEW.salary is more than $15,000, then we're going to throw an error saying, hey, an employee cannot earn more than $15,000. So we try to update Russell's salary to 15,500 and we get the error message. So Russell must not be a president or vice president.

So OLD and NEW-- those are qualifiers, as I was mentioning. Correlation names are used to refer to values of a column before and after the trigger-firing event. We have three correlation names-- OLD, NEW, and PARENT. Pseudorecords refer to the values of the rows before and after the trigger-firing event when they're manipulated in the trigger body as a record. Pseudorecords are also referred to with OLD, NEW, and PARENT qualifiers.

So here we have an example of logging of an update operation by a logging utility in the database. While logging the update operation, the old value has to be written into the log table. This sounds exactly what I demoed, doesn't it? When you perform the log operation through a trigger, you have to refer to the value before the update. You can refer to the value after the update with the OLD qualifier, and the value after the update is referred with the NEW qualifier,

So that's what I demonstrated for you-- OLD and NEW. And these are only for row-level triggers. OLD stores the original value of the record processed by the trigger. NEW contains the new values. NEW and OLD have the same structure as the record that is declared by using the %ROWTYPE. So it's tied to the structure of the table.

So if I do this against the employees table, I can reference NEW and OLD on any of the columns in the whole table since they're tied to the same structure. And so you notice that we have INSERT, UPDATE, and DELETE operations; what the old value would be. So in my case, on an INSERT, the old value would be NULL, but the new value would be inserted value.

On an UPDATE, old would be the value before the update and new would be the value after the update. DELETE would be the value before the delete but we don't have a new value, so it's NULL.

And this is pretty similar to what I showed you here. We have a table called audit_emp. Looks like we're tracking the old_title, the new_title, old_last_name, new_last_name, user_name, time_stamp, id, old_salary, new_salary. So this one is tied to AFTER DELETE OR INSERT OR UPDATE ON employees FOR EACH ROW, and we're putting that into an audit_emp table. And we're using OLD and NEW for most of those column values.

They do have to have the colon in front of them, by the way, except for when they are above the BEGIN. I'll show you what I mean. So here, the NEW qualifier does not have a colon in front of it. We're basically only going to fire in the event that the NEW.job_id = 'SA_REP'. If the NEW.job_id is not SA_REP, then they don't make a commission. So if you reference the qualifier NEW or OLD before the BEGIN, then you don't use the colon in front of NEW or OLD.

This kind of visualizes the BEFORE statement trigger firing, the AFTER statement trigger firing, the BEFORE row trigger and the AFTER row trigger firing, and even more so on the next page. We've got six rows that are affected, so the BEFORE row trigger would fire six times, once before each row is modified. The AFTER row trigger would fire once for every row that's affected after every row that's affected. The BEFORE statement trigger would fire once. The AFTER statement trigger would fire once.

So the summary of the trigger execution model. We execute all the BEFORE STATEMENT triggers. We loop for each row affected by this equal statement. Execute all the BEFORE ROW triggers for that row. Execute the DML statement. Perform the integrity constraint checking for that row. And then execute all AFTER ROW triggers for that row. And repeat that multiple times, depending on how many rows are affected by the SQL statement. And then step number three, once we're all done, execute all AFTER STATEMENT triggers.

INSTEAD OF triggers. So these are tied to views. What if you don't want people to be able to modify data through a view? So instead of making a change to the view, the trigger is going to go in and make the changes to the base tables, instead.

So here, we're showing you, hey, INSERT INTO the view called emp_details. But instead of insert into the emp_details view, we're going to insert into the NEW_EMPS table and we're going to update the NEW_DEPTS table, which are the two tables that the EMP_DETAILS view is based upon. So here's their example. CREATE TABLE new_emps. CREATE TABLE new_depts. CREATE VIEW emp_details tied to both tables.

And then we don't have a slide for that, but let me show you what the INSTEAD OF trigger looks like. We didn't include a slide because they're kind of big. So let me go in and show you what that looks like. And I am going to open up-- so there is the INSTEAD OF trigger.

I'm going to put this into a new worksheet so you can see the code. And there you go. So CREATE OR REPLACE TRIGGER. Give it a name. Here's where it becomes an INSTEAD OF trigger. INSTEAD OF INSERT OR UPDATE OR DELETE ON emp_details view. FOR EACH ROW. IF INSERTING into emp_details, THEN INSERT new_emps table instead and UPDATE NEW_DEPTS table.

If you're DELETING, then DELETE FROM this table and UPDATE this table. If you're UPDATING the salary, UPDATE this table. UPDATE this table. If you're UPDATING the department_id, then UPDATE this table. UPDATE this table. Go back and UPDATE this table again. So you notice it's kind of long, like I said. We didn't include that on a slide. But it allows us to control what's happening on the base tables, rather than allowing people to make changes through the view. OK.

All right, managing triggers. A trigger can be enabled or disabled. If it's enabled, it's going to sit and monitor, and it's going to fire according to a triggering event. If it's disabled, the trigger doesn't run when there's a triggering event. So you do need special system privileges required to manage triggers.

And by the way, if you wanted to enable or disable your triggers, you can disable individual triggers or enable individual triggers. ALTER TRIGGER name of the trigger DISABLE or ENABLE. You can disable or enable all triggers for a table by doing an ALTER TABLE statement. You can recompile a trigger for a table. And you can also drop triggers, as well.

Now, let me backtrack a page because I did want to show you what permissions are required to manage triggers. In order to create triggers, you have to have the CREATE TRIGGER privilege. If you want to be able to alter or drop any trigger, then you need the appropriate privilege. If you want to be able to create a trigger on the database, you need ADMINISTER DATABASE TRIGGER privileges.

And of course, you need to have the EXECUTE privilege on the object if you don't own the object. If your trigger is going to refer to any objects that are not in your schema, somebody has to give you permissions on that object before you can create a trigger against their object.

You can also do these actions on disabling or enable triggers by using SQL Developer. Right-click the trigger. Rename it, Drop it, Enable it, Disable it. And you can look at your trigger information in USER_OBJECTS; in USER, ALL, or DBA_TRIGGERS-- that's going to display your trigger information; and also, if you want to see any syntax errors-- maybe somebody created a trigger or maybe you created a trigger and it compiled with compilation errors-- you can look at the USER_ERRORS dictionary view to see if you have any compilation errors.

OK. So here is the user_triggers. You notice that it has quite a few different columns in that dictionary view. And we've got TRIGGER_TYPE, TRIGGER_BODY. Let's go in and take a look at user_triggers here. select * from user_triggers. There you go. UPDATE_JOB_HISTORY.

SALTRIG-- that's the one I created, AFTER EACH ROW, tied to an INSERT OR UPDATE on ORA61 employees REFERENCING NEW AS NEW and OLD AS OLD. And there is the DESCRIPTION. after insert or update of salary on employees for each row, and then you'll notice that the TRIGGER_BODY contains the information about what's happening through the trigger.

Look at this one. This one here is actually calling a package. Let's take a look at that trigger. So this one is BEFORE INSERT OR UPDATE OR DELETE ON employees table, we're calling a subprogram. So that's something you can do. If your trigger logic is lengthy, put it in a procedure and call it from a trigger.

Now let's look at secure_dml-- that procedure. So this is the one that I had you guys disable earlier that checks whether or not you're trying to make changes during business hours. You have to do it during business hours, not at night and not on weekends. So this trigger calls this program, and here's the logic of that subprogram.

Testing triggers. Test each triggering and non-triggering data operation. Test each case of the WHEN clause. Make the trigger fire directly from a basic data operation, as well as indirectly from a procedure. Test the effect of the trigger on other triggers. Test the effect of other triggers on the trigger.

All right, quiz. A triggering event can be one or more of the following. An INSERT, UPDATE, or DELETE statement on a specific table, or a view, in some cases. A CREATE, ALTER, or DROP statement on any schema object. A database startup or instance shutdown. A specific error message or any error message. A user logon or logoff. All of the above-- it can be tied to any of these.

So you should have learned how to create database triggers that are invoked by DML, create statement triggers and row triggers, use database trigger-firing rules, enable, disable, and manage database triggers, develop a strategy for testing triggers, and remove database triggers.

So let's have you do practice 18, where you are going to create row triggers, create a statement trigger, and you're going to call procedures from a trigger. OK? So that will do it for my demonstrations for lesson 18.

## Practice 18-1: Creating Statement and Row Triggers - New - 17m

I will now demonstrate the practices for Lesson 18 on creating triggers. In this practice, you create statement and row triggers. You also create procedures that are invoked from within the triggers. Before starting the practice, you should execute the cleanup 18 dot SQL script.

So I am going to start with the solutions. And in this practice, as we mentioned before, you are going to create statement and row triggers. You also create procedures that are invoked from within the triggers.

Now, in step number one, we see that the rows in the jobs table store a minimum and maximum salary allowed for different job ID values. You are asked to write code to ensure that employee salaries fall in the range allowed for their job type. For insert and update operations, we're going to create a procedure called check salary as follows.

The procedure accepts two parameters, one for an employee's job ID, and the other for the salary. The procedure uses the job ID to determine the minimum and maximum salary for the specified job. If the salary parameter does not fall within the salary range of the job inclusive of the maximum and minimum values, then it should raise an application exception with the message, "invalid salary," whatever the value for the salary displayed. And then salaries for job-- we're also going to display the job ID-- must be between min and max. And we're going to replace those place holders with the actual salary, and job ID, and minimum and maximum values.

So they tell us to go ahead and open up solution 9 dot SQL from the PLPU solution directory and uncomment the code as described. So I will go ahead and do that. Let me go ahead and open up that particular one. So let's open solution 9 from the labs PLPU solution, and it's going to be the solution 9.

So we are going to run the Creator Replace Procedure, syntax starting on line 6 through line 19, and we'll run that in the My Connection connection. So let's take a look at that logic. Create the procedure called Check Salary.

We have a vmin salary variable and a vmax salary variable. We're selecting the minimum salary and the maximum salary into those variables for whatever the job ID is that we pass in. And then if the salary is not between the vmin sal and vmax sal, we're going to go ahead and raise an error.

Now, on the next page, we're asked to create a trigger called Check Salary Trig on the employee's table. That fires before an insert or update operation on each row. The trigger must call the check salary procedure to carry out the business logic. The trigger should pass the new job ID and salary to the procedure parameters.

So let's go ahead and do that in a new My Connection worksheet. And let's go ahead and show you the syntax for the trigger that you're going to create. Create or replace trigger. Give it a name.

Before insert or update of the javad comma salary on employees for each row, we're going to invoke the checks salary procedure. We're passing in the new job ID and the new salary. So I'll go ahead and compile that. And we've compiled the trigger with no errors.

Now, in the next page, we're asked to go ahead and test the check salary trigger using the following cases. Using your m package, add employee procedure, add an employee called Eleanor Bay to department 30, and then we're supposed to describe what happens and why. So let's go ahead and put that in a new worksheet window as well, trying to add Eleanor Bay to department 30, and you notice we get an error message.

And it says, invalid salary, $1,000. Salaries for the sales rep must be between $6,000 and $12,800. So it looks like our salary is not within a valid range.

Continuing on to the next page, we want to update the salary of employee 115 to $2,000 in a separate operation and change the employee job ID to HR rep. And let's report as to what happens. So I'll go ahead and run both of those statements.

Update employee, so salary equal to $2,000. Let's run that one. Notice that's an invalid salary. They have to be between $2,500 and $5,500. And then let's try to do this one.

And you notice that one also errors out. Invalid salary, $3,100-- salaries for a job HR rep must be between $4,000 and $9,000. So in the book, to describe what's happening, the first update, statement fails to set the salary to $2,000. The check salary trigger rule fails the update operation, because the new salary for employee 115 is less than the minimum allowed for the PU clerk job ID.

And then the second update fails to change employee's job, because the current employee's salary of $3,100 is less than the minimum for the new HR rep job ID. Now we're asked to update the salary of employee 115 to $2,800, and they ask us what happens in that case. So let's go ahead and do that. Whoops. In that case, it worked. The update operation is successful, because the new salary falls within the acceptable range for the current job ID.

Now in the next step, number three, we're going to update the check salary trig trigger to fire only when the job ID or salary values have actually changed. So let's go back and modify our trigger. And this time, we're going to be looking at the values that are coming in when the new job idea is not equal to the old job ID or if the new salary is not equal to the old salary.

Now we're asked to test the trigger by executing the m package, add employee procedure, with five different parameter values. We're going to be adding Eleanor Bay with a salary of $5,000 and a job ID of IT Prague. Now, it tells us that the PL/SQL procedure successfully completed.

Now, update employees with the IT Prague job by incrementing their salary by $2,000. And they ask us what happens. Let's go ahead and do that. Whoops, sorry about that. Let me put my PL/SQL delimiter there and run just my update statement.

And that tells us that we have an invalid salary of $11,000. Salaries for the job IT Prague must be between $4,000 and $10,000. Now we're asked to go ahead and update this salary to $9,000 for Eleanor Bay. Let's go ahead and do that. One row was updated.

And then next, we're asked to change the job of Eleanor Bay to ST man using another update statement with the subquery. And we're asked what's going to happen. So it looks like we error out. The maximum salary of the new job type is less than the employee's current salary. And therefore, the update operation fails.

Now, in step number four, we're asked to prevent employees from being deleted during business hours. We're going to write a statement trigger called delete m trig on the employee's table to prevent rows from being deleted during weekday business hours, which are from 9:00 AM to 6:00 PM. So let's go ahead and show you that logic.

So we're creating the trigger called delete m trig. Before delete on the employee's table, we're going to declare a variable called the day, another variable called the hour. And you notice that we're checking if the hour is between 9:00 and 6:00 and the day is not on Saturday or Sunday. Then we're going to raise an application error saying, employee records cannot be deleted during business hours.

So let's go ahead and compile this. And then let's test it. We are going to attempt to do a modification and when I tried to delete from a place where job ID equals sales rep and department ID is so.

Now, in my case, you notice that my row is deleted. Depending on the time of day where you're doing it, you would get an error instead. In fact, let me go in and change the logic just to show you the error message.

And let me change this to not between 9:00 and 6:00. And now, let's go ahead and try and delete. And you notice that now my trigger kicks in and says, hey, employee records cannot be deleted during the hours of 9:00 AM and 6:00 PM.

Now, let me recompile that trigger so that it behaves like it's expecting to behave. OK, my friends. So that is going to do it for the demonstrations for Lesson 18.
