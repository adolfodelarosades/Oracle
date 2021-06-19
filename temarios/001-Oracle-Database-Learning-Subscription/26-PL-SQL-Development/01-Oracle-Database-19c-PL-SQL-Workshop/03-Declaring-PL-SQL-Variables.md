# 3: Declaring PL/SQL Variables

* Declaring PL/SQL Variables - New - 26m
* The `%TYPE` Attribute - New - 24m
* Practice 3-1: Declaring PL/SQL Variables - New - 12m

## 01 Declaring PL/SQL Variables - New - 26m

OK, my friends, let's take a look at Lesson 3, Declaring PL/SQL Variables. There we are. Unit 1, Introducing PL/SQL. And then Lesson 3, Declaring PL/SQL Variables. OK, the objectives. After completing this lesson, you should be able to do the following. You should be able to recognize the valid and invalid identifiers. So an identifier is the name that we call an object. So if I create a table called employees, its identifier is employees. That's the name that we're calling it.

We're going to list the uses of variables. We're going to declare and initialize variables. We're going to list and describe various data types. We're going to identify the benefits of using the %TYPE attribute. And we're going to declare, and use, and print bind variables.

All right, variables. What are variables? Variables are labeled storage locations. They are used to store and process data in a PL/SQL block. They can hold different types of data. You should declare the variables before you use them in the PL/SQL block. Of course, you need to declare them before you use them in the PL/SQL block.

So here we have an example of the data that comes from a table, and some of that data, we want to store temporarily inside of a variable. So we have declared a variable called v_sal. And we have a SELECT statement that is selecting the salary into the v_sal variable. And then you notice, what we're going to do, we're going to update the employees table, and we're going to set the salary equal to the value stored in the variable plus $100. And that's going to be for the employee 100.

Well, if we look at employee 100, his salary is $24,000. So $24,000 is what's going to be stored in v_sal. So, then, it looks like we're going to give him $100 raise. These are monthly salaries, by the way. So it looks like he'll make 24,100 by the time we're finished with this statement. And there we are, 24,100.

So what are the naming rules? A variable name has to start with a letter. They can include letters and numbers as long as they start with a letter. They can also include special characters-- dollar sign, underscore, the pound sign, or the hashtag. They cannot be more than 30 characters in length, and they also cannot be reserved words. So, for instance, we have a data type called VARCHAR2. We would not create a table with the same name, because that's already been used as a data type.

So variables are declared, and we can optionally initialize those in the declaration section. Now, initializing, what that means is assigning a value to a variable. So we have to define the variable. We declare it in the declaration section, and then we can assign an initial value to it in the declaration section. We use and assign new values in the executable section.

Now, variables are passed as parameters to PL/SQL subprograms. We'll see that when we use the DBMS_OUTPUT.PUT_LINE, for instance. The PUT_LINE is actually a procedure. And, remember, a procedure is a subprogram. So we're passing a variable into a subprogram at that point when we use the DBMS_OUTPUT.PUT_LINE. So variables are also used to hold the output of a PL/SQL program.

So here we have some examples. We have the declaration section. We have the variable called v_hiredate. The data type is DATE. Now, we have not assigned a value there. So the value of v_hiredate would be NULL at that point. We have a variable called v_location, and that is a VARCHAR2 13. And you notice that we're initializing that with the string Atlanta. Now, because it is a character-based variable, we have to have single quotes around the initialization value, by the way.

We have a variable called v_deptno. Now, that is a NUMBER type. And so, notice, we don't have single quotes around the 10 there. Now, that one's a number with a precision of 2. And, by the way, we've assigned a constraint to that. We've said, hey, the v_deptno variable cannot be NULL. And so whenever you define a variable is NOT NULL, it has to be initialized with a value right then and there. So we have to initialize NOT NULL constraint variables.

And then notice that we have another variable called c_comm, and that one is a CONSTANT, and it's a NUMBER type. Now, what a constant is is it's a special type of a variable that, once you assign the value, you cannot change it. The value is constant. We also have to assign a constant when we define them. Just like the NOT NULL, we will get an error message if we don't initialize constants.

Now, the naming convention, we do have a recommended naming convention, and you'll see that in play here. Scalar variables, we recommend starting those with a v_ prefix. Constants, we recommend with a c_ prefix. So that's why the naming convention's a little bit different there.

Variables of different types. So, here, how do we declare and initialize PL/SQL variables? Here, we have the v_myName variable, VARCHAR2 data type, length of 20. DBMS_OUTPUT.PUT_LINE line My name is. Now, because we have not initialized the variable v_myName, it does not contain value. So this is only going to print out My name is with no value. And then notice we're initializing that to John. So the next time we use DBMS_OUTPUT.PUT_LINE, it's going to say My name is John.

Now, the second example, we're initializing the variable up front to the name John, and then we're changing that to Steven. And when we read PL/SQL, it executes top down, so it is going to assign John to the variable first but then we're going to change that to Steven. And so what's going to happen is, when we print that out, it's going to print out My name is Steven.

All right. We can also initialize variables through a SELECT statement. Now, here, they're showing you a syntax slide that shows you a summary, how we have a select list into one or more variables depending on how many columns we have selected in the select list from the table. And then we do a WHERE condition.

So we have different types of variables. We have scalar variables. Scalar variables, as I mentioned, are variables that only take a single value at a time of a single data type. We have reference variables. We have Large Object, or LOB variables. We have composite variables. We have non-PL/SQL variables called bind variables.

So here, again, some examples of declaring variables. A couple of things I want to point out. You notice that we're doing some addition on the v_orderdate variable. It's initialized to a DATE type. We're getting today's date and adding 7 days to it. So whatever next-- whatever the date is 7 days from now, that's going to be what the v_orderdate variable is going to be initialized to.

c_tax_rate, remember, that's a constant with the c_ prefix. It's the word CONSTANT that technically makes that a constant. And we have to initialize those again, as a reminder. Whoops. I hit my scroll wheel on my mouse. Sorry about that. So we have to initialize the c_tax_rate constant.

We have a v_valid variable. It's a BOOLEAN type. Booleans are either TRUE or FALSE-- TRUE, FALSE, or NULL. Now, this one, we've defined as a NOT NULL, so it has to be TRUE or FALSE. We're initializing that to TRUE. Now, this is not a string TRUE. This is the logical TRUE. So that's why the word TRUE does not have single quotes around it. It is the Boolean TRUE, logical TRUE.

Now, we have more than one way to initialize a variable. We can either use the assignment operator, which is the colon equal, or we can use the DEFAULT keyword. Either one is fine. I would say we probably use the colon equal, the assignment operator. We probably use that well more often than using the DEFAULT keyword. We usually use the DEFAULT keyword when we initialize parameters with the default, but you can use that with variables as well.

So they want us to use consistent naming conventions. That comes down to what I was talking about earlier. Usually we have a recommended naming convention, where scalar variables start with the v_. And then-- so if you're planning on using v_ for scalar variables, you should always use v_ for scalar variables just to be consistent.

You should also use meaningful names for the variables, meaningful identifiers for variables. If I want it to hold a salary, I should probably call it v_sal, not v_name name. Name it according to what's going to be held in it. Now, you won't want to name it exactly the same name as a column when you're planning on populating it with the column. That's going to cause confusion and, potentially, errors if you do that.

You do have to initialize variables that you designate as NOT NULL or CONSTANT. And then you should put one identifier per line for better readability and code maintenance. So, as I was saying, don't use the exact same name as a column as an identifier. That gets really confusing. Select employee_id into employee_id. This one would actually run, but it would be really confusing for people maintaining your code. I would probably name the variable v_employee_id rather than just employee_id. And then use the NOT NULL constraint when the variable has to have a value.

So this is our recommended naming convention, depending on the type of object that it happens to be. Variables, v_, constants c_, parameters, p_, bind variables, b_, cursors, records, types, exceptions, file handles, all of those. Now, a file handle, we're going to see an example of that coming up in a later chapter. But a file handle basically is a special type of a variable that allows you to store a composite piece of information.

So, for instance, what's the name of the directory we're working with, what is the name of the file we're working with. What are we doing to that file? Are we reading it? Are we writing to it? Are we appending to it? And so we'll see examples of what a file handle is. We'll actually see examples of everything listed on this page, by the way.

All right. If we are planning on holding string type data or character type data, we've got CHAR, NCHAR, VARCHAR, NVARCHAR, CLOB, NCLOB, as well as VARCHAR2. Sometimes they call it VARCHAR, by the way, because it's technically variable character, And CHAR is technically character. But CHAR sounds-- doesn't sound right, does it? And VARCHAR doesn't sound right.

So we've got the N character, or the NCHAR, as we're talking about there. Those are for multi-byte languages, where it takes more than one byte to store a value. And same with the NVARCHAR. But any of those types, including VARCHAR2, for your data types for strings.

Now, they're showing us different types of delimiters. We use the semicolon to terminate each one of those lines. We're using something called the alternative quote operator. That's the q single quote exclamation point. Now, that alternative quote operator, because we have a apostrophe on Father's day, the operator itself is q single quote delimiter. And it's pretty flexible on what you can use for the delimiter here. They're using an exclamation point as a delimiter. Down here on Mother's day, it's q single quote box bracket. They're using the box bracket as a delimiter.

So all kinds of different delimiters here, as you can see. But the semicolons are the ones you're going to want to be careful of. Those are the ones that terminate each one of those clauses. And strings have to be enclosed in single quotes. If we have apostrophes, you want to take care of that using the alternative quote operators. They're doing that with the v_event variable. And you notice that allows us to print out Father's day and Mother's day with the apostrophe.

Now, with your numeric values, we've got a number of different numeric data types for different purposes-- NUMBER, PLS_INTEGER, SIMPLE_INTEGER, BINARY_INTEGER, BINARY_FLOAT, BINARY_DOUBLE, and BOOLEAN. BOOLEAN is TRUE, FALSE, or NULL, as I was mentioning. Now, BOOLEAN, notice it is a non-numeric data type which can assume one of the three values TRUE, FALSE, or NULL.

But we also have the data types for date and time values-- DATE, TIMESTAMP WITH TIME ZONE, TIMESTAMP WITH LOCAL TIME ZONE, INTERVAL YEAR TO MONTH, INTERVAL DAY TO SECOND. So we have dates, timestamps, and interval types for date and time values.

And then Oracle can automatically do conversion between data types. That's what we call implicit data type conversion. Let me show an example of that. If I do a select 1 plus character 2, I have a numeric. This one is technically a string. Oracle is going to automatically convert that into a number so it can do the calculation. It's right justified in my column, so I know it's a numeric type. So that's an example of implicit conversion.

We typically like to be careful with implicit conversion. We would rather have you do explicit conversion using one of the conversion functions, like TO_CHAR, TO_DATE, TO_NUMBER, TO_TIMESTAMP. There are a number of reasons why we like you to use explicit conversions. One of those is it self-documents. You're basically-- in your code, you're telling it to convert it to a data type, so other people don't have to learn to interpret what's happening when they're maintaining your code.

It can also help with performance as well with explicit conversions. If you're doing implicit conversions, Oracle usually isn't able to use an index, if we normally would have used an index on that column that had to be implicitly converted. So, anyway, number of different reasons.

So, here, they're showing you the v_date_of_joining, which is a DATE data type. And they're passing in a character string showing 02-Feb-2000. Oracle's DATE data type, by default, is DD MON RR. And so Oracle is going to be able to interpret that as a DATE data type, even though technically it's a character string. And it's close enough to the DD MON RR format where it understands the 02 means DD, day of the month, and that Feb means MON, abbreviated month. And then RR, abbreviated year, 2000, it understands that. It looks like the YYYY format, which is going to be able to implicitly convert.

Now, the second example, February 02, 2000, you would actually get an error with that one, because Oracle wouldn't really understand what that string is meaning. It looks like a date to us, but to Oracle it's a character string that doesn't make sense. And so the explicit data type conversion, we're using the TO_DATE function to tell Oracle what those values in the string represent. February is represented by the month, 02 is the day of the month, 2000 is the YYYY, year of the-- well, the four-digit year representation. So I recommend using the explicit data type conversion.

Now, before we go into the %TYPE attribute and composite data types, I should go in and give you some demos on constants and NOT NULLS, and show you what happens if you do not initialize those up front. So if I have a v_name, which is a varchar2 25, varchar2 25, let's do that as a NOT NULL. When I run this, this will give me an error message-- a variable declared NOT NULL must have an initialization assignment.

So I'll go ahead and put Steven there. And let me erase my error message, and let's run it. You notice that's fine. Now let's do v_sal constant number. Let's not initialize that one either, show you what happens. Declaration of a constant V_SAL must contain an initialization assignment. So we have to initialize that as well.

Let me run it, now that I've initialized it. Looks fine. But constants don't let you reassign the value. v_sal colon equal 2600. Now watch what happens when I do this. Expression V_SAL cannot be used as an assignment target. Once I assign the value to the constant, I cannot change it. So any time you want to ensure that something always is that value, you can define that as a constant.

Now, I should go over the delimiters as well for your alternative quote operator. And I'll tell you what. Let me close that with a single quote. If I come in and concatenate together two columns with an is a literal string in the middle, you notice that works fine.

But if I had an apostrophe, that's going to error out. FROM keyword not found where expected. So it's because of this single quote right there. So I can use the alternative quote operator. I like to use box brackets, by the way. And if I put the box brackets there, the q single quote box bracket, terminated with the box bracket single quote, that becomes my alternative quote operator. And you notice how that allows me to have apostrophes

Now, what we were saying earlier is that you don't have to use the box brackets. You can use different delimiters. And you notice this one works just as well. So, anyway, that's the alternative quote operator, is what we call that. All right. Let me get rid of that. Let me clear that out. And let's go back to the book.

## 02 The `%TYPE` Attribute - New - 24m

All right, using the %TYPE attribute and the composite data types. So %TYPE is used to declare a variable according to a database column definition or another declared variable. It's prefix with the database table and column name and the name of the declared variable.

So they're going to show you that we have the v_emp_lname variable. It's defined as the type coming from the last name column in the employees table, so table name dot column name %TYPE. And like we were saying, you can define that either as the type of a column in a table or as the type of another declared variable. So here, we have a variable called v_ balance, which is the number 7,2. And then we have another one called v_min_balance, which is the variable v_balance%TYPE. So whatever data type the v_balance variable is that's the type of the v_min_balance. So technically, it's going to be number 7,2.

Now, why do we use this? Let me show you an example. So let me declare a variable. I'll tell you what, I've already done this one. So let's go back through the History. Let me just get the v_lname example that I had back here. So you remember this one, where we printed out the name King. Now King is only four characters in length. So what if I had set my variable to five characters in length? That would work great for this. I would still get King.

But what happens if I change this ID to somebody who has a longer last name? All of a sudden, I'm going to get an error message-- character string buffer too small. My variable is too small to hold the last name of my employee 101. Employee 101's last name is Kochhar. So it's definitely more than four characters.

So now, if we went in and looked at the table and looked at the current definition of the column in the table, we would see that it's probably about 20 bytes in length. And we could go ahead and set this to whatever that size is in the table. Let's go look that up. Let's look at the Employees table. Let's look at the columns. First name is set to 20 bites.

So what if I came in here and said this to 20? That might work for a while. But what if somebody goes back into the Employees table and changes the definition of the column to some other data type? Or maybe they change the size to an even larger size. Then we have the potential them PL/SQL code might end up stopping working in certain instances because the data types no longer match.

So what we can do is we can instead of hard coding that data type, we can put employees dot last name-- I guess the last name is 25, isn't it? Yeah, last name is 25. Sorry, the book was using first name. I was using last name. So 25 is the current size of my column. But at any rate, so we don't have to worry about it. We'll just use employees dot last name %TYPE. And you notice that this works great. I'm getting back Nina Kochhar's last name.

And it doesn't matter which employee I point it to. It's always going to run as long as this is a valid ID. So there you go, table name dot column name %TYPE. Or another variable vf name, which is of the v_lname %TYPE. We can do first name into v.

Since I have two columns here, two variables here, the first column is going into the first variable. Second column is going into a second variable. And let's go ahead and print out the first and the last name of my employee, Nancy Greenberg. There we go. Employee 101 should be Nina Kochhar. So you see how that works.

All right, so Boolean variables-- Boolean variables can hold a true or false or a null. We can use conditional expressions using logical operators AND and OR or the unary operator NOT to check the variable values. The variables always yield true, false, or null. We can use arithmetic, character, and data expressions to return a Boolean value.

We also have large object types. Large objects are meant to store a large amount of data. If it's character data, that's character large object, or CLOB. A binary large object, that's BLOB. That's something like a picture. If you want to store a picture in the database, you'd store that as a BLOB.

Binary file, now that's BFILE. BFILEs are stored in the operating system of the server, not in the database. And we point to that file in the operating system by using a BFILE. And we have to define the directory where that's stored. And then we use the combination of the directory and the file name in order to reference the BFILE.

National Language Character Large Object, that's your NCLOB. And LOB data types enable you to store blocks of unstructured data up to 4 gigabytes in size. And in some cases large object data types can be up to 128 terabytes, so really large types.

All right, now, we also have composite data types. We're not going to go into composite data types in this chapter. But besides storing a single name, we can store a whole row of data. A row of data is stored in something called a record. We can store a column of data in something called a collection. We will be going over both records and collections in a later chapter. So we just want you to be aware that besides doing scalar variables, we also have records and collections for storing rows of data and columns of data.

All right, bind variables-- so bind variables are created in the host environment. These are also called host variables. They are created with the keyword VARIABLE in PL/SQL. They are used in SQL statements and in PL/SQL blocks. They are accessed even after the PL/SQL block is executed. Referenced with the preceding colon, values can be output by using the PRINT command. Bind variables are required when using SQL Plus and SQL Developer.

So what are they talking about? Let me show you. Let me do a new worksheet here. Let's do a declare-- v_sal number begin. OK? Select salary into v_sal from employees where employee ID equal 100.

And let's go ahead and print that out. And we'll show you that this should return a value. You notice it returns 24,000.

Well, the limitations of your variables are that you cannot use those variables outside of the block. OK? So I cannot reference my variable v_sal in the select statement, because v_sal ceases to exist at this point. So if I try to run this, I'm going to get an error message. It's saying v_sal is an invalid identifier.

So what I could do, instead of creating this type of a variable, I could create a special type of a variable called a bind variable. And then I could use my bind variable right here-- select salary into b_sal. Now, b_sal, we can't print out like this. This would not allow us to print out the value of that.

So what I could do, however, I could put the print command here. And let's just run just this from lines 1 through 10. I won't run line 11 yet. And I just want to show you that the variable is holding at a value of 24,000 inside that bind variable.

And, by the way, whenever we're inside of a block like this, we have to prefix the bind variable with colons, OK? However, when we print it, we don't have to. We don't even need to put the name of the bind variable there with the print command, by the way. You notice how it still allows it to print. If I had more than one bind variable, print would print out both of them.

Let me do another variable. And, by the way, if you have more than one variable, they have to begin with the word variable. Each one has to begin with the word variable. And they have to be defined outside of PL/SQL.

So if you had another variable inside your declaration section, I could do this. I could select last name, salary, hire date into b_name, b_sal, v_hiredate. The one I could print out using dbms output put line is v_hiredate. And so you notice that the variable keywords are before the declare.

Make sure you always do that if you have a declaration section as well, because these are not PL/SQL variables. So we don't declare them here, because this section is for declaring PL/SQL variables. But these are called host. And if you think about SQL Developer as the host, we're defining them in SQL Developer. They're also called bind variables.

All right, so let's run these lines here. I'll show you what it looks like. So you notice B_SAL 24,000, B_NAME King. We also get back the hire date from the DBMS output put line. And then right down here, we've now held the value of the salary inside our bind variable. And you'll notice that we can then use that in another statement.

By the way, make sure that when you define them like this, make sure that you only execute with this button here. OK? If not, if you execute with this button up here, it's not going to recognize that you've already done the work and assigned the value. You're going to get this pop-up instead. And you'd have to reassign the value. And they wouldn't technically even get the value from the execution of the PL/SQL block. So just make sure you run it with the second button here.

And, by the way, these bind variables, once you define them, you no longer have to run them as long as you're in the same session. You notice this will run fine, even though I've commented out those bind variables. And those bind variable values are good for the rest of my session.

So that should hopefully help make all of that makes sense. You have to have a variable keyword. They're accessed even after the PL/SQL block is executed. We referenced them with the preceding colon. We can use the PRINT command to see what values are held in them.

So here's the book example. VARIABLE b_result NUMBER all on one line. I should show you that. If they're not all on one line, it's going to error out. Error report, unknown command. It doesn't know what I'm talking about. So now that that variable definition is all on one line and I run it, you notice it's fine, no error. So just be careful of that.

So SELECT SALARY times 12 plus NVL COMMISSION_PCT, 0 into b_result from employees WHERE employee ID equal 144 END. And then PRINT b_results. So that looks like 30,000. And then here, select this salary from 178 into b_emp_salary. And then we're going to use a SELECT statement to print out anybody else who makes $7,000. So it looks like we have three people that make $7,000 in the Employees table.

All right, you can also do a command call AUTOPRINT. If you set AUTOPRINT ON, you don't have to put the PRINT command. Also, by the way, they're showing you something called a substitution variable. Let me show you what that is.

Oh, let me show you on the last example, by the way. You saw me going in and manually changing this. So instead of manually changing 100, let me do a substitution variable. And those start with the single quote.

So watch what happens when I try to run this. It prompts me to enter in the value for this salary, actually employee ID. So enter the employee ID. I named it incorrectly. There we go. Enter the value for-- enter the emp ID. Let's do 105. OK?

So this is what verify means. It shows us what the old code looks like. It shows us our substitution variable. And then down here in the New section, it shows us what value we typed for this substitution. OK?

If you don't like seeing that feedback, you can always do the set verify off. And let me show you what that looks like. Let's do employee 110. No, let's do employee 99. We didn't find any data. And it also doesn't tell us what we typed in either. I have no idea what number I typed in unless I remembered what I typed in. Where I if I set verify on and did 99, it would tell me what I typed. It would say, hey, you typed in employee 99. So I personally like the verification, so that it shows me what value I typed in.

But, yeah, that's what substitution variables are all about. They prompt the user to enter a value. If this would have been a string-- so if I would have said enter the name, I would need to put single quotes around it, because this is a character-based column. And that way I could enter a character-based value for that. And there we go. There's 17,000. And you see that this makes sense now that you see what it looks like on the verification-- single quotes around the substitution variable. All right.

OK, so there we are, using AUTOPRINT with bind variables. Oh, I didn't show you AUTOPRINT. But set AUTOPRINT ON, it automatically show you the value. You don't have to use a PRINT.

That brings us to our quiz. The %TYPE attribute is used to declaring a variable according to a database column definition. That is true. Is used to declare a variable according to a collection of columns in a database table or view. That's false. %TYPE is only for a single column, not multiple columns. Is used to declare a variable according to the definition of another declared variable. That is true. Is prefixed with the database table and column names or the name of the declared variable. I'm going to say false on that, because they're pluralizing column names. OK? %TYPE is only used with one column name. So if they took that s off, that would be true.

But, yeah, we have another one called row type, which is used with multiple columns. We haven't told you about that one yet. But %TYPE is single columns. %ROWTYPE is multiple columns. So I would say B and C are the ones that are true.

All right, so that's going to do it for the lesson. We're going to have you guys go ahead and do Practice 3, where you're going to be determining valid identifiers, valid variable declarations, declaring variables in an anonymous block, using the %TYPE attribute to declare variables, declaring and printing a bind variable, and executing a PL/SQL block.

OK, my friends, so that's going to do it for Lesson 3.

## 03 Practice 3-1: Declaring PL/SQL Variables - New - 12m

I will now demonstrate practices for Lesson 3, Declaring PL/SQL Variables. Now, I am going to start with the solutions, as I was mentioning earlier, so that I can demonstrate on how to solve these practices. And so what we're going to do is we're going to focus on what are the valid and invalidate identifiers.

Now, if you remember from the lecture, the identifier names have to be 30 characters or less. They have to start with an alpha character. So they can't start with a number, for instance. And remember that they can't start with special characters. And we are also limited to special characters we can include. We can do dollar signs, pound signs, and underscores.

So if we used the word today as an identifier, you'll notice that that is valid. If we used last_name as an identifier, you know it is that is valid as well. Letter C on today's date with the apostrophe, that's invalid because the apostrophe character is not allowed. Letter D number of days in February this year, now that's also not going to work because that's too long. That's beyond our 30 characters that we allow.

Isleap$year, that is valid. The dollar sign is one of the special characters that we can include. As long as it doesn't start with the dollar sign, we can put the dollar sign in any place in there. Letter F is invalid because we're not allowed to start with one of the special characters, like dollar signs, pound signs, and underscores. Letter G is valid. Number along with the hashtag at the end is valid. And then number 1 to 7, they can be alphanumeric, so as long as it starts with an alpha character. So you notice that number 1 to 7 is also valid.

Now, in number 2, we're asked to identify valid and invalid variable declarations and initializations. Letter a, number of copies with the PLS integer type, that is valid. Letter b, printer name, that one is a constant. And the data type is var char 2 10, now that is invalid because any time we have a declaration of a constant, we have to initialize the variable. And since we're not initializing that variable in letter b, that is an invalid declaration.

Letter c, deliver to, that is a var char 2 length of 10. We're initializing that to this string of Johnson. But that is invalid because Johnson requires single quotes around it. Since we're initializing the variable with a piece of character data, we have to have the character data enclosed in single quotes.

The last one, by when, that is a date type. And that is initialized to current day plus 1. You'll notice that is valid. Now, it looks like we have our activity guide, actually I accidentally numbered that a instead of d. I think that should be a, b, c, d. So we'll need to correct that.

All right, step number 3, examine the following anonymous block and then select a statement from the following that is true. And I tell you what, let's go in and copy this. And, whoops, I got too much there. I'll copy what it can, and I'll hand type the end on there.

OK, so what's going to happen with this one is the block going to execute successfully and print Fernandez? Is the block going to produce an error because the f name variable is used without initializing it? Is the block going to execute successfully and print null Fernandez? Is the block going to produce an error because you can't use the default keyword to initialize a variable of type var char 2? Or is the block going to produce an error because the vf name variable is not declared?

Well, if we go ahead and run that, we notice that that will successfully execute. And it prints the word Fernandez. So we see the block will execute successfully and print Fernandez. And so that is the correct response for that.

OK, moving on to the next page, we want to modify an existing anonymous block and save it is a new script. We're going to open Lab 02 02 solution dot SQL script that we created in Practice 2. And in the PL/SQL block, we're going to declare a variable called v_today. And we're going to create another variable called v_tomorrow.

So let me go ahead and open up that saved file here. I saved mine in Home, Oracle, Labs, PLSF Labs. Go ahead and open that.

OK, so we're going to declare two variables, one called v_today. And that's going to be a date type. And we're going to initialize that to sysdate. And then the second variable is going to be called v_tomorrow, which is going to be v_today type.

All right, now in the executable section, we want to initialize v_tomorrow with an expression that calculates tomorrow's date, which means we want to add 1 to the value in v_today. And then we want to print the value of v_today and v_ tomorrow after printing hello, world. OK, so we're going to initialize v_tomorrow to v_today plus 1.

And then we want to print out-- I tell you what, I will just copy dbms output, just to make it easy to type that. We're going to have it two more times, as you see here. We want to print out what today's date is. And we want to print out what tomorrow is.

All right, so now, they want us to say that is Lab 03 04 solution. So let me go ahead and do a File, Save as. And we'll do Lab 03 04 solution.sql. We'll go ahead and save it. And then we're asked to go ahead and execute it.

And you see that we print out the words hello, world. For me, today is 23rd of June of '20. And tomorrow is the 24th of June of '20.

OK, next, we're asked to go ahead and edit this solution script. We're going to add code to create two bind variables named b_basic_percent and bpf_percent. Both bind variables are of the type number. So let me go ahead and do that-- variable b_basic_percent, if I could spell percent correctly. And it's a number type. And then variable bpf_percent. And that one is also a number type.

By the way, it doesn't matter if you're your data types are in uppercase. But I'm just capitalizing those. So it looks like a book.

And then Step 5b in the executable section, we want to assign the values of 45 and 12 to b_basic_percent and to bpf_percent. All right, so let's go ahead and do that. So I will do colon b_basic_percent initialized to 45 and bpf_percent initialize to 12. OK?

And next, we want to terminate the PL/SQL block with the slash. And then we want to use the print command. OK. And we'll go ahead and run that. And we see b_basic_percent 45, bpf_percent of 12. And you notice that that matches the screenshot.

Now, there is a note here. Notice, it says or print. So we don't have to use the print command with both of those bind variables. I could just come in here and say print. Let me clear the bottom and run it again. And you'll notice that it gives me the same output. So just an alternative way of printing out your bind variables.

All right, my friends, that is going to do it for the demonstrations for Practice 3.
