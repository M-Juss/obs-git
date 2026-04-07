THEIR ARE 2 COMMON WAYS TO AUTHORIZE A USER:
1. TOKEN-BASED
2. SESSION / COOKIE-BASED
Difference of this 2 is that TOKEN usually stores in localStorage that can be read by java script and visible to users when checking dev tools. While SESSION ussually stores in cookie, it lets the browser store it and automatically reads it in every request without being seen however it can still be prone to scripting

# Moral Lesson
BOTH HAVE THE SAME PROBLEM.
THERES NO NEED FOR CHAINS AND ADDTIONAL LOCK IN THE FRONT DOOR TO PREVENT THE THEFT WHEN HE IS ACTUALLY INSIDE THE ROOM.
SOLUTION?
MAKE SURE U VALIDATED ALL FORMS
MAKE SURE EVERY INPUT IS VALIDATE AND SANITIZED TO PREVENT XSS!