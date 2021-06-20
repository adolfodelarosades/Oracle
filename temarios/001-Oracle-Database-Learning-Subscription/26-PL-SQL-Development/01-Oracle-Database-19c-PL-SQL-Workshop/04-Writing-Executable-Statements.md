# 4: Writing Executable Statements

* Writing Executable Statements - New - 27m
* Practice 4-1: Writing Executable Statements - New - 17m

## Writing Executable Statements - New - 27m

Let's take a look at chapter 4, writing executable statements. So we are here, lesson 4, writing executable statements.

And the objectives-- we are going to identify the lexical units in a PL/SQL block. We're going to use built-in SQL functions in PL/SQL. We're going to describe when implicit conversions take place and when explicit conversions have to be dealt with. Write nested blocks and qualify variables with labels. Write readable code with appropriate indentation. And then how to use sequences in PL/SQL expressions.

First up on the agenda, writing executable statements in a PL/SQL block. So we want to describe what lexical units are. So lexical units are the building blocks of any PL/SQL block. They are sequences of characters, including letters, numerals, tabs, spaces, returns, and symbols.

And they can be classified as identifiers, such as v_fname and c_percent. As delimiters, like the semicolon, the comma, the plus sign, the comma, the hyphen. Literals-- John, 428, or true. And comments-- either using the double hyphen for a single line comment, or the slash-asterisk-asterisk-slash to comment out multiple lines.

All right, literals-- so when we use literals, character end date literals have to be enclosed in single quote marks. Numbers can be simple values or scientific notation.

So here we have the variable name called v_name. You notice that's initialized to a literal character string. So we have single quotes around that.

And when we format code, the statements can span several lines. They're showing you how to format your code as I was showing you.

Right-click the worksheet, go down to where it says Format, or choose Control-F7 for the shortcut. And it's going to wrap an indenture code and automatically make your keywords uppercase. So it beautifies your code.

Now how do you comment code? As I mentioned, if you use two hyphens, that's going to comment out a single line of code. And we can actually use that methodology for documenting what's happening in the code.

And that's what they're showing us there. The following line displays the annual salary, DBMS_OUTPUT.PUT_LINE, v_annual_salary. Now because DBMS_OUTPUT.PUT_LINE, v_annual_salary is also a part of that line, that commented out line, it's not going to execute. If we would have wrapped DBMS_OUTPUT.PUT_LINE onto the next line, then that would have actually executed.

Now if you want to comment out multiple lines of code to prevent them from being executed, you can use the slash-asterisk and the asterisk-slash, as they're showing you there. So we recommend using comments in your code to describe what's happening in particularly complex pieces of code, or to put a message in there as to what's happening as far as the overall. Why did you create this script, for instance, might be a comment.

We can use predefined functions that are used in SQL and PL/SQL as well. However, we do have some that are not allowed. Decode is not generally allowed in PL/SQL. Group functions are not allowed in PL/SQL.

Now those are not allowed in the PL/SQL code. But if you have a SQL code embedded inside of your SQL syntax, group functions and decode can be used with SQL elements. They just can't be used with PL/SQL SQL elements. We can use single-row functions, built-in functions with strings, built-in functions with numbers, built-in functions with dates.

Let me show you what I mean about group functions not being available in PL/SQL. But they are available via SQL. Let me show you what I mean about that.

So if I have a variable like this, so here I have a PL/SQL variable, here I have a group function. It's not going to like that. So it says, line 2, column 20, encountered this symbol, comma, when expecting one of the following.

Let me do something else. Let's do max, something like that. And here's where they're telling us, hey, the function or pseudo-column max may be used inside a SQL statement only.

So you're not allowed to use group functions with your PL/SQL objects, however, I could do this. Select max salary into v_sal from employees. That would work.

And that's because I'm using the group function on my SQL code that's in my PL/SQL code. So hopefully that helps to make sense as to what we're talking about down here.

So they're showing you some examples of using the length function. Now, the length function, that's a single-row function. So you notice, we're able to use that with our variable.

v_desc_size is initialized to the length of the variable v_prod_description. v_prod_description has a really long string in that. And so it's going to go ahead and count how many characters are in that. And that's going to be the initialization for v_desc_size.

The second example, v_tenure is initialized to the months between the current date and the hire date. So that'll be fine. It'll tell us how many how many months an employee has worked. And that's going to be assigned to the v_tenure variable. So you can use SQL functions in PL/SQL, as long as they're not group functions and decode.

Now using sequences in PL/SQL blocks, here we have a new hire. We have a manager that says, hey, what should we have for her employee ID. Should I search the database to find the last employee ID? And how accurate would that be because I can't repeat the employee ID?

Well, we can actually use sequences in order to initialize variables. Sequences, if you don't already know, are database objects that can be used by multiple users to generate sequential numbers. Sequences can be created through the CREATE SEQUENCE statement.

So I'm going to show you how to create that. I've actually got a demo on that. Here I'm going to create the sequence called MY_SEQ. It's been created.

And then I'm going to initialize the variable by using the my sequence, the name of the sequence .NEXTVAL. And when I run this, you'll see that we're going to assign the value.

Well, I'll tell you what, let's see. Put my PL/SQL delimiter there. And I need to declare there. Looks like I did a typo there.

Declare the variable. And then there you go. So you notice how we got the value of the sequence here, which was 1 initially. And then we called .NEXTVAL. We got a 2.

If we run it again, we're going to get 3 and 4. If we run again, we're going to get 5 and 6. So you notice how the sequence just keeps advancing every time we call sequence named .NEXTVAL.

So that's what they're showing you in the book, how to create the sequence. We're starting with 1, incrementing by 1, no maximum value. We teach you all about sequences, by the way, in the Introduction to SQL class. Then we're using the sequence. We're initializing the sequence to the variable, then we're using the variable.

Writing nested blocks. We can write blocks inside of blocks. PL/SQL blocks can be nested. An executable section, which is the section between the begin and the end, that can contain nested blocks. An exception section can contain nested blocks as well.

So here we're showing you an example. We have an outer block in blue. We've got a nested block in red. Now as far as the visibility of variables, inner blocks or nested blocks are able to reference variables in the outer block. Outer blocks are not allowed to reference variables in the inner block.

So here, v_outer_variable is initialized to GLOBAL VARIABLE. v_inner_variable is initialized to INNER VARIABLE. You notice in the nested block we're able to reference both of those variables. It's going to print INNER VARIABLE and GLOBAL VARIABLE.

And then down here, the outer block has DBMS_OUTPUT.PUT_LINE as well. And you notice we're referencing v_outer_variable on that one.

Let me show you that. Let me just comment this one out for the moment so it won't run. And let's go ahead and run these lines. And you notice, we get INNER VARIABLE and GLOBAL VARIABLE.

Now if I tried to reference INNER VARIABLE here, that is going to error out because the outer block is not allowed to refer to variables on the inner block. So you notice how that doesn't have any visibility. It v_inner_variable must be declared. It can't see it.

However, it can reference the outer variable because we're already in the outer block. There you go. These are printed from the inner block. This one is printed from the outer block.

So let's show you another example. Here we have two variables that have the same name. We have v_date_of_birth in the outer block, we have v_date_of_birth in the inner block.

When we refer to the v_date_of_birth, it's going to look first in its own declaration section. So the date of birth for this one right here is going to be the 12th of December, 2002. And then the date of birth out here is going to reference this one, which is going to be 20th of April, 1972.

So let's show you that one. We're going to print out the father's name, and then the child's birthday. And then the child's name, and then the father's birthday.

Father's named Patrick. Date of birth, 12th of December. So it looks like the father was born December of '02. And then the child's name Mike, looks like that child was born in 1972.

So what we can do is we can add on these things that we call labels. This allows us to break scope because variables always look to their own block for the variable first. What we're doing when we refer to the date of birth here in the inner block, we're prefixing it with the label from the outer block. And that's going to allow us to print out the correct father's birthday. We're going to point to the outer date of birth rather than the inner date of birth.

And then the child's birthdate, let me show you where we had this before. We had this before the ends. There's no way to break scope and refer to an inner variable in the outer block. So we had to pull the child's birthdate into the nested block.

But let's show you that by using that label. We're forcing it to look at the outer variable, not the inner variable. And now we get father's named Patrick. Father's birthdate in '72. Child's name, Mike. Child's birthdate, 12th of December, '02.

That little label right there allows us to look at this one, not this one. Let's go back to the book. And I'll show you that.

Using a qualifier with nested blocks. There we are. We label the outer block. We use that label. Doesn't have to be outer, by the way. You can call the label whatever you want that makes sense, as long as you don't violate the naming rules. But there you go. Whatever you use here, you could use here, to have it point here rather than here.

So we're going to test you guys. So we want you to determine the variable scope. So let me show you a couple of examples. Now we have some questions in that book.

Now I can't get to the questions in the book. I can't get to the questions in the book right now because I'm in the PowerPoint. So let me go in and come up with some questions just to make sure this makes sense.

So at position 1, what is the value of the message going to be. So remember that if we don't prefix the variable, we're going to look at the most local variable that we have. So we're talking about this v_message. This v_message was initialized to CLERK not, concatenated with the previous v_message.

The previous v message was eligible for commission. So this should read CLERK not eligible for commission. Remember, it runs top down.

So initially it was this, which is here. And then we concatenated this onto this. So let's just see what we get. CLERK not eligible for commission. There we go.

Now let's take a look at v_comm. At position 1, what is the value of v_comm? At this position, what is the value of v_comm?

So let you take a look at it. And I'll tell you what I'm going to do. I'm going to copy this into another worksheet so you can see that. And I can scroll a little easier. Oops. Copy.

So at position 1, what is the value of v_comm? We have multiple v_comms. We have a v_comm up here. We have v_comm right here. We're inside of our nested block here.

So I think it should be this one, zero. Let's run it and see. Looks like it is zero. Now out here at position 2, what is the value of v_comm.

At position 2, we're pointing to this v_comm now. But notice what happens to that outer v_comm right here. We're multiplying it by v_sal times 0.3.

We have two different v_sals. We have a v_sal here, we have a v_sal here. Which one is it going to use? This one is going to use this one.

So outer v_comm is going to be initialized to inner v_sal times 0.3. So it'd be 50,000 times 0.3. So that's going to be 15,000. There you go.

Now what if I do this? What if in number 1 I come out and say outer.v_comm? What is that going to be? It's going to be the same thing. Outer.v_comm is initialized to v_sal times 0.3/ 15,000 here, 15,000 here. We're pointing to the same variable.

Now what about out here? What happens if I do v_message right here? Right here it was CLERK not eligible for commission.

We're changing it again right here. So it's going to be SALESMAN CLERK not eligible for commission. Because remember, this was already changed previously up here. It became CLERK not eligible for commission. And so you notice that we get SALESMAN CLERK not eligible for commission.

So these things execute top down. Once we change it, it remains that until it's changed again. Inner blocks can refer to outer blocks. Outer blocks cannot refer to inner blocks.

So for example, if I come in here and say, what is the value of v_total_comp, right here on line 19, v_total_comp is right here in the inner block, the nested block. We're not going to have visibility on line 19. So this is going to error out when I try to run it.

v_total_comp must be declared. If I can just highlight just that error message. v_total_comp must be declared. It has no visibility.

But v_total_comp right here. See what that value is. $50,000 looks like. That is v_sal plus v_comm. 50,000 plus 0 is still 50,000. So you'll have some exercises in the labs where you're going to be going in and running through some examples like that.

Using operators and developing readable code. We can use logical arithmetic concatenation. We can use parentheses to control the order of operations. We can use the exponential operator as well, the same as we can in SQL.

For instance, we can increment the counter for a loop. Loop count is initialized to loop count plus 1. We can set the value of a Boolean flag. good_sal is a Boolean type. So is the sal between 50,000 and 150,000? If so, then it's true. If not, then it's a false.

We can validate whether an employee number contains a value. Valid is initialized to empno is NOT NULL, rather.

So here are your guidelines. Make code maintenance easier by documenting the code with comments. Develop a case convention for the code. Develop naming conventions for your identifiers and for other objects. Enhance readability by indenting.

We're going to show you an example here of what your code should look like. For clarity, intent each level of code. And when something belongs to the line above it, it should also be indented.

Department ID, comma, location ID, you notice those both belong to the SELECT. The variable is indented as well. And if you right-click your code and use the Format option from the pop-up, it'll automatically make your code look like this.

Let's take a look at a quiz. You can use most single-row SQL functions, such as number, character, conversion, and date in PL/SQL expressions. And that's going to be true.

So we should have learned to identify the lexical units in a PL/SQL block. We should have learned to use built-in SQL functions in PL/SQL, how to write nested blocks to break logically-related functionalities, how to decide when to perform explicit conversions, qualify variables in nested blocks, and how to use sequences in PL/SQL expressions.

So we are going to have you guys do a practice-- practice 4 overview. You're going to review scoping and nesting rules. And you're going to write and test your PL/SQL blocks.

So let's go ahead and have you guys go ahead and do your practices. And that will conclude the demonstrations for practice 4.

## Practice 4-1: Writing Executable Statements - New - 17m

I will now demonstrate practices for lesson 4-- Writing Executable Statements. In this practice, you notice that they do have a note at the top. If you have executed the code examples for this lesson, make sure that you execute the following code before starting this practice-- drop sequence my_seq.

So what they're talking about is if I had gone in and opened up the PLSF directory and if I had ran the code examples for lesson 4. Let me just open that so you can see what that looks like. They're saying, if you had ran the code example 04, you would want to go in and issue this drop statement.

So let me show you how to run the drop statement. You're going to open up a new worksheet for MyConnection. And I'm going to drop sequence my_seq.

And I'll just run this with the second button. And you notice that, in my case, I get an error message, Sequence does not exist, because I haven't actually ran the code examples.

So now what we're going to do in this next section is we're going to have you look at the scope of variables in order to try and determine visibility of the variables, as well as what the values would be when we're initializing those.

So you'll notice that in step number 1, they're saying, evaluate the preceding PL/SQL block and determine the data type and value of each of the following variables according to the rules of scoping.

So letter A, what is the value of v_weight at position 1? Here is position 1 right here. So what is the value of v_weight?

So if you go in and look at your code, v_weight is initialized to v_weight plus 1. We have a local definition of v_weight right here. So we would have 1 plus 1, which should be 2.

And then what is the value of v_new_location at position 1? v_new_location is a nationalized to Europe. v_new_location is initialized to Western concatenated onto v_new_location. So that should be Western Europe at position 1.

Then they're asking us the value of v_weight at position 2. v_weight-- now you notice that this is after the end. So this v_weight is talking about v_weight. So that should be 600 plus 1, so 601.

And what is the value of v_message at position 2? v_message is initialized to v_message concatenated to is in stock. Should be a product. 10,012 is in stock is what that should be.

And then what is the value of v_new_location at position 2? Western. Now, v_new_location, we don't have an outer v_new_location.

We have one that's in the inner block, which, remember, we won't have visibility on that. We won't have the ability to look inward. So this is can actually error out if we try to take a look at v_new_location at position 2.

So we can double check our answers. Let's go down to the solutions. 2 was what we had for the weight. Western Europe was what we had. That is right. 601, that's what we came up with. Product, 10,012 is in stock. And then this last one would error out because v_new_location location is not visible outside the block.

Let's go on to the next question. They want us to take a look at this. And they want to know the value of v_customer in the nested block. So we're going to have to go in, and so here's our nested block right here.

By the way, we left out some code. So I better go back to the previous screenshot. And let's take a look at the values.

The value of v_customer in the nested block is 201. The value of v_name in the nested block is Unisport. The value of v_credit_rating in the nested block is good. There it is right there. The value of v_customer in the main block is Womansport. The value of v_name in the main block is-- it won't run, that's illegal. And the value of the v_credit_rating in the main block is excellent.

So let's double check those. So 201, we got that for v_customer. Unisport for v_name in the nested block, and as well as the data types, by the way-- NUMBER and VARCHAR2.

The value of v_credit_rating in the nested block, that was good. Data type of VARCHAR2.

The value of v_customer in the main block was Womansport. The data type is VARCHAR-- well, VARCHAR2 technically.

The value of v_name in the main block. And again, that one's going to not be visible. And you would see an error.

And then the value of v_credit_rating in the main block is excellent. And the data type is VARCHAR2.

Number 3, use the same session that you use to execute the practices in the lesson titled, Declaring PL/SQL Variables. If you have opened a new session, execute lab 03_05_solution.sql.

So I'm in a new session. So let me go ahead and open lab 03_05 solution. And that was labs. And lab 03_05 solution, oh, I see that they want you to do.

So go in two labs PLSF solutions, open that. They want you to go and do solution 3, basically what we had finished up with in lesson 3. I'm just going to open it from my labs 03_04_solution.sql.

Now what we want you to do is to use single line comments and text to comment the lines that create the bind variables. We do need to run it at least once so it's bound in our session. So I'm going to go to MyConnection and I'm going to run it. Make sure it runs successfully.

Next, they want you to comment out the variable definitions. Because I've already executed it in this session, I don't have to redefine them.

And then in the next step we're asked to use multi-line comments to comment the lines that associate the values to the bind variables. So right here, slash-asterisk followed by asterisk-slash.

And then in the Declaration section, declare and initialize two temporary variables to replace the commented out bind variables, and then declare two additional variables, v_fname of type VARCHAR2 and size 15, and v_emp_sal of type NUMBER and size 10.

So let me go ahead and do that as well-- v_basic_percent number initialize to 45, v_pf_percent number initialize to 12. And then v_fname, and then v_emp_sal.

And by the way, you can comment out the other lines if you don't want to see those as well. If you don't want to see v_today, you can comment that out. You can comment out v_tomorrow. And we can also do multi-line comments on the block that prints those values.

Next, what we're going to do is we're going to include that SELECT statement. And we're going to come in and say, oh by the way, I'm going to have to get rid of that one as well.

SELECT first_name, comma, salary, INTO v_fname, v_emp_sal, from employees WHERE employee_ID equal 110. By the way, I'm going to comment out my print command as well.

Next, what we want to do is step letter F. We want to calculate the contribution of an employee towards the provident fund. The provident fund is 12% of the basic salary. And the basic salary is 45% of the salary.

We want you to use local variables for the calculation. And try to use only one expression to calculate the provident fund and print the employee salary and his or her contribution towards provident fund.

So let's do that. We're going to print out hello, concatenated to v_fname. And then we'll do DBMS_OUTPUT.PUT_LINE-- your salary is v_emp_sal.

And then DBMS_OUTPUT.PUT_LINE-- your contribution towards PF-- and then drop to the new line so you can see the v_emp_sal calculation. Divided by 100, multiplied by v_pf_percent, divided by 100.

I'm going to make sure that math works right. Your contribution towards PF concatenated to v_emp_sal multiplied by v_basic_percent divided by 100 times v_pf_percent divided by 100. So that looks right.

We are asked to go ahead and run it. I'll tell you what, let me erase this and then run it. And there we go.

Hello John, your salary is 8,200. Your contribution towards PF is $442.80. Just double check that against what the book says we should get. And it looks like we got back the correct results.

So they ask us to go ahead and save that as lab 04_03_solution.sql. So let me come up here and go File, Save As lab 04_03_solution.sql. And there we go.

So that will complete the demonstrations for practice 4.

