# 16: Using Oracle-Supplied Packages in Application Development

* Using Oracle-Supplied Packages in Application Development - New - 18m
* Practice 16-1: Using the UTL_FILE Package - New - 16m

## Using Oracle-Supplied Packages in Application Development - New - 18m

OK, my friends, let's take a look at lesson 16, Using Oracle-Supplied Packages in Application Development. We are here in unit 4 working with subprograms in lesson 16, Using Oracle-Supplied Packages in Application Development. So after completing this lesson, you should be able to describe how the DBMS Output package works, how to use the utl file package in order to direct output to operating system files, describe the main features of utl mail, and describe the JSON data structures.

So identifying the benefits of using Oracle-supplied packages and listing some of those packages-- the Oracle-supplied packages are provided with the Oracle server. They extend the functionality of the database. They provide PL/SQL access to SQL statements, and most of the Oracle supplied packages are installed during database creation. Notice that modifying Oracle-supplied packages can cause internal errors and database security violations, and so you're asked not to modify the supplied packages.

So there are more than 200 different Oracle-supplied packages. Now, here is an abbreviated list of some of those Oracle-supplied packages, and we've already been using one of those, as you see-- the first on the list, which is the DBMS Output package. So the lesson agenda is how to-- or rather, an example of using the following Oracle-supplied packages, the DBMS Output package, the Utl File package, and the Utl Mail package.

So how does the DBMS Output package work? The DBMS Output package enables you to send messages from stored subprograms and triggers to other stored subprograms or buffer. The Put and Put_Line subprograms are going to place text in the buffer. The Get_Line and Get_Lines subprograms are going to read the buffer, and messages are not sent until the sending subprogram or trigger completes.

Now besides the DBMS Output package, we have the Utl File package. The Utl File package extends PL/SQL programs to read and write operating system text files. It provides a restricted version of operating system stream file I/O for text files and enables creating files and operating system directories defined by a create directory statement.

So here, we see on this page an example of how to create a directory. Now, not everybody can create a directory. You do need to be granted the Create Directory privilege in order to be able to do that. But what we'll do is we'll create a database directory that points to an operating system path, and the operating system path is where we will be interacting with the files. So let me demonstrate how to use the Utl File package.

So what I'm going to do-- I'm just double checking my directories list here, and you notice that I don't have any directories granted to me. So I'm going to create or replace the directory called Report star, and this is going to be the path in my os where my reports are going to be written. And I can actually open a terminal, and let's go ahead and navigate to that location.

So I'll CD to home, Oracle Labs, PLPU Reports, and you'll notice that I happen to have three files in there currently. So let me go ahead and create the directory, and then it should show up here under the directory list. I'm just going to refresh it, and you notice I have the directory called Report star.

Now, next, what I'm going to do is I'm going to use the utl file package in order to create a procedure called sal_status. I'm going to pass in the name of the directory, and I'm going to pass in the name of the file. Now, you'll notice that I have a cursor that's going in and selecting the last name, salary, and department ID and sorting on the department ID. I have a variable called v_newdept, and I have a variable called v_olddept.

Now what I'm going to do is I'm going to use what we call a file handle, and that's where my variable called f_file is. It is a special type of a variable which allows me to pass in multiple components into it to interact with a file. So you'll notice that I'm going to pass in a name of a directory, the name of a file, and what I'm doing to it. In this case, I'm writing to a file in that directory.

So I'm going to use my Utl File package in order to open that file for writing, essentially, in that directory. You'll notice that the file handle variable is getting initialized with that information, so every time I reference that file, it understands my directory name, my file name, and what I'm doing to it. And then I'm going to use the Utl File Put_Line in order to write a line of code, basically a report generated on today's date, and then a new line and then a combination of put lines and new lines where I'm going to end up putting the name of the department-- or rather the department ID along with the word "department." I'm going to be writing in the name of the employee and what they earn. And finally, after I'm done consuming all of the rows from the cursor, I'm going to put a line in my report that says end of report.

Now, the Utl File package also has some exception handlers as well, so I'm showing you a couple of those. We've got one called invalid file handle. Maybe it doesn't have the correct directory name, for instance, and maybe I don't have the ability to write to a file. Maybe I don't have the write privileges in that directory for instance, and so I'm going to handle that one with that. So in each case, we're going to reference the package name Utl File and then one of the subprograms or putting in the file handle name into those different subprogram calls.

So let me go ahead and create the procedure called sal_status, and then when I run it, I need to pass in the name of the directory-- that's what I called it up here, reportsdir-- and then the name of the file as well. So before I run that, I just wanted to show you that I do not have the file out there called sal_report2. Oh, I guess I do, so let me change the name-- sal_report3. And so let me execute it, and it looks like it successfully completed. So now if I go back and relist what's in that directory, you'll notice that I have a sal_report3, and what I can do is I can go in and open that so that you can see what that file looks like.

So there you go-- report generated on the 29th of June '20. I'm writing the department ID, the employee name, and what they earn. The next department-- the employee name and what they earn.

It looks like there's two people in department 20. Department 30 has a few employees in that, and we basically print out information about all of the employees inside of each one of the departments until we've consumed all of the employees in the cursor. So there you go. That is an example of one of our packages that is supplied by the Oracle database.

Now, there is a listing of some of the subprograms that's available there in the Utl File package. The Is Open function, for instance, determines if a file handle refers to an open file. There is an F_Open function, an F_Closed function, an F_Copy procedure, an F_getattribute procedure-- tons of different procedures and functions, as you see.

Now, not only can we write to a file, but we can also append onto an existing file by using the same file handle. Or we can read data that's already in a file at that directory location. Now, I showed you an example of two different exception names that are in the Utl File package, but there's actually more exceptions that are available. So here is a listing of the different exception names-- invalid path, invalid mode, invalid file handle, invalid operation, read error, write error, and internal error.

Now, the F_open and Is_Open functions-- so the F_Open function opens a file for input or output. And this one is expecting, of course three parameters-- the name of the directory, the name of the file, and what we're doing to it, whether we're reading, writing, or appending. And then the Is_Open function determines whether or not we have opened that particular file handle or whether we've actually opened that file for writing or appending.

So this example in the book is similar to what I showed you. So in this case, we're writing to a file, and they're showing you, at the end, we're going to close the file. And then we've included the two exceptions that you see there. Now, in addition, to the Utl File package, we have the Utl Mail package, and this one is a utility for managing email. It requires the setting of the SMTP_Out_Server database initialization parameter and provides the following procedures-- a send procedure for messages without attachments, a send_attach_raw for messages with binary attachments, and a send_attach_varchar2 for messages with text attachments.

Now, in order to setup and use the Utl Mail package, the DBA is going to have to do some of this. They're going to have to install the Utl Mail package and define the SMPT_Out_Server initialization parameter. The DBA then needs to grant the users the required privilege, and then if you're a developer, and you have been granted the privileges, you can then invoke the Utl Mail subprogram and send an email.

So we're going to show you the three subprograms that are part of Utl Mail. We've got send, we've got send_attach_raw, and send_attach_varchar2. So we're showing you how the DBA would go in and install the Utl Mail package. So the first file, that is called utlmail.sql, is the file that contains the specification for the Utl Mail package.

The second file that you see there, called privatemail.plb, that is the file that contains the package body. Now, the .plb extension means that file is actually obfuscated, so you can't actually look at the logic from inside the package body. But you can go ahead and-- or the DBA can go ahead and run that package, and it'll go ahead and install the Utl Mail package body.

And then the DBA needs to set the SMTP_Out_server. And notice that they're doing that, and that's a system level parameter. And then as a developer, we would then invoke a Utl Mail procedure.

So the one we're showing you is the send procedure. We have the parameters for the sender, email address, the recipient email address, the message, and the subject line. And you'll notice that we're using mixed notation for parameter passing there. We start out with positional, and then change to named, and so that's what we call mixed notation.

So this is the signature for this send procedure. You notice that the sender and recipients do not have any defaults. So you have to provide a sender email address, and you also have to supply a recipient address.

Now, you'll notice that the message parameter is also a mandatory parameter because it does not have a default. So minimally, you would have to provide the sender, the recipient, and the message in order to send an email. Everything else has a default, and so you could skip over carbon copying, blind carbon copying, or having to provide a subject line, for instance.

Now, the send_attach_raw procedure-- this allows us to send raw attachments. And what we will do is have the ability to provide-- I'll show you the example-- the attachment using the Get Image function, and you notice we are getting the image called oracle.gif. It's going to be attached in line according to the true parameter there. The mime type is an image/gif, and then the file name for the attachment is going to be oralogo.gif. And you'll notice that we've also supplied the sender, the recipients, and the message as well, and also, by the way, the subject and mime type.

Now, if we wanted to send a varchar2 attachment, the signature list looks pretty similar to this send_attach_raw procedure, and here, we have an example of that. The name of the file that we're attaching is notes.txt. The name of the file for the email is going to remain notes.txt, and you'll notice that it has the similar parameters that we showed you in the previous example. So pretty simple-- you just supply the correct parameters, and it'll send an email.

So that brings us to our quiz. The Oracle-supplied Utl File package is used to access text files in the operating system of the database server. The database provides functionality through directory objects to allow access to specific operating system directories. And that is actually true.

So that is going to do it for the demonstrations of practice 16, but I do want to point out that we do have a lab. You're going to use Oracle-supplied packages in application development. This practice is going to cover how to use the Utl File package in order to generate a text report. So I'll let you go ahead and do that, and that'll do it for my demonstrations for lesson 16.

## Practice 16-1: Using the UTL_FILE Package - New - 16m

I will now demonstrate practices for Lesson 16, Using Oracle-Supplied Packages in Application Development. In the overview, we see that in this practice, you will use the UTL_FILE package to generate a text file report of employees in each department. It is recommended that you run the cleanup_16.sql script.

OK. I will go ahead and start with the solution, which is going to be down on page 4. And in this practice, you're going to use the UTL_FILE package to generate a text file report of employees in each department.

You first create and execute a procedure called employee report that generates an employee report in a file in the operating system using the UTL_FILE package. The report should generate a list of employees who have exceeded the average salary of their departments. And finally, you're going to view the generated output text file.

So what we'll do is we will create a procedure called employee report that generates an employee report in a file in the operating system using the UTL_FILE package. The report should generate a list of employees who have exceeded the average salary of their department.

Your program should accept two parameters. The first parameter is the output directory. The second parameter is the name of the text file that is written. We want you to use the directory location value UTL_FILE. We want you to add an exception handling section to handle errors that may be encountered when using the UTL_FILE package.

Now if you prefer, you can go ahead and run the solution 7 SQL script. And we ask you to uncomment and select the code under task number 1.

So I'm going to go ahead and show you how to create the directory, because I don't think that you actually have this directory in existence. And we are going to have you execute this procedure by reporting to a directory called REPORTS_DIR.

So I will go ahead and show you how to do that, first of all. What I'm going to do is I'm going to create or replace directory REPORTS_DIR as. And then I'm going to do the path in the operating system where I want my file to be written to.

So it will go to home/oracle/labs/plpu/reports, if my memory serves me correctly. Let's navigate there and just make sure that that is valid. I'm going to open up a terminal. And I'm going to cd to that path just to make sure that I'm remembering it correctly. OK, looks like that's the correct path.

OK. So what we'll do is go ahead and execute that. And you notice that it says that the directory REPORTS_DIR is created. And if you go into your directories category over here in the object tree and expand that, you should see that REPORTS_DIR directory. You may end up having to refresh the directory in order for that to show up if it does not automatically refresh.

OK. So now that we have the directory created, what we will do is go back and create the procedure. We're going to create or replace procedure, and we'll call it employee_report. And this is going to accept two parameters.

The first parameter is going to be our directory for a p_dir parameter, and the second one is going to be our p_filename. And that one's going to be of varchar2 type.

OK. Now I'm going to create a file handle called f, and the type of my file handle is going to be a utl_file.file_type This is a built-in file handle type built into UTL_FILE.

And then I'm going to define a cursor. And we'll call it cur_avg. And this is going to be a simple little select statement. last_name, department_id, and salary from the employees table. And this is going to be a correlated subquery, so we'll name it outer for our alias for the table.

Where the salary is greater than, and then our subquery is going to select the average salary from employees where the department_id equals our outer department_id. OK. And it looks like we're going to sort that as well. So let's do an order by department_id.

OK. Next, we'll do our executable section. And we're going to initialize our file handle to the utl_file.fopen. And we're going to pass in the name of the directory through the parameter, and the name of the file name through our parameter, and we're going to pass into a capital W for a write, W meaning write rather than read.

Next what we'll do is we'll put a line of code, utl_file.put_line. And we're going to print out-- actually, we're going to put a reference to the file handle, because every time we use UTL_FILE we have to reference the file handle so that it knows the directory, and the file name, and what we're doing to it.

And we're going to put, "Report generated on," and we'll concatenate that with sysdate. And then we'll do a utl_file.new_line. And again, we'll pass in our file handle reference.

OK. Then we're going to do a cursor for loop. We're going to put utl_file.put_line. Again, we'll reference the file handle. What we're going to do is we're going to rpad the last name to 30, and we're going to concatenate that with a space.

And that's going to be concatenated to an lpad of the department_id. And in the event that we have somebody that doesn't have a department_id, we're going to use the nvl function. Oops, looks like I spelled department incorrectly.

And we're going to do 9999. In the event that we don't have a department_id, it's going to be listed as 9999. And then we're going to put a hyphen. And then we're going to do 5.

That's going to be concatenated to a space. And that's going to be concatenated to another lpad. And we're going to do the salary this time. And then we'll do our end loop.

OK. Then we'll do a utl_file.new_line. Again, referencing our file handle. And then we'll put a final line of code. And we'll put, end of report. And then we'll close our file using utl_file.fclose. Again, passing in the file handle. And then that'll end our procedure.

So let me format this. And let's just look through it and make sure that the code makes sense. OK, and what I'm going to do is just wrap some of this code around so we can see it all. There we are. Oops.

Let me do that with some of this so you can see it. The trouble with doing demonstrations is trying to show the book. Sometimes my window is not wide enough. OK, well, I'll tell you what. Let's go ahead and compile it and see if we have any errors on creating the procedure. Looks like we're fine.

OK. So let's go ahead and expand the procedures category. And let's refresh our procedures. And let's look for the employee_report subprogram. There it is.

All right, so it looks fine. Let's go ahead and invoke it. So in step number 2, we're going to use the REPORTS_DIR directory as the alias for the directory object as the first parameter. And then we're going to use the sal_rpt71.txt as the second parameter.

So I'm going to go ahead and copy that code out of the book. It's simple enough. Oops. It didn't like my shortcut for copying, obviously. OK. EXECUTE employee_report REPORTS_DIR sal_rpt71.txt. Let's execute it.

OK. Successfully completed. Let's go to that directory location. cd /home/oracle/labs/plpu/reports. And we have a sal_rpt71. Let's invoke that with gedit. And it looks like we were successful in writing our report.

OK, so let's go back to the book. And that is what they're showing us here. And it looks like it looks just like what the book said it should look like, other than the date on the report.

OK, my friends. So that is going to do it for the demonstrations for practices for Lesson 16.
