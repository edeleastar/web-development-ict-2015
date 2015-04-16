##Assignment Exercises

These exercises can be considered valid "stories" for your assignment 2 submission

###Assignment Story 1 

Lab 9 introduced a 'data.yml' file in th conf directory. This contained initial user data loaded at startup:

~~~
User(homer):
    firstName: Homer
    lastName: Simpson
    email: homer@simpson.com
    password: secret

User(marge):
    firstName: marge
    lastName: Simpson
    email: marge@simpson.com
    password: secret
~~~

Extend this data to include the full homer clan (and friends). Note, the number of spaces (4) before each field is significant.

###Assignment Story 2 

Extend the User Model to include the following new fields:

- Age
- Nationality

These fields must be filled in when a user registers.

###Assignment Story 3 

For the new fields accepted in Story 2, display them on the users Home Profile page.

In addition, on the users 'Public' profile (then one a friend can see), display just the 'Nationality' field


###Assignment Story 4

Even if a user seems to have logged out, we can still access the spacebook pages by entering the url of some of the controllers. For instance, log in, then log our immediately and try these links:

- <http://localhost:9000/home>
- <http://localhost:9000/homeprofile>

How could you prevent this?

HINT: The session object has a method called 'clear()'. If we call this (say in logout action), then it will remove any things we have put in there. For every action, we could first check to make sure a valid ID is in the session, otherwise redirect to the start page.


###Assignment Story 5 

Provide a way for a user, once logged in, to change some of their profile information. You could take two approaches to this:

- Provide some extra fields on the home profile which could all be changed when the 'changeText' button is pressed.
- Provide a link on the home profile - say 'edit details' - which takes you to a new page where you can edit the details.

###Assignment Story 6

The Members page now shows a list of all members - including the currently logged in member. This clearly makes no sense and we should try to remove the current member from the list.

HINT: This is the Members controller index method:

~~~java
  public static void index()
  {
    List<User> users = User.findAll();
    render(users);
  }
~~~
 
The challenge is to remove the current user from the users list before we send it to the view. Objects can be deleted from a list using the remove method:

~~~
   user.remove(currentUser);
~~~

How would you get a User object representing the current user? From the session of course - something like this perhaps:

~~~
    String userId = session.get("logged_in_userid");
    User currentUser = User.findById(Long.parseLong(userId));
~~~
