# 21: Tuning the PL/SQL Compiler

* Tuning the PL/SQL Compiler - New - 25m
* Practice 21-1: Using the PL/SQL Compiler Parameters and Warnings - New - 16m

## Tuning the PL/SQL Compiler - New - 25m

OK, my friends, let's take a look at lesson 21, Tuning the PL/SQL compiler. We are here in unit 6, Tuning the PL/SQL Compiler. The objectives-- after completing this lesson, you should be able to use the PL/SQL compiler initialization parameters. You should also be able to use the PL/SQL compile time warnings.

So the PL/SQL initialization parameters-- the PL/SQL compiler implicitly rearranges the code for better performance. The compiler behavior is defined by its initialization parameters. You can use initialization parameters to tune the performance of the compiler according to the application requirement.

So we have a number of different compilation parameters that can control your PL/SQL compilation. For this class, the ones that we're concerned with are going to be the PL/SQL code type and the optimization level. So we can actually control the optimization level through SQL Developer. Let me show you where this is done.

So if I'm in SQL Developer, and if I go to Tools, and if I go to Preferences, and if I go to Database, and if I go to PL/SQL Compiler, you'll notice that I have an optimization level of 2. Now, we've got optimization levels from 0 to 3. 0 is turned off. Level 3 is the top level of optimization.

Now, we recommend level 2 for most of the PL/SQL code, and so you'll notice that's what it's defaulting to here in SQL Developer. So I'm going to go ahead and leave mine set to 2. Also, I want to point out, because we're going to be talking about this coming up in the second half of the chapter, this is also where we can go in and enable the different types of warnings.

Right now, we don't have any warnings that are enabled, but we have three categories of warnings. We have informational, we have severe, and we have performance. You can enable all of those warnings, or you can enable just the categories of warnings that you want to see. And so you can set the optimization level as well as your warning preferences through this interface in SQL Developer.

So if we look at the dictionary view, user PL/SQL object settings, what I'm going to do is I'm going to look at the PL/SQL code type and PL/SQL optimized level. This, again, is the one that we saw was set to 2 by default in SQL Developer. Now, for production purposes, the recommendation for most PL/SQL code is going to have PL/SQL code type of native rather than interpreted.

Interpreted code is the PL/SQL code type that you would want to use if you're using the debugger because the debugger can't work with natively compiled code. Natively compiled code, however, can run up to 30% quicker for the PL/SQL components when it's stored as natively compiled code. So to the benefit of that performance boost potentially, you should set your PL/SQL code type to native.

So we can set the optimization level in SQL Developer. We can also set it at the session level, or at the system level if you have the permissions to do that. But this is how you also change your PL/SQL code type.

So if I wanted to go ahead and change my demopkg package to native and 2, what I would do is I would alter my session, and I would set the PL/SQL code type to native. And then I would go to my package, and I would recompile it. And let me compile my package body as well. And now, let me go back and take a look at my user PL/SQL object settings, and what you will see is that my package is now stored as natively compiled code with an optimization level of 2. So really easy to do.

Now, let me go back in the book and show you what I was just talking about. Now, interpreted is the default, because we figure when you install the database, you're going to want to write some PL/SQL code, and you're going to want to debug it. So interpreted as the default so that you can debug it. Level 2 is the default for the PL/SQL optimized level.

Now, in 19c, to compile PL/SQL units for debugging, you want to specify PL/SQL optimized level equal 1, and then compile for debug. So there is the view, user PL/SQL object settings that I was talking about. This is also showing you all of the columns that are part of that particular view, and they're showing you how to go in and query that, as I mentioned.

Now, once you set it, because we're setting ours to this session level, you do have to be careful about going into another session. Let me open up another worksheet, and what I'll do is I will say alter package demopkg compile. And what's going to happen is it's going to use whatever is set for this session. And when I go back to my session and lookup again and see what my package is set to, you're going to notice that it's back to interpreted mode.

So what you can do is-- now, let me recompile this as native. Let me just right click and compile it again-- or actually, I'll just say alter package demopkg compile so that I can get it back to native. Let's just go see if it's back to native. There we are.

So what you should do if you want to preserve whatever your optimization level and code type is, you should put in this clause, "reuse settings." When you do that, it will look up what the settings are for the object as is right now, and it will not overwrite those settings when you recompile the package. So let me do that. I've recompiled it, but when I come back to this session, you'll notice, when I re-query the user PL/SQL object settings view, you'll notice they're still set to native. So that's going to be a recommended practice if you want to make sure that you're not changing those parameter values.

So they're showing you here, alter session set PL/SQL optimized level equal 1. Alter session set PL/SQL code type equal native. Go in and create the object or recompile it, and then when you go in and look at the user PL/SQL object settings view, you notice that this one is set to native.

Now, your warnings-- I haven't really received any warnings back. Let me go in and make a change in my preferences again, and what I will do is I will enable all my warnings. And then I'm going to go in and recompile maybe one of my subprograms that has outmode parameters in it.

This time when I compile it, I should get some warnings. I get two warnings. It says, Get Employee omitted the optional Authid clause, which we talked about in the last chapter. Default value Definer used. And it also says, parameter P_Job may benefit from the use of the NOCOPY compiler, which, again, we talked about in the last chapter.

So that's how you get your warnings to show up. Now, we have several different ways to work with our warnings we can use the alter session command to set those warnings.

Now, these are the different categories of warnings. We're enabling severe. We're enabling performance. We're disabling informational.

So I can go ahead and do that, and tells me my session is altered. And then I can come in and maybe do individual ones if I want. Rather than set all three of those, I could just set one of them. And what I can do is I can actually go in and use the DBMS Warning package in order to get the warning settings string.

So you'll notice that we've disabled informational, enabled performance, and enabled severe. So this is the DBMS Warning package that allows us to do that. Also, another way-- select value from v$ parameter where name equal PL/SQL Warnings. This is going to allow us to see what our warnings are set to as well. So it depends on what permissions you have, depending on how you go in and see what your warning values are set to.

Now, we can also make some of our warnings errors by using the alter session command and setting the PL/SQL warnings equal to enabling severe, disabling performance. And warning 5,003, we're going to treat it as an error. In case we get that, that'll show up as an error when we compile.

With the DBMS Warning package, we can also not only retrieve the values, but we can also set the values through the package instead of using the Alter sessions commands. So we can set the warning setting string. In this case, we're enabling all warnings for this session, or we can add warning setting category, disable performance for this session-- either one of those used in the DBMS Warning package. And if I do this one, for instance, and then execute the DBMS Warning GetWarning setting string, you see that we have disabled informational, disabled performance, which is what we just did there, and enabled severe.

Now, in the book, we're going to show you that we have this scenario where somebody wants to create a procedure to compile their code, and what we want to do in this is we want to get the current warning settings. We want to disable performance warnings. We want to print those out. We want to compile what we're compiling. Then we want to set the warning string back to whatever it was and then print it out.

So I'm going to go ahead and create this procedure, and then what I will do is I will execute the compile code against my demopkg package, and it should compile it. And you notice that it shows what the current warning settings were, and then we modified them, and then we restored them. Looks like it just so happens that the current warning settings were the same as the modified warning settings, so let me go in and enable all of them for the session. And then we will recompile, and we should see some differences here.

There we are-- current warning settings, we enabled all. Modified warning settings, we enabled informational, disabled performance, enabled severe, and then we restarted those back to enabling all of those. And we used the DBMS warning package in order to do that. So that's what we're talking about here, the PL/SQL compile time warnings. We can either use the PL/SQL Warning Initialization parameter, or we can use the DBMS Warning package as we showed you.

So what are warnings? Warnings are messages from the compiler that help in improving code maintainability. Developers can use them to reduce the chances of bugs creeping into the application. A PL/SQL unit flagged with warnings may execute successfully, but might exhibit unexpected behavior or inefficient performance. All of your PL/SQL warning messages use the prefix PLW.

So the benefits of your compiler warnings-- it's going to make programs more robust and avoid problems at runtime, identify potential performance problems, and identify factors that produce undefined results. So here are the three categories-- severe, performance, and informational. Severe is where a condition might cause unexpected action or wrong results. Performance is where the condition might cause performance problems. Informational is where the condition does not affect performance or correctness, but you might want to change it for better maintainability.

So we're going to show you again how to do that by using either the PL/SQL warnings initialization parameter or the DBMS Warning package. So as I was showing you earlier, alter session set PL/SQL warnings, enabling severe, enabling performance, disabling informational; or enabling severe; or enabling severe, disabling performance, and setting code 5,003 to an error. And here, they're showing you that you can do that also in SQL Developer, as I showed you.

So here is where you can view the current setting of the SQL warnings. As long as you have the SELECT privilege on the V$ parameter view, then you can go in and take a look at your PL/SQL warnings. Now, you can view compiler warnings through SQL Plus with the Show Errors command-- you've seen me do that throughout the course-- and also through the data dictionary views. So here, we're creating a procedure called badproc. We have a Show Errors command, and you notice that it comes back and says, hey, we encountered the symbol dollar sign when inspecting one of the following.

The PL/SQL warning parameters are stored along with each compiled subprogram. This is why we might want to recompile the subprogram using the reuse settings clause, so that the original settings stored with the program will be used. Again, reminder, whenever you compile an object that was already created and compiled, you want to be considerate of what settings were used-- whether we're using native compilation, what optimization level, and so on and so forth.

We can also use the DBMS Warning package subprograms. This package is used to manipulate the behavior of the warning messages and to change the definition of the PL/SQL warnings parameter and to query, modify, and delete current system recession settings. So in order to set warnings, we have two procedures. In order to query warnings, we have three functions. In order to replace warnings, we have a procedure, and in order to get the category, whether the category is severe, informational, or performance, the Get Category subprogram can tell you that.

So we're showing you the signature for these different procedures, and we're showing you some examples using the DBMS Warnings SetWarning setting string or using the DBMS Warning AddWarning setting category or AddWarning setting cat. Then we have the functions-- GetWarningSettingCat, GetWarningSettingNum, GetWarningSettingString, and GetCategory. So if you don't know what category Warning 5,000 or 6,000 or 7,000 is, you can plug that in. For instance, here, we are getting the category of warning code 7,203. We see that is performance.

Anything in the 5,000 range is severe. Anything in the 6,000 range is informational. Anything in the 7,000 range is going to be performance. But if you forget those, we've got the subprogram that lets you get that warning setting category.

And then here is that compiled code procedure that I showed you, where we are using the DBMS Warning package in order to get the current warning setting string and change it, where we're disabling performance for the session. Printing out what those modified values are, compiling our subprogram, setting it back to the original value, and then printing that out so that we can see what the restored warnings are. So this was the demo that I ran for use, so you saw how that worked.

So that brings us to the quiz. The categories of PL/SQL compile time warning messages are severe, performance, informational-- those three. All, technically, I guess, would be a category because we can enable all three with All. And then critical is not one of the categories.

So in this lesson, you should have learned how to use the PL/SQL compiler initialization parameters, and you should have learned how to use the PL/SQL compile time warnings. We are now going to have you practice this in lesson 21. You're going to display the compiler initialization parameters. You're going to enable native compilation for your session and compile a procedure.

You're going to disable the compiler warnings and then restore the original session warning settings. And then you're going to identify the categories for some compiler warning message numbers. So let's have you go ahead and do the practices for Lesson 21, and this will conclude the demonstrations for lesson 21.

## Practice 21-1: Using the PL/SQL Compiler Parameters and Warnings - New - 16m

I will now demonstrate practices for Lesson 21-- Tuning the PL/SQL Compiler. In the practices for Lesson 21 overview, we see that in this practice, you displayed the compiler initialization parameters. You then enable native compilation for your session and compile a procedure.

You then suppress all compiler warning categories and then restore the original session warning settings. Finally, you identify the categories for some compiler warning message numbers. Before starting the practice, you're asked to go ahead and run the cleanup21.SQL file.

Now, I'm going to start with the solution. And the solution reiterates what we just talked about where we display the compiler initialization parameters. And you enable native compilation for your session and compile a procedure. And you suppress the compiler warning categories and then restore the original session warning settings. Finally, you identify the categories for some compiler warning message numbers.

OK, now notice that we have some messages there about if you have dropped the emp package or the add department procedure in the cleanup scripts. Go ahead and uncomment the below and execute the following code of ad department. And so just to see if I have the correct structures, I'll go ahead and run both of those. And let me open up my connection here. And I'll go ahead and create my sequence.

OK, so it looks like I already have that object. And let's take a look at the add department procedure. OK, it looks like we have that procedure now. And let me go ahead and erase my worksheet. Now, in step number one, it says to display the following information about compiler initialization parameters by using the user PL/SQL object settings data dictionary view.

Note the settings for the add department object. So we're going to click the Execute Statement icon to display the results in the Results tab. We're going to want the object name, the object type, the objects compilation mode, and the compilation optimization level. So let's go ahead and run this, and we'll take a look at the information for the add department subprogram.

In my case, it looks like it is set to native. OK. In the book, it looks like it was expected to be interpreted. So probably when I did my demos earlier, it was changed when I did my demos to native. So let me just go in and alter my session. And I'll set the PL/SQL code type equal to interpreted. And let me run that. And then I'll go ahead and recompile my add department procedure.

OK, and then let's go back and take a look at that again. OK, so now we see that my add department procedure is interpreted and set to optimization level of two, which is what the book is showing that it should be. OK, next, we're going to alter the PL/SQL code type parameter to enable native compilation for your session and compile the add department.

So what I'll do is I'll change my session to allow native compilation. And our session has been altered. And next, we will compile the add department procedure. And we have completed that task. And so we will rerun our SELECT statement on lines one through four. And we will just look to ensure that the add department procedure is set to native compilation.

All right. Step letter D, they tell us to switch compilation to use interpretive compilation. So let's go ahead and change this back to interpreted. And I'll run that. And then on the next page, page eight, they're telling us to use the Tools preferences in SQL developer in order to disable the compiler warnings categories.

So I'll go ahead and do that. I'll go up to Tools. I'll go to Preferences. And I'll go to Database to PL/SQL compiler. And what I'll do is I will disable all of my warnings. OK. And in fact, let's go ahead and disable every category as shown in the book. And then I'll click OK.

Next, in step number four, we're going to edit, examine, and execute the Lab 21 for SQL script to create the unreachable code procedure. So let me go ahead and open up that lab file. Lab 2104.SQL from the Home Oracle Labs PLP Labs Directory. And we will go ahead and run this in the My Connection Connection in order to create the procedure.

And let's go into the procedures category and refresh it so that we can see our unreachable code procedure. And next, what we'll do is we will answer question number five. What are the compiler warnings that are displayed in the compiler log tab? OK.

You notice that we did not get any warnings that came up. OK. So that is what they're telling us here. Note that the message on the message's log tab is compiled without any warning messages because we disabled the compiler warnings in step three.

OK, onto the next page. Next, we're asked to go ahead and enable all compiler warning messages in this session back in the preferences panel. So let's go ahead and go to Tools, Preferences. And we'll change all of these to Enable. And we'll click OK.

Next, we're asked to recompile the unreachable code procedure. And we're asked what compiler warnings are displayed. Let's go ahead and recompile. OK. Now, in this case, I think what I'll do is I'm going to just go ahead and click on unreachable code. And I'm going to compile it from this window here.

And you notice that I am getting some warning messages showing up in the compiler log. Next, on the next page, page 11, you'll notice that we're getting the same warnings that they are designating here. And it says, if you get the following two warnings in SQL developer, it is expected in some versions of SQL developer.

If you do get the following warnings, it is because your version of SQL developer will use the Oracle 11 database deprecated PL/SQL debug parameter. OK. Now, notice that we do not get that deprecated message. OK. However, we do get other warnings about the Off ID clause and the warning on PLW6002, which says unreachable code.

OK, step number eight, we're asked to use the User Errors Data Dictionary View to display the compiler time messages or the compiler warning messages that are detailed as follows. So I'm going to open up a new worksheet. And we're going to describe user errors. And we're going to see all of the columns that make up the User Errors Dictionary View.

Now, continuing on with step eight, we're going to do a select star from user errors. And this would be continuing on page 12. And we'll go ahead and run that. And you notice that we have in my case several different user errors. Now, these are not necessarily errors. Because of my text column, I can tell that these are not errors at all, but, rather, these are warnings.

OK, now in the note in the book, it says the output was displayed on the Results tab because we use the F9 key to execute this select statement. The results of the select statement might be different depending on the amount of errors that you had in your session. So you notice that mine is a little bit different than what the book is showing.

OK, step number nine, we're going to create a script named Warning Messages that uses the execute DBMS output and the DBMS Warning Package to identify the categories for the following compiler message numbers-- 50/50, 6075, and 7100. And we're asked to go ahead and enable the server output before running the script.

So let's go ahead and execute as they're describing. OK, so I'll go ahead and run line five. We're using the DBMS Warning Package. We're using the Get Category function. And we're going to be prompted using the substitution variable in order to put in the different warning codes that they're describing here in the book.

So let's go ahead and run line five. And I'll put in 50/50. And you notice that that is a severe warning category. OK. Next, we'll go ahead and run that again. And this time we'll use 6075. And we notice that that is an informational category. And we'll go ahead and execute it a third time. And we will use 7100.

And you notice that that is performance category. So that is what the book is showing us that we have severe informational and performance. OK, so that is going to do it for the demonstrations for Practice 21.
