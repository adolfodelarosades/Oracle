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
## 03 Practice 3-1: Declaring PL/SQL Variables - New - 12m
