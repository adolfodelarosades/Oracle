# 6: Writing Control Structures

* Writing Control Structures - New - 28m
* Basic Loop: Example - New - 14m
* Practice 6-1: Writing Control Structures - New - 12m

## Writing Control Structures - New - 28m

OK, my friends. Let's take a look at chapter 6, Writing Control Structures. So we are here in unit 2, Programming with PL/SQL, lesson 6, Writing Control Structures.

After completing this lesson, you should be able to do the following-- identify the uses and types of control structures, construct an IF statement, use CASE statements and CASE expressions, construct and identify loop statements, and use guidelines when using conditional control structures.

OK, so this slide represents conditional statements, including IF-THEN-ELSE and IF-ELSE-IF-ELSE statements, and also a couple of different types of LOOP statements.

So IF statements. So the IF statement can have, optionally, some ELSE statements. Basically, what we're doing is, if this condition is true, then go ahead and do this type of an action. And then if we decide to include an ELSE statement, we will define what's going to happen in the event that that statement is not true.

Now, we can also expand that further. We can have multiple different conditions. If this condition is checked and is true, then go ahead and do this. However, if that condition is not true, then check the next statement. However, if that statement is not true, go ahead and check the next statement. And finally, if none of the above are true, we would default to the ELSE statement.

Now one thing I should mention, that if you have an IF, you have to have an END IF that's terminated with a semicolon as well.

OK, so let's take a look at an example. We're going to declare a variable called v_myage. You'll notice that that is a number initialized to the value of 10. And then in the executable section, we're checking to see if the value inside of v_myage is less than 11. If that is true, then we're going to print out the string 'I am a child'. And since 10 is less than 11, since that evaluates to true, then we would print out 'I am a child'.

Now, here we're initializing the variable to 31. And when we evaluate 31 as being less than 11, we notice that that is not true. And so we've actually added an ELSE clause to capture what happens when the value in v_myage is not less than 11. And so in this case, since 31 is not less than 11, we get the ELSE put-- the ELSE output rather of 'I am not a child'.

And then maybe we have several different conditions that we want to check. So you'll notice here we've got IF v_myage is less than 11, THEN 'I am a child'. ELSIF v_myage is less than 20, THEN 'I am young'. ELSIF v_myage is less than 30, THEN 'I am in my twenties'. And another one for IF v_myage is less than 40, THEN 'I am in my thirties'. And finally, if none of the above, then 'I am always young'.

So since this is 31, it falls under the ELSIF v_myage is less than 40. And so it's going to print out 'I am in my thirties'. Now notice the spelling of ELSIF. You notice it's E-L-S-I-F. There is no E in the middle. So I just want to point that out, just to make sure that you don't misspell that.

Now, what happens if we don't initialize a variable? So if we don't initialize a variable, it's automatically going to default to the ELSE clause. And so you notice here we get, I am not a child. So that's one of the reasons why we usually recommend that you always initialize a variable, so it doesn't default to a particular behavior. So always a good idea to initialize your variables.

All right. Let's take a look at CASE statements and CASE expressions. Now, with CASE expressions, you might recognize these if you are pretty good at writing the SQL language, because the CASE expression is an expression that can be used in SQL.

Now, I have two different variations of CASE expressions. We have CASE expressions, and we have searched CASE expressions. A regular CASE expression is when the selector falls immediately after the CASE keyword. A searched CASE expression is when we move that selector down into the individual WHEN clauses. And what that would allow us to do is to put multiple conditions that we wanted to check.

So let's go ahead and take a look at the book examples. Here, they have v_grade, which is initialized to a substitution variable. And you notice that we're expecting a character input on that, based on the single quotes around the substitution variable of 'grade'. And this is going to prompt us to enter a value. We're actually applying the UPPER function to that. So no matter how we type it, it's always going to be uppercase. And then v_appraisal is not initialized.

Now starting in the executable section, we're going to initialize that v_appraisal variable, depending on what we type in for the v_grade variable. And we're using a CASE expression to do that. So we're saying, CASE WHEN v_grade = 'A' THEN 'Excellent'. WHEN v_grade IN 'B' and 'C' THEN 'Good'. ELSE 'No such grade'. And then we have the END keyword there.

Now, this happens to be a searched CASE expression, because the selector, in this case, the variable v_grade, does not follow immediately after the CASE keyword. It falls into the individual WHEN clauses. So I think I'll give you guys a demo on this one, and so that it makes sense on what is the difference between a standard CASE or a searched CASE.

And I would do this just in a standard SELECT statement. Select last_name, job_id, and salary from employees. And let's imagine that I'm evaluating maybe giving people a raise. And so I'm going to use a CASE expression to kind of take a look at what these raises might look like.

And so what I might do is I might say, case job_id, when the 'AD PRES', or the president of the company, then salary times 2. When 'AD_VP', then salary times 1.5.

ELSE-- whoops, misspelled salary here. Now, when you have a CASE, you have to have an END. And let me format this, so it looks a little better for you. And let's take a look at what happens in this case. Let me tell you what. I'll run this as a statement so it's a little easier to read.

All right, so you notice in the condition, when the job ID is president, we're going to double the salary. When they're vice presidents, then we're going to do 1 and 1/2 times the salary. And everybody else is getting their salary cut in half.

So this is a standard CASE expression, because the selector in this case, the job_id column, follows immediately after the CASE keyword. Now, I can turn this into a searched CASE expression by moving that job_id column into the individual WHEN clauses. Now if I run this, you'll notice that it's exactly the same results. But what I can also do is I can add additional conditions.

And so now, before I run that, you'll notice I have two vice presidents, but only one of those is called Kochar. And so when I rerun this with that additional condition, one of the VPs gets a pay raise, the other one gets a pay cut. So that's what we can do with a searched CASE expression. All right?

OK, so let me go back to the book examples. And again, they're showing you the searched CASE expression. And then we have something called a CASE statement. Now, a CASE statement is a PL/SQL object. And we can recognize that this is a CASE statement, because it ends in the word END CASE instead of, on the previous page, ending in just END. So END CASE.

Now with a CASE expression, we evaluate the condition and return a result based upon the condition. With the CASE statement, however, we're going to evaluate the condition, and then based upon what happens with that expression, if it's true or not, we're going to go out and do some sort of an action based on that.

So as the book is saying here, hey, if 108 matches the value of v_manager_id, an action is performed instead of just returning a value. The action defined can modify the database also. And they're pointing out that it uses END CASE instead of END.

So I'm going to backtrack one page. You'll notice with the CASE expression, each of the individual WHEN clauses do not end in a semicolon. In a CASE statement, each of the individual WHEN clauses, because they do some sort of an action, they do need to end in a semicolon.

So what are we doing in this case? WHEN the v_manager_id variable is 108, THEN we're going to select the department_id and the department_name into the two different variables from departments for that manager. Then we're going to count how many employees exist in that department.

And then it looks like we're going to check another manager. WHEN v_manager_id is 200, then we'll do something similar most likely. Now notice that we've initialized it to 108. So in the book, when they executed this, you'll notice the output. It tells us, you are working in the finance department, and there are six employees in this department. OK?

Now, handling NULLs. So you do have to be careful when you're working with NULL values. You can avoid some common mistakes by keeping these rules in mind. Anytime you have a simple comparison involving NULLs, it's always going to yield NULL. If you apply the logical operator NOT to something that contains a NULL, it's still going to be a NULL. If the condition yields NULL in conditional control statements, its associated sequence of statements is not executed.

So we have these logic tables to help you in determining how Oracle is going to evaluate. We've got AND, OR, and NOT operators. So let's take a look at the NOT. NOT on TRUE is FALSE. NOT on FALSE is TRUE. NOT on NULL is still NULL. And that's because-- whoops, I accidentally clicked the page there. And that's because NULL values are indeterminate. And so if I say NOT against something that does not contain anything, it's still going to evaluate to a NULL.

Now, if we have the OR operator, only one of those sites has to evaluate to TRUE in order to return a TRUE. So TRUE OR TRUE is TRUE. FALSE OR TRUE is TRUE. NULL OR TRUE is TRUE.

Now, TRUE OR FALSE is TRUE, as we mentioned. TRUE OR NULL is TRUE. FALSE OR FALSE is FALSE. And look how FALSE OR NULL behaves. FALSE OR NULL evaluates to a NULL. And NULL OR NULL evaluates to a NULL. So we've got three occurrences of when we're going to get a NULL back with the OR operator-- FALSE OR NULL, NULL OR FALSE, and NULL OR NULL.

Now, with the AND operator, both sides have to evaluate to TRUE in order to be a TRUE. So TRUE AND TRUE are TRUE. And you'll notice that's the only time when it's TRUE. [CHUCKLES] FALSE AND TRUE is FALSE. FALSE AND FALSE is FALSE. NULL AND NULL is NULL. NULL AND TRUE is NULL. NULL AND FALSE, however, is FALSE. So keep those in mind.

We're going to ask you kind of a little quiz question here. What is the value of the flag variable using the AND operator, depending upon what the values of REORDER_FLAG and AVAILABLE_FLAG are? So TRUE AND TRUE, remember what that gives us. That gives us back a FALSE, because-- or I mean a TRUE rather. [CHUCKLES] TRUE AND TRUE is TRUE. It's the only time with the AND operator that we get a TRUE back.

TRUE AND FALSE is FALSE. NULL AND TRUE, OK, what do you think that is? NULL AND TRUE, remember that one? NULL AND TRUE is NULL. NULL AND FALSE is FALSE.

Let's go back and double-check our work. NULL AND TRUE? NULL AND TRUE is NULL. NULL AND FALSE is FALSE.

All right. Now we're going to look at three different types of LOOP statements. Now, I think I'm going to do some demonstrations up front, before I show you the book examples.

A loop is a PL/SQL component that allows us to repeat a statement or a sequence of statements multiple times. We have something called a basic loop, we have something called a FOR loop, and we have something called a WHILE loop. So I'm going to demonstrate each of these, and then we'll come back and take a look at the book examples.

OK. So let me do a DECLARE. And then we do a v_val number. Oops, got my Caps Lock on. And I'm going to initialize that to 0, OK? Couldn't decide whether I wanted to do 0 or 1. [CHUCKLES]

All right. So let's do a loop. A basic loop always executes at least once. Now when you do a LOOP, you always have to make sure that you have a valid exit condition. So and I like to always put an END LOOP there, because we need to also have an END LOOP to close out our LOOP. And I do that just so I don't forget, because sometimes when I'm thinking about my logic, I forget about my END LOOP. So that's just something that I decided to start doing, just to make sure that I didn't forget my END LOOP.

OK. So the first thing I'm going to do is I'm going to print out the value of v_val. OK? And then I'm going to go ahead and do a valid exit condition. Exit when v_val is greater than 10 is going to be my exit condition. And then I'm going to increment my v_val variable-- v_val initialize to v_val+1. OK?

So I've got my beginning of my loop. I've got my END LOOP. I've got my valid exit condition. Once v_val is greater than 10, then we're going to exit. And let's go ahead and run it. And you notice that it stopped.

Now in my case, I am printing out what the value of v_val is before I check my condition. So when it was 10, that's not greater than 10, so it continued. So you notice they added one more to it, so that would have been 11. And then we printed out 11, and here's where I checked it. Hey, is 11 greater than 10? Yes. And you notice that we stopped processing.

So you can play around with the order of these, OK, if you wanted to maybe cut this and put it after the valid exit condition. So you can kind of play around with the order of your exit condition. And you notice then it only prints up to 10. So just kind of work with it to get it to give you the behavior that you want.

So basic loops, these always execute at least once. So basic loop always executes at least once, OK? So simple. Really simple type of a loop.

Now the next type, I'm going to do a WHILE loop. And the difference in these-- a WHILE loop always checks before it enters a loop. And if it evaluates to a TRUE, then it's going to do the loop. If it evaluates to a FALSE, it's going to stop.

So I don't actually have an exit condition like this any longer. What I can do is I can say, WHILE v_val is less than 11 LOOP. And let's format this. There you go.

So while this is true, while we're less than 11, LOOP, we'll go ahead and print it out. We'll go ahead and increment it, just like I did with the basic loop. And then once v_val is no longer less than 11, then it's going to stop. So in this case, you notice that it stopped once v_val became 11. So these may not go into the loop. If this condition evaluates to a FALSE up front, it doesn't even have to do the loop.

All right. And then we have the third type of a loop called a FOR loop. A FOR loop executes a defined number of times. I don't need to increment this by the way, and I don't need my declaration, because what I'm going to do is I'm going to say, FOR i in 1..10 loop, and I'm going to print out the values of i.

Now, i is what we call an implied counter-- implied counter. That's why we start it with i, because it's implied. And we can refer to i between the LOOP and the END LOOP, but it is undefined outside of the loop.

And by the way, we're not allowed to increment i. I can't say, i initialize to i+1. It won't let you do that. And these are called bounds, B-O-N-- blah. Let me type it on the screen-- bounds. Lower bound on the left. Upper bound on the right.

So let's run it, so you can see what it looks like. There we are, 1 to 10. And, by the way, we have the ability to do a reverse, so for i IN reverse, 10 to 1. We still put the bounds-- lower bound to the left, upper bound to the right-- but you notice that it processes it in reverse order.

And just to show you that you can't redefine i, let me try and do it and show you the error message. Expression 'I' cannot be used as an assignment target, OK? So you can't do that. And also, you can't refer to i outside of the loop. So if I try to print i out here, I'm going to get another error-- Identifier 'I' must be declared. So i only exists here to here.

All right. So let's show you the book examples. And here we have an example. What we're doing is we're initializing the country_id variable to Canada, you know, CA for short. The v_loc_id we're not initializing. v_counter, it's initialized to 1. v_new_city is initialized to Montreal. And we're going to select the MAX(location_id) into the v_loc_id variable from locations where the country_id = v_countryid.

So I happen to know that the location ID currently, the maximum location ID for Canada, is 1900. So when we do our loop, we're going to insert some new rows. Insert into the locations table values v_loc_id plus v_counter. V_counter is 1 at this point. So this is going to be 1901, Montreal and Canada. We're going to increment the counter to 2. We're going to exit when the counter is greater than 3. 2 is not greater than 3, so we're going to loop again.

This time, we're going to put in the location ID of 1902. V_counter is going to be incremented to 3. 3 is not greater than 3, so we're going to loop again. And then this time we're going to put in location_id 1903.

So we're going to get three new locations inserted into our table-- 1901, 1902, and 1903. At that point, we're going to exit the loop, and we're going to print out how many rows are added. OK, at that point, v_counter is 4, so counter less-- you know, 4 minus 1 is 3, that's how many rows we added. Since we started with one, we have to offset by one to determine how many rows were added.

## Basic Loop: Example - New - 14m

OK, so that's a basic loop. The while loop, on the other hand, we're going to do exactly the same thing. But we're going to check the value of the counter before we go into the loop. We're going to end up getting the same three rows added-- 1901, 1902, and 1903. OK, While v counter less than or equal to 3 loop. OK.

So one is going to get inserted, 1901. We're going to increment it to 2-- check to see if 2 is less than or equal to 3. It is. So we iterate again, insert 1902. Increment v counter to v counter plus 1, which is 3. 3 is less than or equal to 3. That is true. So we're going to insert our third and final row.

And then we are going to do the for loop. I just want to point out here on the syntax slide, it does show you that we can do the reverse. There is a lower bound. There is an upper bound. By the way, if you wanted those bounds to be populated using variables, you can do that.

So you could say for i IN 1..VMAX LOOP COUNT-- something like that. And make sure that you initialize the variable that supplies the bound value. And then it would work. OK. So the counter, as I said, it's an implicit counter, OK. And so here we are. For i IN 1..3 LOOP. And this time, they're showing us the rows that are added-- 1901, 1902, and 1903.

You'll notice we're using i as a value. First time we iterate, 1901. Second time we iterate, 1902. Third and final time that we iterate, 1903 for our i values. So you can use the i values. You just cannot change those, right? And here's what I was talking about with the for loop. Reference the counter only within the loop. It is undefined outside the loop.

Do not reference the counter as the target of an assignment. And the loop bound should not be null. So that's what I was saying if you have a variable that you use instead of the lower or upper bound. Make sure that they are initialized. OK? So here is the suggested use of loops.

Use the basic loop when the statements inside the loop must execute at least once. Use the while loop if the condition must be evaluated at the start of each iteration. And use a for loop if the number of iterations is known. All right, now, you can also use labels with nested loops.

You can have loops inside of loops, OK. You can exit the outer loop with an EXIT statement that references a label. We're going to show you some examples here. This is not a complete example. But it's showing you that we're defining a label for the outer loop. We're defining a label for the inner loop. And you notice that we have EXIT conditions, OK.

Exit outer loop when this is true when the variable equals yes, OK. Exit when inner loop done equals yes. That's going to leave the inner loop only. OK. They left off the inner loop preference there. But that's what they're talking about there. This part here should be down here. And then we have something called a PL/SQL CONTINUE statement.

So what the PRC will CONTINUE statement allows you to do is, maybe you only want part of the loop to continue processing. OK. Or maybe we have a loop inside of a loop. And we want the inner loop to stop processing based upon some sort of a condition.

So I am going to go in and show you this, I think. So what I'm going to do-- I'm going to go ahead and open up some solutions so that I can show you what this looks like. All right-- not solution-- sorry-- good examples. And I just want to show you the examples here on those last two topics that we're talking about.

I'm going to modify these a little bit so that it's a little more clear. And by the way, if there's anything that you guys want to try, you should have access to the demonstrations that we give you in the book, OK, code examples. So feel free to go in and look at those different code examples.

All right. So this one only has one set of loops. It's going to loop 10 times, as you see here, from one to 10. We do have a continuous statement. Now, the CONTINUE statement-- I'm actually going to put some asterisks right here, because the CONTINUE statement is talking about what's happening above it, OK.

So once i is greater than 5, the lower part is going to stop executing. OK. So let me go ahead and run this. And we'll take a look at the output, OK. So top part of the loop, bottom part of the loop. Top part of the loop, bottom part of the loop. Top part of the loop, bottom part of loop. Top part of loop, bottom part. Top, bottom-- what is that? 1, 2, 3, 4, 5.

OK, so we're at 5 for i. The next time around will be 6. So 6 is going to be greater than 5. We're going to stop processing the out of loop total DBMS output, OK. So you notice how this part stops, which is defined right here. OK.

So the CONTINUE statement is basically saying, hey, once this condition is true, stop processing the bottom part of the loop. OK. Now, we have another example right here where we have a loop inside of a loop. So if we didn't have a continuous statement for every iteration of the outer loop, we would loop five times on the inner loop. OK.

But you notice we have a CONTINUE statement. I'm actually going to comment that out so you can see what it looks like without the CONTINUE. And, again, I'm going to put some asterisks there so it stands out a little better. OK.

So a loop inside of a loop. The outer loop loops five times. The inner loop loops five times for every loop at the outer. Outer loop, inner loop processes five times. So think about it like this. Why would we want to do a loop inside of a loop? Well, what if we're processing employees inside of a department? OK, department 10-- that would be my outer loop.

Then I would process all the employees in Department 10 in an inner loop. And then I would go to Department 20 in my outer loop. And then I would process everybody in my inner loop in Department 20. OK. So it's common to do loops inside of loops. And you can do loops inside of loops inside of loops. OK. So that's what it looks like without the CONTINUE statement.

Now, if I add in the CONTINUE statement, what's going to happen is the inner loop is going to stop processing based upon the condition. OK, and the condition is i plus j is greater than 5. I should point this out. The outer loop uses an i for a counter. The inner loop uses a j for the counter.

So when i plus j is greater than 5, OK, once we hit 5 out here, OK, 5 plus 1 is 6. So guess what. We're not going to process this one at all at that point. So let's show you what the output looks like. OK, so i. And then the inner loop processes 5 times.

But once we hit the fourth value for j-- OK, you notice how it starts processing. So we only get for loops. The next time, we only get three loops in the inner loop. The next time, we only get two loops in the inner loop. Next time, we only get one loop in the inner loop. OK.

So basically we're saying stop the inner loop when this condition is met and then go back out to the outer loop and continue the outer loop. So that's what the CONTINUE statement allows us to do. Now, we don't have you do that in labs. But I just wanted to make sure that you are able to see the flexibility of using the CONTINUE statement with loops.

OK, so I tell you what. Let's go back out to the book. So the CONTINUE statement definition is that it adds functionality to begin the next loop iteration, provides programmers with the ability to transfer control to the next iteration of a loop. It eases the programming process.

It may provide a small performance improvement over the previous programming workarounds in order to simulate the CONTINUE statement. And then there are two of the examples that I showed you. So there is the first one, which is a simple 10 loop. And then the second one that I showed you.

OK, that brings us to our quiz. There are three types of loops-- basic, for, and while. That is true. All right, so in this lesson, you should have learned to change the logical flow of statements by using the following control structures-- conditional statements using if statements, CASE expressions and CASE statements, the three types of loops-- basic, for, and while, the EXIT statement-- always have a valid EXIT condition to avoid an infinite loop-- and then the CONTINUE statement.

So we are going to have you guys do the practices for lesson six. You're going to perform conditional actions by using IF statements. And you're going to perform iterative steps by using loop structures. All righty, so that is going to do it for the demonstrations for chapter 6.

## Practice 6-1: Writing Control Structures - New - 12m

 
[ORACLE UNIVERSITY JINGLE]

I will now demonstrate practices for Lesson 6, Writing Control Structures. I am going to start out with these solutions. And we see that we are going to execute the command in the lab 0601.sql file in order to create the Messages table. We're going to write a PL/SQL block to insert numbers into the Messages table.

We're going to insert the numbers from 1 through 10. We're going to exclude 6 and 8. We're going to commit before the end of the block. So let's go ahead and run that lab that they're recommending there, lab 0601.sql so that we can have a table called Messages created. Let me go in and open that. So I'm going to go to labs-- home/oracle/labs/pls labs.

There we are lab 0601.sql. We'll go ahead and open that. And I'll go ahead and run this against the MyConnection. And we'll go ahead and run this as a script. And we now have a table called Messages. I am going to refresh my table list, so that we can see the Messages table there. And let's just expand that. We see that it's only got a single column called Results. All right.

Let me go ahead and close that file. And then in Step B, well, on Step A, we're going to insert the numbers 1 through 10, and then commit. So let's go ahead and do that using a new worksheet window. We're going to start with begin, and we're going to do a for loop. And then we're, again, going to do a conditional control statement. If i=6 or i=8, then, basically, we're not going to do anything, then null. OK.

Now, else, meaning if it's not 6 or 8, then we're going to insert into Messages into the column called Results, values of i. And then we'll have our end if, and then we'll have our end loop. And then we will have our commit. And then we will have our end.

Now let me go ahead and format that. There we go. And then I'll do my block terminator there at the end. And then we'll go ahead and execute a Select statement from the Messages table. All right. So let's go ahead and run that, first of all. OK. PL/SQL procedure successfully completed.

Now let's go ahead, and run the separate Select statement. And we see that we were able to insert from 1 to 10, skipping 6 and 8. And you'll notice that that actually matches the output in the book. OK. Continuing on to the next page, we're going to execute the lab 62.sql script. This script creates an emp table that is a replica of the Employees table. It alters the emp_tab a new column called Stars of VARCHAR2 data type, end size 50.

We're then going to create a PL/SQL block that inserts an asterisk in the Stars column for every $1,000 of the employee's salary. And then we're asked to go ahead and save your script as lab62_sol.sql. By the way, I'm going to go back one page just to see if they wanted us to save the previous one. No. Doesn't look like we have to save that one, so-- all right.

I will go ahead and open lab 62. that's going to create the table called EMP with the Stars column. And we'll go ahead and run this against MyConnection as a script. OK. Again, let's go ahead and refresh our table list over here. And we have our emp table. Let's just make sure that the Stars column is on the end. OK.

Let's go ahead and close the lab file. And let's open up a new worksheet. And then let's go ahead, and do our declaration section. We're going to declare a variable called the empno, and that's going to be the emp.employeeid%type-- type. And let's go ahead and initialize that to employee 176.

And then we're going to have another variable called v_asterisk. And that was going to be an emp.stars%type. And we're going to initialize that to null. And then we're going to have a variable called v_sal, which is going to be the emp.salary%type. And we're not going to-- we're not going to initialize that one either. OK.

In step letter B, we're asked to write logic to append an asterisk to this string for every $1,000 of the salary. For example, if the employee earns $8,000, the string of asterisks should contain eight asterisks. If the employer is 12,500, the string of asterisks should contain 13 asterisks. So looks like we're going to want to round up 12,500 to 13,000.

So let's go ahead with that executable section. Now just in case somebody does not have a salary, we're going to use the mvl function. And we're going to round the salary divided by 1,000, and if they don't make a salary, then we're going to do 0. OK. And we're going to do that into the v_sal variable from the emp table where the employee ID equal our variable. So we're only going to do this for employee 176.

And then we're going to go ahead and do a loop. For i in 1..v_sal loop v_asterisk is going to be initialized to the asterisk concatenated together with an asterisk. And then we'll end the loop. OK. So let's look at this logic. Let's imagine somebody makes $12,000. 12,000 divided by 1,000 would be 12. So we're going to get 12 into the v_sal variable.

And then we're going to loop 12 times in that case. And so, we're going to initialize v_asterisk, which initially is null to one asterisk. So on the first loop, we're going to get one asterisk. On the 12th loop, we're going to wind up with 12 asterisks. So I think that makes sense.

Next we'll go ahead and update that Stars column, update the emp table, set stars equal to be asterisk where the employee ID equals the employee number variable. So it's 176. Right. We'll commit that. We'll end. We'll do our PL/SQL block terminator. Let's format that to make it look pretty.

And then we will do a separate select statement. Select employee ID, salary, and stars-- whoops, not starts-- stars from the emp table where the employee ID equal 176. And I suppose we should probably make that formatted, as well. All right. They do ask us to save this as Lab 62 to sol.sql, so let's go ahead and do that. Save.

We'll do this under Labs. And I'm going to just click on that one, and change the title to Lab 6-- Lab 602_sol.sql. OK. So let's go ahead next, step letter E, we'll go ahead and execute and save this script as I just did. So let's go ahead and execute this part.

Looks like I have a misspelling there, line 19, let's go ahead and enable line number, so I can see where line 19 is. I'm going to right-click right here and toggle line numbers. Ah, there we are, right there. All right. Let me resave that. Let me read execute that. OK.

This time we were successful. And now let's go ahead and run the select statement separately. And there you go, employee ID 176, 8,600, looks like nine stars. Let's count those, 1, 2, 3, 4, 5, 6, 7, 8, 9. All right. So it looks like everything is working as we expected. This will conclude the demonstrations for Practice 6.
