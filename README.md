# Reflected xss vulnerability 

-A very common example of XSS occurs when an application employs a dynamic page to display error messages to users.The page takes a parameter containing the message’s text and simply show this text back to the user within its response.

-This type of trick is conveninent for hackers, it allows them to customized error page from anywhere in the application without needing to hard-code individual messages within the error page itself.

-FOR EXAMPLE--> http://example.com/error/5/Error.ashx?message=Error+occurred { this example which returns the error message in the page } 

-HTML source for the returned page, we can see that the it simply copies the value of the message parameter in the URL and inserts it into the error page template at the appropriate place. [ <p> Error occurred </p> ]

-This behavior of taking user supplied input and insert it into server's response is one of the sign of Reflected xss .

-Now craft a URL which which replace a Error message with a piece of javascript that generate pop-up 
http://example.com/error/5/Error.ashx?message=<script>alert(1)</script> { this payload <script>alert(1)</script> will cause a pop up message when the page rendered with the user's browers }

-we clearly see that the contents of the message parameter can be replaced with arbitrary data that gets returned to the browser.


# Exploiting the Vulnerability

-XSS vulnerabilities can be exploited in many different ways to attack other users of an application. The simplest way is to Hijacking the user’s session gives the attacker access to all the data and functionality to which the user is authorized.
 
User's session hijack in 7 steps:
1> User login to application 
2> Attacker feed crafted URL to user 
3> user requests attacker's URL 
4> server responds with attacker's javascript 
5> Attacker’s JavaScript executes in user’s browser
6> User's browser sends session token to attacker 
7> Attacker Hijacks User's session 
