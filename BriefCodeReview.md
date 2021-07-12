Developers Responsibility:

-	A solution/ project should compile well without error or warning. 
-	A program or a snippet is not complete, without developer-tested and unit tests cases.	
-	A complete documentation also crucial for a solution. 
-	A snippet is tidy (indentation, line length, no commented-out code, no spelling mistakes, etc).
-	We have to consider proper use of exceptions handling using Middleware.
-	We have to impose appropriate use of logging	
-	Make sure unused imports/usings are removed
-	The code should follow Coding Standards c#9/latest	
-	Are there any leftover stubs or test routines in the code?	
-	Are there any hardcoded, development only things still in the code?	
-	Solution should be platform independent
-	Security scan with any standard tool is must. E.g. veracode
-	Does the code release resources? (web connections, DataBase connection,static files)	
-	Corner cases well documented or any workaround for a known limitation of the frameworks
-	Can any code be replaced by calls to external reusable components or library functions?	
-	Design pattern need to take care of possible deadlocks. Use of CQRS
