## Dev Connector Application

In the project directory, you can run:

### `Node Explanation`

#### An explanation of a Rest call on the backend

This is the main js file for the Node server backend.

    // routes
    const users = require("./routes/api/users");
    const profile = require("./routes/api/profile");
    const posts = require("./routes/api/posts");

This goes to the routes folder, and in there we have a users, profile, and posts js file. Each of these have http requests, which means when you hit the endpoints, they invoke the logic within each request. Let's take post.js as an example.

First off, we are using MongoDB, so we have created models, which will be explained below in another section.

    // @route  GET api/posts/
    // @desc   Get posts
    // @access Public
    router.get("/", (req, res) => {
    Post.find()
        .sort({ date: -1 })
        .then(posts => {
        res.json(posts);
        })
        .catch(err =>
        res.status(404).json({ nopostsfound: "No posts found with that ID" })
        );
    });

In this get request, we assign the url '/', which is prepended in the server.js file. As the second argument, it takes a callback function for the request and response. Post.find() asks MongoDB using the mongoose library to find all Post objects. Then we sort them in descending order with .sort({ date: -1 }). Since this is Promise-based, on success of this call, the .then(....) section takes the result of finding all objects in the database, and we simply send the object back in the response. If there were no posts found, then it goes to the .catch(...) section and sends a 404 status back.

This is essentially how all of them work. We find something from the database using similar syntax, for each object(s) we find, some logic is performed and we send something back to the server in a response.

Runs the app in the development mode.<br />
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.<br />
You will also see any lint errors in the console.
