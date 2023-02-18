# Putting it All Together: Client-Server Communication

## Learning Goals

- Understand how to communicate between client and server using fetch, and how
  the server will process the request based on the URL, HTTP verb, and request
  body
- Debug common problems that occur as part of the request-response cycle

## Introduction

Just like the last lesson, we've got code for a React frontend and Rails API
backend set up. This time though, it's up to you to use your debugging skills to
find and fix the errors!

To get the backend set up, run:

```console
$ bundle install
$ rails db:migrate db:seed
$ rails s
```

Then, in a new terminal, run the frontend:

```console
$ npm install --prefix client
$ npm start --prefix client
```

Confirm both applications are up and running by visiting
[`localhost:4000`](http://localhost:4000) and viewing the list of toys in your
React application.

## Deliverables

In this application, we have the following features:

- Display a list of all the toys
- Add a new toy when the toy form is submitted
- Update the number of likes for a toy
- Donate a toy to Goodwill (and delete it from our database)

The code is in place for all these features on our frontend, but there are some
problems with our API! We're able to display all the toys, but the other three
features are broken.

Use your debugging tools to find and fix these issues.

There are no tests for this lesson, so you'll need to do your debugging in the
browser and using the Rails server logs and `byebug`.

**Note**: You shouldn't need to modify any of the React code to get the
application working. You should only need to change the code for the Rails API.

As you work on debugging these issues, use the space in this README file to take
notes about your debugging process. Being a strong debugger is all about
developing a process, and it's helpful to document your steps as part of
developing your own process.

## Your Notes Here

- Add a new toy when the toy form is submitted

  - How I debugged:
      - I clicked first the Create New Toy button to see what error it will return.
      - It returned an error message that looks like this:

        ```POST http://localhost:4000/toys 500 (Internal Server Error)```
      - From the error message, it will tell you that the error is in the server, so i checked the rail server log to look for the last request came through and it will show you that error is in the controller action 'create'.
      - By checking the create action, there's a typo in Toys.create. It has to be Toy.create.

- Update the number of likes for a toy

  - How I debugged:
      - I clicked the Like button to see what error it will return.
      - It did return an error message that looks like this:

        ``` SyntaxError: Unexpected end of JSON input at ToyCard.js:21:1 ``` 
      - Knowing that the error is json input, i checked the update action in the controller if it's rendering json and then update the code.

- Donate a toy to Goodwill (and delete it from our database)

  - How I debugged:
    - I click delete or donate button to see what error it will return.
    - It returned an error message that looks like this:

        ```DELETE http://localhost:4000/toys/9 404 (Not Found)```

    - I then checked the server log and saw an error message that looks like this:

        ```ActionController::RoutingError (No route matches [DELETE] "/toys/9"):```

    - It shows that it doesn't have a delete route so i just added a :destroy route in routes.rb.
