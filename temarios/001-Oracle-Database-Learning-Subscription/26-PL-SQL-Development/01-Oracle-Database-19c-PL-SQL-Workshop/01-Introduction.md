# 1: Introduction

* Introduction - New - 17m
* Practice 1-1: Getting Started - New - 19m

## 01 Introduction - New - 17m

Welcome to Oracle Database 19c-- PL/SQL Workshop. This is the introduction chapter. And for this lesson, we're going to go over the objectives for the lesson first up. And we see that after completing this lesson, you should be able to do the following-- discuss the goals of the course, describe the HR database schema that is used in this course, identify the available user interface environments that can be used in this course, and reference the available appendixes, documentation, and other resources.

Next, we're going to take a look at the course objectives, as well as the course agenda. For the course objectives, we see that, upon completing this course, we should be able to identify the programming extensions that PL/SQL provides to SQL, write PL/SQL code to interface with the database, design PL/SQL anonymous blocks that execute efficiently, use PL/SQL programming constructs and conditional control statements, handle runtime errors, describe stored procedures and functions, create packages, and create triggers.

We see next that we have the course roadmap. In unit 1, called Introducing PL/SQL, we are going to have a lesson on an introduction to PL/SQL, a lesson on declaring PL/SQL variables, another lesson on writing anonymous PL/SQL blocks. Lesson 5 is using SQL statements in PL/SQL blocks.

In unit 2, entitled Programming in PL/SQL, we're going to write control structures, work with composite data types, use explicit cursors.

In unit 3, entitled Working with PL/SQL Code, we're going to teach you how to handle exceptions, and an introductory look at creating procedures and functions.

Continuing on with unit 4, entitled Working with Subprograms, we're going to break out into individual chapters creating stored procedures, creating functions, debugging subprograms, creating packages, working with packages, using Oracle-supplied packages in application development, using dynamic SQL.

And in unit 5, we're going to work with triggers. Lesson 18 is called creating triggers. Lesson 19-- creating compound DDL and event-based triggers.

Finally in unit 6, entitled working with PL/SQL code, we have lesson 20 on Design Considerations for PL/SQL code, lesson 21 on using the PL/SQL compiler, and lesson 22 on managing dependencies.

Now, let's take a look at the schema and dependencies used in this course. So we're going to use a schema called Human Resources for this course. The schema already has some tables built into it.

And here we have a summary of what those table names are entitled. Now it does have the table names as well as the column names listed on this page. And you notice that the columns that are highlighted in blue are the columns that contain the primary keys.

Now this page also shows the relationship between the different tables. So for instance, employees work inside the departments. Departments are assigned to locations. Locations are located in countries. And countries are inside regions.

Now, sometimes that relationship goes the other direction. For instance, we have some managers which manage departments. And so you notice not only do we have a relationship between employees and departments, but we also have a relationship between departments and employees. The other relationship besides managers and departments is department IDs which are assigned to employees.

Now let's take a look at the course agenda. For the first day, we're going to look at the introduction chapter. And then we'll go into an introduction to PL/SQL, a chapter on declaring PL/SQL variables, writing executable statements, using SQL statements within a PL/SQL block, and writing control Structures

On the second day of the course, we're expected to look at working with composite data types, using explicit cursors, handling exceptions, introducing stored procedures and functions.

On the third day, we're going to look at creating procedures, creating functions, debugging subprograms, creating packages.

On the fourth day, we're going to work with packages using Oracle-supplied packages in application development, using dynamic SQL, as well as creating triggers.

And finally on the final day of the course, we're going to create compound DDL and event-based triggers, a chapter that is performance-based called design considerations for PL/SQL code, and tuning the PL/SQL compiler. We'll also have a chapter on managing dependencies.

So as far as the class account information, we have actually cloned the HR account into three different accounts. We have an ora41 account, we have an ora61 account, and we have an ora62 account.

The ora41 account and ora61 accounts are the accounts that we are going to use for the full five days of the course. The ora62 account is used if you decide to go in and also attempt to do the additional practices.

Now, the password is provided in the Activity Guide. In the Activity Guide, what you want to do is look for a page that has the credentials. And that's usually towards the front of the Activity Guide, usually around page 5 or 6. Each machine has its own complete environment and assigned the same accounts.

Besides what we cover in class, we also have these additional appendixes. Appendix A, Table Descriptions and Data, Appendix B, Using SQL Developer-- and that, by the way, is the tool that we're going to use in this class mostly-- Appendix C on Using SQL*Plus, which is a command line, Appendix D, Commonly Used SQL Commands, Appendix E, Managing PL/SQL Code, Appendix F, Implementing Triggers, Appendix G, Using the DBMS_SCHEDULER as well as the HTP Packages.

Now as I mentioned, we also have an Activity Guide. The Activity Guide is where you're going to go in and do the practices. And also, by the way, we also have the solutions for the Activity Guide. Just in case you wanted to run solutions for any of the chapters, we do have references in the Activity Guide so that you can go in and run the solutions rather than having to hand type or hand code yourself.

So let's take a look at the overview of Oracle Database 19c and related products. So the focus areas of the Oracle database are information management, Oracle Cloud, application development, and infrastructure grids.

Now, application development, what we're talking about there is you can use several different tools to build applications in the Oracle database. We have Application Express that you might use to build applications within the database. And Application Express also fully supports PL/SQL, as well as those other elements on the page also supporting PL/SQL.

The 19c Oracle database also includes high availability features, performance features, security features, information integration, and lots of tools for manageability, such as Oracle Enterprise Manager Cloud Control. As far as the available PL/SQL all development environments, we do have several different environments that are available in order to write PL/SQL.

Now we have Oracle SQL Developer, which we will use in this course. We also have Oracle SQL*Plus, which is a command line tool that's also built in to this class.

Now although we have Oracle SQL Developer Web listed as one of the tools that is available in PL/SQL, we do not have that actually set up in your lab environment. We will talk about that more in just a moment as far as what is Oracle SQL Developer Web.

So Oracle SQL Developer is a free graphical tool that enhances productivity and simplifies database development tasks. You can connect to any target Oracle database schema by using standard Oracle database authentication. And as we mentioned previously, we're going to use SQL Developer in the course.

The specifications of SQL Developer are that it is developed in Java. It does support Windows, Linux, and Mac OS 10 platforms, enables default connectivity by using the JDBC Thin driver, connects to Oracle database version 9.2.0.1 and later, and also connects to Oracle database on Cloud as well.

Now here we have a screenshot of what the SQL Developer interface looks like. Now the one that is listed here is version 19.1. You may have a different version available to you in your labs. But the interface itself has the same look and feel from earlier versions up to the most recent versions.

So if you learned to use it in 19.1 and you end up having an install that is version 4 of SQL Developer, you should be able to use it if you learn on a later version.

Now, if you're coding in SQL*Plus, now we have an example here on this page of logging into the database. Now what we're doing in this case is logging in as a user called HR. And we're also showing you that, once you're logged in, you will get an SQL prompt. And that's where you can go in and start writing your PL/SQL code. I might add that you can also write SQL code there, if you prefer.

Now SQL Developer Web is a browser-based application that uses Oracle REST Data Services, also known as ORDS, to provide me any of the database development and administration features of the desktop-based Oracle SQL Developer.

The SQL Developer Web user interface has three components. It has a header at the top, a page body. And the page body content varies depending on which page you're viewing. It also has a status bar at the bottom.

So here we see the header at the top. And you notice that here it says Description of the illustration header.png, and then the page body.

Now this has a hamburger icon. And so depending on what you click on, the content is going to vary depending on which page you are viewing. You can use the Selector icon to control what you are viewing. And you'll notice here we've got a dashboard as well as SQL Developer listed. And the SQL Developer Web user interface has a status bar at the bottom as well.

So how do we access Oracle SQL Developer Web? It does run in Oracle REST Data Services. And access to it is provided through schema-based authentication. To use Oracle SQL Developer Web, you have to sign in as a database user whose schema has been enabled for SQL Developer Web.

In Oracle Autonomous Database databases, the admin user is pre-enabled for SQL Developer Web to enable another database user schema. On the SQL Developer Web login page, we would enter the username and password of the database user for the enabled schema, then click Sign In. And the worksheet page would be displayed.

Now let's go ahead and take a look at the Oracle documentation as well as additional resources. You notice that we have Oracle Database PL/SQL Language Reference, Oracle Database Reference, Oracle Database SQL Language Reference, Oracle Database Concepts, the Oracle Database PL/SQL Packages and Types Reference, Oracle Database SQL Developer User's Guide, the Two-Day Developer's Guide, and Getting Started with Oracle Cloud.

As we start getting into the course, I will go out and show you on the web where you can access some of these different resources, as well as we have some additional resources for self-study-- for instance, Oracle Database-- New Features self-study. We also have a what's new in PL/SQL in Oracle Database on OTN, and the online SQL Developer home page and the SQL Developer tutorial available at the two URLs that you see on your screen.

So that's going to wrap it up for the introductory lesson. We should have learned how to discuss the goals of the course, describe the HR database schema that is used in the course, identify the available user interface environments that can be used in the course, reference the available appendices, documentation, and other resources. And that will conclude demonstrations for chapter 1.

## 02 Practice 1-1: Getting Started - New - 19m

I will now show you demonstrations for practice 1. This is your student lab desktop. And it may look similar to what yours looks like.

Now my SQL Developer icon used to be over here on the left. But what I want to do is I want to organize my icons so that as I am demonstrating to you that I can have my SQL Developer on one side of my screen. And I can display my Activity Guide on the left-hand side of the screen.

Now as far as the environment, I do have a copy of my Activity Guide. And it is located underneath our Home directory underneath the Labs directory. You'll notice that I actually have a directory called Activity Guide.

You should have something similar. It's most likely called Student Guide. And inside of that you should see that you have some different PDFs. And those should be the same materials that you were able to download.

Now as far as the activities, each chapter has an activity that follows the demonstrations. Now this chapter here, this is my security credentials. So I think what I'm going to do, I'm going to go ahead and open that first, because I wanted to describe the different users that we're going to be creating in this particular environment.

So we have three different schemas that we'll be connecting to-- schema ORA 41, schema ORA 61, and schema ORA 62. Now they have the same objects inside of each of these.

We are going to use the My Connection description to connect to ORA 41 for about the first two days of the class. For the last three days of the class, we're going to create another connection also called My Connection. But you'll notice that we have a difference in the case sensitivity of the connection name.

The second My Connection is going to be used to connect to the schema called ORA 61. And that's what we're going to connect to in order to do labs for the last three days of the class.

If you choose to do the additional practices, then you will also be creating a connection to ORA 62 by using a connection called Video Company.

Now you'll notice that the password is the same for all three of my different users. It's cloud_4U. So that's what I'm going to memorize right now because that's the little piece of information that I'm going to need. And I'm going to go into my first practice. This should be the practice for lesson 1.

And the practice for lesson 1 starts out by showing us the overview. In these practices, you perform the following. You're going to start SQL Developer. You're going to create a new database connection. You're going to browse the schema tables. And you're going to set an SQL Developer preference.

Notice that all written practices use SQL Developer as the development environment. Although it is recommended that you use ask SQL Developer, you can also use the SQL-plus environment that is available in this course.

Now, the way that the labs are organized, we have the labs listed out. And it basically shows you the instructions without any screen shots. So for instance, start SQL Developer in step 1.

In step 2, create a database connection by using these different parameters. And step C, it's talking to the password that we just looked up in the security credentials document.

Now again, your password's probably listed on about page 5 or page 6 of your Activity Guide. That's usually where we put those on the production version of the activities. So that's where I would look. I would look in your Activity Guide on about page 5 or 6 to get your password.

But what I wanted to point out is that we actually do have solutions listed as well. Now, the solutions includes screenshots. So they're a little bit more descriptive than what it's telling you in the base instructions.

So for instance here, start SQL Developer. Down here on page 5 is where the solution starts. Notice it says start SQL Developer. And it tells you how to do that. Double-click the SQL Developer icon on the desktop.

So probably what I would do is I would probably favor using the solutions for you to do your labs for this course, because it does include screenshots. It does include the code that you're going to be writing. And you might end up using both methodologies. You might want to try something without looking at the solutions.

But for my demonstrations, I'm actually going to have the solutions listed so that you'll see how I looks in the solutions and you'll also see how that looks live so I'm going to start with number 1, start SQL Developer. Now I'm not going to double-click my SQL Developer icon on the desktop. I'm going to right-click and click on Open, instead. That's just my preference I wanted to show you that there's more than one way to start SQL Developer.

By the way it is technically SQL Developer, but you will hear me call it SQL, just like PL/SQL, ask you you'll hear me call that PL/SQL SQL at some point during the course. I started out by calling it PL/SQL rather than P-L-S-Q-L. And I started out by calling S-Q-L SQL when I started many years ago. And it's a hard habit to break.

So I'm going to create a database connection here in step number 2. Notice there is a hint that tells you, select the Save Password checkbox. You notice that we have a screen shot down below of what that's supposed to look like.

So let me right-click my Oracle connections. I'm going to click on New Connection. And what I'm going to do is I'm going to name my connection the same as what the book is telling us to name it. MyConnection. Notice the case sensitivity that they're having us do.

Username-- ORA41. Password-- if you remember that from the security credential document, mine was cloud_4U. I'm going to put a tick in the box for Save Password.

Down here where it says service name, I'm going to put ORCLPDB1. And then I'm going to click Test. And you notice that I have a status of success.

Just double check that I have my Save Password checked. And I'm going to go ahead and click Save. And I now have the connection saved over here on the left.

Now on the next page, on page 6, it does show those steps that I just demonstrated. You click on Test, as long as you get the status of success. Now they have you just click on Connect in the instructions. That's going to automatically save your connection.

I typically like to click Save and then Connect. So I'll go ahead and click Connect Now, as instructed in letter B.

And in the Activity Guide, page 7, you see that we want to browse the structure of the employees table and display its data. So in order to do that, what we're going to do is we're going to expand the connection for the MyConnection user. We're going to expand the tables category by clicking the little plus sign.

And then in order to display the structure of the employees table, we're going to look for the employees name and we're going to click on it, just a single click. And here it's showing us the structure of the employees table. It has the column names. It has the data types.

Next, step number 5, we're going to use the Data tab to view the data in the employees table. So that's what I'm going to do next. I'm going to click on the Data tab. And this is what the data looks like in my employees table.

Now in step number 6, we're asked to use the SQL worksheet to select the last names and salaries of all employees whose annual salary is greater than $10,000. We want to use both the EXECUTE statement, which is an F9 shortcut and the Run Script button, which is the F5.

And then we're going to review the results of both methods of executing this SELECT statement. We're asked to go ahead and take a few minutes to familiarize yourself with the data or consult Appendix A which provides the description and the data for all the tables in the HR schema that you'll use in the course.

So to display the SQL worksheet, click the MyConnection tab. And what I'm going to do is I'm going to click right there on the MyConnection tab. And you notice that I have a worksheet.

Now this tab as we see was opened previously when you drilled down on your database connection. You can open up another worksheet by selecting this icon right here. I can click the little dropdown. And I can click on my connection. And I can open up another connection window, another worksheet.

These are the same session, by the way. But that's how you open up a worksheet in case you want another worksheet to open.

Next, what we're going to do is we're going to go ahead and write the query that you see on the screen-- SELECT last name, salary from employees WHERE salary is greater than $10,000.

Now they want us to show you how to run that as a statement, as well as a script. The statement, you'll notice the shortcut is Control-Enter or F9. And you'll notice that the Run Script button is an F5. Or you can just simply click on those buttons. I think what I'll do is go ahead and click on the Run Statement button, and show you what the output looks like.

By the way, you notice this is a little more interactive. You can drag these columns around in the results. And then the second button is a run script button. And if I click on that, you notice that I get my data listed in a little more command line-looking output.

So usually I run SQL statements with the Run Statement button. With PL/SQL, because it has also usually additional commands, I usually run PL/SQL using the second button, or the Run Script button. So I would recommend that you go with that methodology as well.

Next, we're going to set some preferences. So one of the things I'm going to set is the size of my font just to make sure that it's large enough for you to read my font when I do my demonstrations.

So what I'm going to do, I'm going to go to Tools and I'm going to go to Preferences. And I'm going to go to where it says Code Editor, and I'm going to expand it. And I'm going to click on Fonts. And I'm going to bump mine up to about an 18. And then I'm going to click OK.

That way, you can see my code a little better. And so I can see my code a little bit better.

Now in the book, step number 7, they do show you how to get to the preferences. So again, I'll go Tools, Preferences. And then in step number 8, we're going to Select Database, Worksheet Parameters, in this Select default path to look for scripts text box. And we're going to browse for the home/oracle/labs/plsf directory.

So I'll go ahead and do that. I'll go to Database, Worksheet. And here is where they're talking about-- Select default path to look for scripts. I'm going to go ahead and browse.

And I'm going to look for the directory that they are recommending-- home/oracle/labs/plsf. And again, go ahead and click Select. And notice that path matches the path as described in the book. Now notice this directory contains the code example scripts, the lab scripts, and the practice solution scripts that are used in this course.

Next, we're asked to go ahead and familiarize ourselves with the structure of the home/oracle/labs/plsf directory. So let me go ahead and demonstrate that. Let me click OK on my Preferences window. And then again, I come up here to where it says File, Open.

And I'm going to select the PLSF directory, which is right here. And you notice that it's telling us it has three sub-directories-- Code Examples, Labs, and Solutions. So I if open up Code Examples you'll notice that we have code examples for lessons 2 through 10.

Now if I go up a level and go to the Labs directory, you'll notice that we have several labs as well. The APs are the additional practices, by the way, in case you choose to do those.

Let me go back up a level. Let me go to the Solutions and open that. And you notice that we also have the solutions for the different labs.

And then you can also use the Files tab to navigate through the directories to open the script files, using the open window and the Files tab, navigate through the directories and open a script file without executing the code.

So I'll go ahead and open up a solution, for instance, for lesson 2, and click Open just so you can see what that looks like. And you notice that this includes the solution for chapter 2.

Let me go ahead and close the worksheet. I'm going to go ahead and click on No on that. Let me close the employees table. And now it says to close any SQL worksheet tabs, click X on the tab as shown. And just make sure that it looks somewhat like mine looks like.

I've closed out all my scripts. I've closed out all my worksheets. And we are ready to continue on with the next chapter at this point.

So that's going to finish up the demonstrations for chapter 1 where we went in and set up our connections.
