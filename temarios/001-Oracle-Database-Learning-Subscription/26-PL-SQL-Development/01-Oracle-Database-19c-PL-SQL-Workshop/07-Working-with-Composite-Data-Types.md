# 7: Working with Composite Data Types

* Working with Composite Data Types - New - 37m
* Associative Arrays (INDEX BY Tables) - New - 14m
* Practice 7-1: Working with Composite Data Types - New - 23m

## Working with Composite Data Types - New - 37m

OK, my friends. We will now take a look at Chapter 7, "Working with Composite Data Types." We are here in Unit 2, "Programming with PL/SQL," Lesson 7, "Working with Composite Data Types." OK, after completing this lesson, you should be able to do the following, describe PL/SQL collections and records, create user-defined PL/SQL records, create a PL/SQL record with the %ROWTYPE attribute, create associative arrays including the INDEX BY table and the INDEX BY table of records.

So what are composite data types? Well, composite data types are data types that we define or that we use in order to store more than one value. So if we wanted to be able to store a whole row of data in memory, we might use a composite data type. Or maybe we want to store a column of data, then we might use a composite data type as well.

So in this slide here, Alice is the database designer of the HR schema. And Alice is wondering, hey, is there a way to add more than one contact number in the same table? Or is there a way to group an employee's address as a single column instead of having to have separate columns for number, street, state, state, postal code or zip? And so that kind of leads us into the discussion of composite data types.

Now, we have composite data types that include PL/SQL records. Records hold rows of data. And then we have collections. A collection allows us to store columns' worth of data or columns of rows of data. Now, they're showing us three different types.

We have associative arrays. We've got nested tables. And we've got VARRAYs. In this class, we're going to have you only work with the associative arrays. Associative arrays are only PL/SQL structures. Nested tables and VARRAYs, on the other hand, can be PL/SQL structures or they can persist in the database as column types in a table.

So in the event that you wanted to store multiple phone numbers for each employee along with a label that describes what sort of phone number it happens to be, I might use a nested table or a VARRAY as the definition of a column in my table. And if you can think about a nested table or a VARRAY of being a little teeny table that's inside of the field of a column for a row-- and so, you know, those are more advanced structures. So we don't really cover the nested tables and VARRAYs in this class.

So this screen here kind of describes the differences between PL/SQL records versus collections. PL/SQL records, they're used to store related but dissimilar data as a logical unit. So think about that as a row of data in a table, typically contains related data.

I've got an employee name. I've got an employee salary. I've got an employee job ID. Those are related to each other, because they pertain to an employee.

Collections, on the other hand, they're used to store data as a single unit, data that is not necessarily related, but maybe has the same type. Like, maybe I want to store a column of last names as a single unit. Records are used when you want to store values of different data types that are logically related, collections, used when you want to store values of the same data type.

With records, each record, or each element, rather, can be accessed as a record_name.field_name. With collections, we need to access each element by referring to its unique subscript. And I'll show you what that means here in a little bit.

So an example of a record, we're using a record to hold employee details that are related because they provide information about a particular employee. Or with collections, we want to use a collection to hold the emails of all employees. It may store any number of email IDs. However, email one is not related to email two, and so on and so forth.

All right, so I'm going to give you a demonstration on records, first of all. And then we'll come back and take a look at the book. And I've still got some examples here from the last chapter, so let me get rid of those, start fresh with a new worksheet.

OK, so I'm going to show you what we might have done previously. And then I'll show you how we can use the record to store the same information instead. So let's say that I have v_fname. And let's say I have v_lname.

OK, and then I have my executable section. And then I'm going to select my first_name and my last_name into these two variables. I'll keep it simple. I'll just do the select at the moment.

All right, so I have a column that's going into this variable. I have a column that's going into this variable. And when I run it, you can see that this worked successfully.

I guess I should probably do a put_line so that we can see what the values are here. And let me go ahead and run it. And we see that that is Steven King.

Now, an Oracle table can have up to 1,000 columns in it. So with this mechanism, I would have to define 1,000 different variables in order to store 1,000 different elements for a single row in a table that had 1,000 columns. So what I could do instead is I could actually create a custom type.

And in order to create a custom type, I'm going to define it as a type. And I'm going to give it a name. My type is called emptype.

And I'm going to say it's a record. And then I have to define my, what we call our fields or our components. And they're going to be comma-separated components.

So I basically defined a composite type that has two elements in it. One, it looks like, is going to store a first name. The second one is going to store a last name. And then I'm going to define my record of the type that I just created. So my record is of this type which has this structure. So now what I can do is, instead of popping this into two different scalar variables, I'm going to select those two values into the record.

Now, you have to be careful, because you still have to select the columns in the same order that they are defined in your type. So this one is going to go into the first component. The last name is going to go into this component because they're positionally matched.

And by the way, because these components are inside of a record, I have to prefix those with the record name. So it becomes record_name.field_name. And when I run it, you'll notice that I get back exactly the same results. But the point is that it's now into a single structure rather than into multiple structures.

Now, what if I wanted to do this instead? What if I wanted to select the whole row into a record? Well, I've got a choice at that point. I could either define all of my fields in the correct order. And I happen to have 11 columns in the employees table. So I would have to define all 11 fields or all 11 components in my type before I could use it.

So I could do that. Or we have a shortcut. If I want to do the shortcut, what I can do is I can get rid of my type. And if I know that this data comes from a table, I can put the name of the table along with the %ROWTYPE attribute. Now, when we do that, we don't have to define the type. The record takes its structure from the structure of the table that we use with the %ROWTYPE.

And the field names get their names from the columns in the table. I know that in the employees table I've got a first_name column. And in the employees table, I know that I have a last_name column.

And if I wanted to look at the salary, emprecord.salary-- and when I run it, you notice that I can refer to anything in the entire row that's stored in the record just by referring to the correct field name, hire_date, for instance, so 17th of June of '03. So that's a nice little shortcut, having that ability to define a record based upon the structure of a table.

All right, let me go back to the book. And we're going to show you the book examples. So here we have somebody thinking about employee promotions.

And what we want to have happen is, we want to update the job ID of each employee. We want to add data to the job history table to reflect a promotion. And we want to modify the salary of the employee.

So this is where we're showing you how to create your type, where we're defining the type name. And we're defining the field declarations. Now, the field declarations can be regular data types. Or they can be %types or %rowtypes. You notice all the flexibility in the field declarations that they're pointing out down here, field_type, variable%type, table.column%type, table%rowtype, standard data type like varchar2 or number.

OK, so this is the book example. We're defining our own type called t_rec. We're storing the first name, the salary, and the hire date. You notice the v_sal field is the number type. The first name is employees.first_name%type. The hire date is employees.hire_date%type. And then our record is called v_myrec. And it's initialized to the type of t_rec.

Now we're selecting the first name, salary, and hire date in the correct order that the filter defined in the type into the record for employee 100. And you notice that we're printing out the first name, the salary, and the hire date, getting back exactly the same information that you saw me retrieve. I think my hire date is different. But you know, we're going to make the hire date.

OK, so the record structure, we've got the field declarations. The example, field one is employee_id number six. Field two is last_name varchar2 25. Field three is job_id varchar2 10. And so you see that it's a composite type, because we're storing three pieces of information with potentially different data types.

Now we have the shortcut that I was talking about. We have the %rowtype attribute. We declare a variable according to a collection of columns in a database table or view. Fields in the record take their names and data types from the columns at the table or view. Now, I mentioned table, but I do want to point out that %rowtype can also be against a view, as we're saying here.

So prefix the %rowtype with either the database table name or the view name. In the example, we're defining a record called employees which is based on the employees %rowtype. OK, now this one's a little bit more advanced. Here we're defining our own type that includes a v_sal field, a v_minsal field that has a default setup for it, a hire_date-- oops. I don't know what happened. I think my finger hit my scroll on my mouse.

So we have a v_sal, a v_minsal, which I said we defaulted to the value of 1,000. We have the v_hire_date, which is the employees.hire_date%type. And then we define a field called v_rec1 which is of the employees%rowtype.

So we are defining a type that can hold 14 pieces of information all in one. So v_sal would be one value. v_minsal would be a second value. v_hire_date would be a third value.

And then v_rec1 can hold 11 pieces of information, because it's based on the structure of the employees table. And we have 11 columns in that table. So 11, 12, 13, 14 pieces of data can be stored in that one record.

And then we have the record called v_myrec, which is of the t_rec type. Now, what we're doing is we're showing you how to initialize those directly. So v_minsal, notice-- or remember, I should say, we defaulted to 1,000. So what we're going to do is we're going to initialize v_myrec.v_sal to v_myrec.v_minsal plus 500. So we'd be 1,500.

v_myrec.v_hire_date is going to be initialized to sysdate. And then we're going to select the whole row from the employees table into v_myrec.v_rec1, which is this one right here that holds 11 pieces of data. So we're storing the whole row of information for Steven King inside that v_myrec record inside of the field called v_rec1, which has 11 fields of its own.

And now notice how we have to refer to the values inside of the record, name of the record, name of that field, name of the field. record_name.field_name.field_name. You might say record_name.record_name.field_name, because this is technically a record right here. So that one's a little more advanced, a record inside of a record.

All right, the advantages of using the %ROWTYPE attribute, the number and data types of the underlying database columns don't need to be known. And in fact, those might change over time. The %ROWTYPE attribute is useful when you want to retrieve a row using select star or when you want to do row level inserts and updates. Let me show you what I mean and that.

So here I'm selecting the whole row of information for Steven King. Let's look at his salary again here. You can erase all this. OK, what if I decide I want to change his salary? I'll change that to $1. Let's go ahead and print out what that looks like.

And what if I had multiple changes? What if I not only wanted to change his salary, but what if I also wanted to change his commission percent? Let's change his last name just to keep it simple.

OK, let's run it, show you what that looks like. Steven KING in upper case, $1-- I'm going to roll that back by the way, because I don't really want to change that. But actually, we didn't even change anything in the database. But that's what I'm going to do next, because I'm sure know how to do a row level update.

Update employees set row equal to emprecord where employee_id equal emprecord.employee_id. And let's run it again. So here I am updating the employees table. I'm setting the row equal to the record. So that's a row level update.

OK, now I could go out to the employees table. And we could take a look at what his data looked like. Upper case and $1, so you notice how we overwrote the whole row.

Now I'm going to roll it back, because I don't really want to make that change, as I was saying. But just for the purpose of example, showing you how that might work-- I'm to go back to my employees table and just refresh it. And I got my $24,000 back.

Or maybe what I might want to do is, what if I have a copy on a table? Create table-- I'll create an empty table here. And then what I will do is refresh my tables. There is my copyemp. And then down here, what I'll do is I will insert into copyemp values emprecord. And that's going to be a row level insert.

OK, now when I go to my copyemp table, you notice that I inserted the row into that. So you know, row level inserts, row level updates-- so let's go back to the book. And that's what they're talking about down here.

Now, we're going to show you some examples in the book. But I wanted to show you that simply first before we show you the book examples. So here we're selecting the whole row into the record. The record's based on the structure of the employees table.

And what we're doing is we are selecting a row from one table so that we can insert into another table called retired_emps all of these individual pieces of data coming from the record, record_name.employee_id record_name.last_name, record_name.job_id. Now, the retired_emps table has two fields in it that hold dates. It's got a HIREDATE column. And it's got a LEAVEDATE column.

So for the hire date, we're using the value from the record. For the leave date, we're using the sysdate function to populate that one. OK, so pretty easy, you know, record_name.field_name to populate another table.

Now in this one, we are creating a record. And what we're going to do is we're going to do an update. So we're going to create the record. This time, the record is not based on the employees table. It's based on the retired_emps table.

And now we're going to select the row of information from the retired_emps table into the record. Now we're going to change one of the fields in the record to the current date. And then we're going to update the retired_emps and set the roe equal to the record where the employee number equal the employee number, so showing you how to use a row level update.

Let me just see if there is another one I wanted to show you. No, I think that'll do it. So they're showing your row level insert, showing you row-level update. All right, now let's take a look at the PL/SQL collections.

PL/SQL collections, we're going to show you how to use index by tables, also known as associative arrays. Think about an associative array as a collection with two columns. We have a primary key that can be either an integer or a string data type. And then we have a column that can either hold scalar values or record values.

Now, the key, that's used as an index so that I can interact with the values that are stored. So if I needed to interact with Kramer, I would point to key number four. So I'm going to show you how to build these. And then we'll come back and take a look at the book again here.

And I might as well do this in a new worksheet here. OK, so I'm going to declare a type, just like I did with records. Instead of saying type emptype is record, this time I'm saying table emptype is table of employees.last_name%type. So it looks like I want to store last names of my employees in there.

And then we have to tell it what type of an index it's going to have. Remember, this can be a integer-based index or a character-based index. So I can use PLS integer. I can use binary integer. I could say index by varchar2 if I wanted to. So we're just defining what our index is, and then emptable of emptype.

Next what I'll do is to do a for loop. OK, and I'm going to go ahead and select the last name of my employee into my emptable. And I'm going to use my implied counter value to assign the index for the value stored in the collection. So employee 100 will be stored in an index by table at index 100.

So let me just print out, since I know Steven King is somebody stored at index 100, I'm going to say, emptable. And I need to refer to the index. What is stored at emptable 100?

Well, that's going to be King, right? And so that's the value that I should get back when I run this. You see King? King is stored at index 100.

Kochhar should be stored at index 101 since the index is going to match that person's employee ID. De Haan should be stored at index 102. There you go. So I've loaded up my index by table. And now I can refer to the values by pointing to the index.

Now what it could do, I could do a second loop here for j in. And what I could do in this case, I can use something called index by table methods so that I can be able to iterate through the index by table values. So these are my table methods, first and last. So I'm saying, hey, iterating from the first record to the last record loop, really the first index to the last index. And then what I'm going to do is again refer to j.

Now, index by tables don't have to be stored in order. So I might have index 100, then index 103, then index 101, then index 110, then index 109. And that's why these table methods are important, because I'm just going from that first record to the last record. And what that's going to allow us to do is to print out all of the last names of everybody that is stored in my index by table or my associative array.

Now, we also have other methods. I can actually delete some records if I wanted to. I can also print out what the values are of my indexes. Let me do this.

I just want a delimiter there. I'm going to do emptable.prior j. And I'm going to do emptable.next j. OK, so these are methods as well. It allows us to see what our index values are. And what I'll do is I'll concatenate this to prior index.

And let's use next so that I can see what my-- OK, so Steven King is held at the first index value. So we don't have a prior index. The next index, though, is going to be 101.

So index 101 points to Kochhar. And in that case, the prior index is 100, which was pointing to King. And then the next index is 102 that points to De Haan. So this allows us to see what our index values are.

Now, we can also delete elements. So I can come in. And I can say emptable.delete 105. Now, that's going to cause a problem, because it's going to cause a hole right in the middle of my array. And I'm going to get an error message, no data found.

You'll notice that it did start to print everything out. But once it hit that hole in my array, it throws a no data found error. Any time you have a select statement in PL/SQL it needs to return a row, or else it's going to give you an error message. So in this case, we have our error message.

So what I can do is I can do another method. If emptable.exists j, then do this, else null end if. So I can do a conditional check to see if the index exists. So you notice that that allows me to avoid my error.

## Associative Arrays (INDEX BY Tables) - New - 14m

OK. So now what if I wanted to store a row of information in my assistive array? Well, what I can do in this case-- you know, if I wanted to do a select star rather than just selecting the last name into my associative array, what I would need to do is I would need to change my type.

And what I would is I would do this as an employees%rowtype. And then what I would have to do is I would have to go ahead and list the field name that I want to be able to interact with whenever I wanted to refer to it. So let me go ahead and run this. You'll see that I get basically the exact same results.

But I have the option, besides interacting, which is the last name, maybe I want the first name. Or maybe I want my salary. And so this is called an index-by table of record when I use the row type for my type definition of my associative array.

And so, whoops. I just highlighted one section there. There you go. So you notice I have all of my listed indices, and I have all of my salaries. And if I wanted to look at my hire dates, you notice I can do that as well. OK. So index-by table of scalar values or index-by table of record.

Pretty similar. Only three changes that I had to make in order to go from an index-by table of scalar to an index-by table of record. OK, so now let's go back to the book. And I think that should make it easier for you to understand what they're talking about here in the book.

So again, here is an associative array, where we have a key value pair. And in my case, my key was a PLS integer type. And so we have an employee here who wants to generate an expense report for each department, and so we're showing you what the associative array structure looks like.

The first column is our key. And here they're showing you that this one is a PLS integer. And as I mentioned, the indices don't have to go in any particular order with your associative array structures. That's why we have the methods to go from first to last. That's why we have the methods for next and prior. And then what is stored at the index key can either be a scalar value or a record value.

OK, so we are showing you the steps to create an associative array. Create the type. In this case, the type is a table of employees at last and present type. It looks pretty similar to what I just got through showing you.

And then we create the index-by table of that type. So in this case, we are defining a type of email_table, and it's a table of employees.email%type indexing by PLS integer. And then our index-by table is called email_list of the email_table type. And we are manually initializing each of those different values to our index-by table.

By the way, these should have a colon in front of those. email_list 100 colon equal SKING. email_list 105 colon equal DAUSTIN. email_list 110 colon equal JCHEN. It looks like something-- it looks like it got erased when we created the PowerPoints for this. And then we're printing out the values of email_list. email_list index 100 is SKING. email_list 105 is DAUSTIN. email_list 110 is JCHEN.

OK, now we're showing you how to create an associative array with a record. OK, index-by table of record. So we define the type that's of the departments%rowtype. Incidentally, in this one, we're indexing by VARCHAR2 length of 20, so that's our index. The index-by table is called dept_table.

And what we're doing in this case is selecting, into the dept_table, a row from department 10, so we're storing the whole row for department 10 in our index-by table. And now although they're saying index by VARCHAR2, you'll notice that their index is still an integer-based. So, you know, maybe you want to store the index with a VARCHAR2 when you want to do something like storing the value of the index-- or the value of the department record based on a department name.

Maybe my index is the department name rather than an integer value. OK. And I showed you guys the methods. So here they're showing you a couple of those methods.

We've got email_list.FIRST. We've got email_list.LAST. So we're able to see what the index first value is and what the index last value is. The first is 100. The last is 110 based on how we're populating those.

We also have another one called COUNT. I didn't show you that one, but if you wanted to know how many members are in your collection, you could use the COUNT method to tell you how many values are stored in your collection. And then here, we're using the method FIRST and LAST in order to iterate through our index-by table for i IN my_emp_table.FIRST dot dot my_emp_table.LAST. LOOP.

And then we're going to print out the last name of everybody stored in that collection, similar to what I showed you. OK, now nested tables, these are also collections. Collections are different than associative arrays, however. Nested tables can be stored as a-- or we'd like to say can be persisted as a database column type in a database table.

Nested tables represent sets of values. Nested tables can be used as column types in database tables. Each entry in the column of the database table can hold a set of values.

We're going to show you an example of this. The type is dept_mail, and it's a table of VARCHAR2 20. And then the name of the next table is called mails of the type dept_mail. And you notice how we're assigning the values SKING, NKOCHHAR, LDEHAAN, AHUNOLD. And that's going to automatically assign the subscripts in the order that those values are listed under dept_mail.

So SKING would be a subscript 1. NKOCHHAR would be a subscript 2, LDEHAAN a 3, AHUNOLD at 4. And then we're using the FIRST and LAST methods again to print out all of those emails. And then varrays. So with varrays, when you define those types, you do need to describe the maximum number of elements that are going to be used.

You can always extend those, or you can trim those. So what if you load up five emails, and all of a sudden, you need five more? So you can extend that out to 10 if you like, but the thing that is different with varrays is that they are nice and incremental. Our nested tables also are incremental. OK.

So you notice the sub scripts. These are like the indices in the index-by tables. The sub scripts are nice and ordered in this case. One, two, three, four, five. We don't have gaps in there, so we can't delete things out of the middle. We have to trim them from the end. So index-by tables are a little more flexible, because we can load up the index-by table and then delete things in the middle.

They don't have to be nice and ordered on the index values, where, nested tables and varrays, those are not as flexible in that regard. And so as I mentioned, you know, we don't really get into nested tables or varrays in this class, other than just showing you some examples.

So here, we're declaring the type email. Notice we're defining that is VARRAY 5. So we're going to hold up to five emails, if you want to think about it like that. Now we don't have to store five, but we have the potential to store up to five. You notice we're still only loading up that varray with three emails, and we've got room for two more in the event that you want to put two more emails in there. And those are going to be subscripts 1 through 5 in order to refer to those.

All right, so summarizing collections. Associative arrays are key value pairs. They're used only in PL/SQL blocks. Those cannot be persisted to the database. Nested tables are sequentially indexed data, can be persisted to the database as columns of a table. varrays are also sequentially indexed data with an upper limit, can be persisted in the database as columns of a table as well.

OK. That brings us to our quiz. Identify situations in which you can use the percent rowtype attribute. When you are not sure about the structure of an underlying database table. That is true. If you just want to do a select star, you can use the percent rowtype attribute. You don't have to know the structure of the underlying database table.

Letter b, when you want to retrieve an entire row from a table, that's true as well. Select star, right. Or when you want to declare a variable according to another previously declared variable or a database column, that's not rowtype. That's percent type. So letter a and b would use percent rowtype. Letter c would use percent type.

OK. So in summary, in this lesson, you should have learned how to define and reference PL/SQL variables of composite data types, PL/SQL records, associative arrays including index-by tables and index by table of records. How to define a PL/SQL record by using the percent rowtype attribute. And we also talked about the three PL/SQL collection types. Associative arrays, nested tables, and varrays.

So you are going to do a practice, where you're going to declare an associative array. You're going to process data by using associative arrays. Declare a PL/SQL record and process data by using a PL/SQL record. OK, so that is going to do it for chapter 7.

## Practice 7-1: Working with Composite Data Types - New - 23m

I will now demonstrate practices for Lesson Seven, working with composite data types. Now we actually have it looks like about three different problems on this one. So I will go ahead and start with the solutions so that you can see what's happening as I talk about what we're doing.

OK, so in step number one, we're asked to write a PLSQL block to print information about a given country. We're going to declare a PLSQL record based on the structure of the countries table. We're going to declare a variable called v_countryid and assign the string CA to v_countryid So let me go ahead and do that.

Now just to make sure that my DBMS output line shows me my data, I'm going to go ahead and do the command set server output on. Now, we're going to go ahead and do something called set verify off. This is a command that turns off a feature. If you use substitution variables, it turns off that repeat function of the SQL developer tool. So I'm going to set verify off. That's optional, by the way.

And then let's go ahead and start with our declaration section. So as instructed. We're going to create a variable called v_countryid. It's going to be a carchar2 size 20. And we're going to initialize that to the string of CA for Canada. All right, in step letter C, we want to create a record called v_country_record of the countries%rowtype. So let's go ahead and do that, v_country_record of the countries%rowtype.

All right, now in letter D, we are asked to start the executable section and get all of the information from the countries table by using v_countryid. And we want to display selected information about the country. So let's go ahead and start that section.

Since we're using a record, we're going to select star into our record, v_countryid, and-- or sorry, v_country_record from the countries table where the country ID equals the v_countryid variable. Now just to make sure that it is the correct case convention, because the country ID data is stored in uppercase syntax in this particular table, we're going to go ahead and use the upper function. And now here, in this case, because we've actually initialized it with an uppercase CA, it won't really have any effect on that particular assignment. But in case we make this where somebody could go ahead and supply that a runtime using something like a substitution variable, we'll want to make sure that we're always getting v_countryid in uppercase because the data, as I mentioned, is stored in the country ID column in uppercase.

All right, so next we want to go ahead and print out the information about the country. So we use the DBMS output.put line. We're going to put some labels here, it looks like. Country ID is going to be v_country_record.country_id. And then we'll concatenate that with-- we're going to do a space after that single quote so that our next label is kind of spread out a little bit, Country Name. And we'll concatenate that to v_country_record.country_name. I am going to just copy that record. And we'll just change that variable name or that field name there.

All right, let's concatenate that together to it looks like region information. And since that's still on my clipboard, I'll go ahead and paste that. And we'll just swap that out with region. And there we go.

All right, just double checking that I've got enough parens there to close out my grouping, looks good. OK, so let's go ahead and format that. It looks like I have an extra semicolon there. Let me form that. All right, let's go ahead and run it. And let's compare that with what the output looks like in the book. It looks good, country_id Canada, country_name, Canada-- or country_id CA, country_name Canada, region two, looks good.

And now it says you may want to execute and test the PLSQL block for countries with IDs DE, UK, and US. OK, so let's go ahead and do that. Let's just put UK. There you are. And let's try DE for Germany. There we are. And let's try US. There you go.

OK, so let's continue on to the next page, page six. It asks us to create a PLSQL block to retrieve the names of some departments from the departments table and print each department name on the screen, incorporating an associative array. And then it looks like we're going to save the script as lab_07_02_soln.sql.

So I'll go ahead and open up a new worksheet. So let's do a set server output on. We're asked to declare an index by a table called dept_table_type of the type departments.department_name. And then we're going to declare a variable my_dept_table of type dept_table_type to temporarily store the names of the departments.

All right, so we'll start out with the declare. And we'll define our type, dept_table_type table type is table of departments.department_name%TYPE. And then we'll index by pls_integer. And then the actual array is, the table name is my_dept_table. And the type is going to be dept_table_type.

All right, now I think what I'm going to do is just wrap that [INAUDIBLE] of the code there. OK, there is my type. And here is my index by table. All right, that looks good.

Next, in step letter B, we're going to declare two variables, one called f_loop_count and another called v_deptno of type number. We're going to assign 10 to a f_loop_count and 0 to v_deptno. So let's go ahead and do that. f_loop_count is a number type 2 on the precision. And it looks like we're going to initialize that to 10. And then v_deptno, and that's going to be a number size of 4 initialized to 0.

OK, now in step letter C, it says, using a loop, retrieve the names of of 10 departments and store the names in the associative array. Start with the department ID of 10. Increase v_deptno by 10 for every iteration of the loop. The following table shows the department ID for which you should retrieve the department name and store in the associative array. So departments 10 through 100, it looks like they increment by 10.

OK, so it looks like that's going to start with an executable section. Let's continue on to page seven. And yup, it looks like we're going to start with the executable section.

So we're going to do for i in 1.. f_loop_count-- remember, f_loop_count is set to 10. So we're going to loop 10 times. We're going to initialize the v_deptno variable. Right now it's set to 0. We don't have a department 0, so we're going to have to increment that. v_deptno initialize to v_deptno plus 10. All right, so now we'll have department 10.

And then we will go ahead and select the department name into the my_dept_table. And we're going to set the index using the i value. So the index of 10 is going to point to department 10.

From departments where the department ID equals v_deptno-- so select the name of the department. Store that in the array from the departments table where the department_id equals the variable, which we've set to 10. All right, and then we're going to have to have an end loop.

All right, now in step letter D, it says, using another loop, go ahead and retrieve the department names from the associative array and display them. So we'll do another loop. Now we'll just go ahead and reuse the i variable-- or the i implied counter.

Remember that this ceases to exist at the end of the end loop. So we'll go ahead and recreate it here. For i in f_loop_count, let's go ahead and loop. And we'll just print out the values from the index by table. Dbms_output.put_line my_dept_table-- and we'll refer to the value in the index coming from the i, the implied counter.

All right, let's go ahead and save this script as lab_07_02_soln.sql, lab_07_02_soln.sql. All right, let's run it. Aha, it looks like we have an error. Take a look at it. f_loop_count is not a cursor.

And that's going to be line 15 column 10. Let me look through my logic here. For n1 [INAUDIBLE] f_loop_count loop, [INAUDIBLE]. Ah, there we go, 1.. I left that piece off. Let's save it.

OK, so I forgot to do the 1.. It didn't know how many times to loop, because I was just pointing to the variable without a lower bound. So that will do it. All right, let's go ahead and run it. OK, there we go, administration through finance. It looks like it's exactly like with the book has.

OK, next, step number three, we're going to modify the block that you created in task two in order to retrieve all information about each department from the departments table. So instead of storing just the department name, it sounds like we're going to store the whole row and index by a table of record, it looks like is what we're going to do.

So what we're going to do, load Lab 7-2 solution. I've already got that. You have declared the associative array to be of the departments.department_name%type. Modify that so that we're using the ROWTYPE attribute instead. So let's go departments%ROWTYPE. All right, they want us to use the ROWTYPE attribute.

All right, let's go on the next page, compare that with what they did. And yup, it looks like they did exactly the same thing there. And then modify the select statement so that you retrieve all department information into the associative array. So rather than just selecting the department name, we're going to have to select star. And then we're going to have to come in and retrieve the department information from the associative array and display the information.

So let's just go in and change our dbms_output.put_line. Instead of just pulling back one value, we are going to have to reference the department number, the department name, the manager ID, and the location. So it's going to be indexed by table index.field_name.

I'll go ahead and do the first one. It looks like they want us to do a nice little label on that. So I will do a department number. And we'll concatenate that to my_dept_table, i, index value, dot department_id.

Now let's just run that, just make sure that runs. There we are. So departments 10 through 100, looks great. And then I think to save time, I'm just going to go ahead and copy that.

And we have four columns in the departments table. So it looks like we're going to go ahead and I have to add three more lines there. So I'm going to paste. I'm going to concatenate that. I'm going to paste. Oops. And then I'll concatenate that. And then finally, I will paste. All right, so department_ID, department_name, manager_ID, and location_ID.

And then of course, we have to change the label. So this will be Department name. This will be Manager ID. And this will be Location ID. It better give us this a space there so that the labels will print out correctly.

All right, let's go ahead and run that and see if we get some output that looks like the book. OK, Department Name, Administration Manager ID 200, Location ID 1,700, looks good. That's department 10.

All right, now, I don't think they want us to save this one. Yeah, they don't want us to save it. So let's just go ahead and-- well, I'll tell you what I'll do. I'll go ahead and save it as Lab 7-3 solution, although they don't tell us to do that. I will do it just in case they tell us to save it at some point in the future.

OK, so now I saved that as lab_07_03_soln.sql. I'll go ahead and close it. I am going to close this one. And I'm going to say no to save changes. And that way, I have it back to what it looked like originally. And it looks like we're all done with this one as well. OK, so that will conclude the demonstrations for Practice 7.
