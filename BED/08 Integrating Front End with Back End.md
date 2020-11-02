
08 Integrating Front End with Back End
===



## Table of Contents
- [08 Integrating Front End with Back End](#08-integrating-front-end-with-back-end)
  * [Table of Contents](#table-of-contents)
    + [Front End](#front-end)
    + [CORS](#cors)
  * [Practical Example](#practical-example)
    + [Initialise](#initialise)
    + [Homepage](#homepage)
    + [Fetching Posts](#fetching-posts)
    + [Implementing CORS in Controller](#implementing-cors-in-controller)
    + [Building Profile Page](#building-profile-page)
      - [HTML file](#html-file)
      - [JS Code](#js-code)
    + [Login Page](#login-page)
      - [HTML](#html)
      - [JS Code](#js-code-1)
    + [Redirect if not logged in](#redirect-if-not-logged-in)
      - [JS Code](#js-code-2)


### Front End
- how it'll work
    - user goes to valid url
    - client server send template html w/o data from db
    - js code bundled with html execute on user's browser
    - browser requests for data from our restapi with axios
    - once rest api responds with data, jquery used to append data to html
- jwt token will either be stored on localStorage or as a cookie

### CORS
- for security reasons browsers restrict cross-origin http reqs made by scripts
    - since front end server services file from localhost:3031 and API server is on localhost:3000, we are making cross-origin reqs
    - get around by adding `Access-Control-Allow-Origin` header in api resp with value `*` (hence allowing all)
    - install cors express middleware too
        - `npm install --save cors`
- [read more](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)


Practical Example
---
### Initialise
```javascript=
// index.js in root dir
app.get("/", (req, res) => {
  res.sendFile("/public/index.html", { root: __dirname });
});

app.get("/users/:id", (req, res) => {
  res.sendFile("/public/user.html", { root: __dirname });
});

app.get("/users/", (req, res) => {
  res.sendFile("/public/users.html", { root: __dirname });
});


const PORT = 3001;
app.listen(PORT, () => {
  console.log(`Client server has started listening on port ${PORT}`);
});
```

### Homepage
```htmlmixed=
// index.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Friendbook</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
</head>
<body>
    <body>
    <div class="container">
        <nav class="nav">
            <a class="nav-link" href="/">Home</a>
            <a class="nav-link" href="/users/">All Users</a>
        </nav>
    
        <div style="margin-top: 2rem;">
            <h1>Home</h1>

            <form id="create-post-form" style="margin-top: 2rem;">
                <div class="form-group">
                    <textarea class="form-control" id="create-post-form-body" rows="3" placeholder="What's on your mind?"></textarea>
                </div>
                <button type="submit" class="btn btn-primary">Create Post</button>
            </form>

            <div id="posts">
            
            </div>
        </div>
    </div>

    <script
        src="https://code.jquery.com/jquery-3.3.1.min.js"
        integrity="sha256-FgpCb/KJQlLNfOu91ta32o/NMZxltwRo8QtmkMRdAu8="
        crossorigin="anonymous"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js" integrity="sha384-UO2eT0CpHqdSJQ6hJty5KVphtPhzWj9WO1clHTMGa3JDZwrnQq4sF86dIHNDz0W1" crossorigin="anonymous"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js" integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM" crossorigin="anonymous"></script>
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <script>
        // your JS code goes here.
        
    </script>
</body>
</html>
```

![](https://i.imgur.com/1tQXtjk.png)


### Fetching Posts
```javascript=
// append this js code into the script tag in html code above
// FETCHING POSTS
// API url
const baseUrl = "http://localhost:3000";
// hardcoded because we have not added login yet.
const loggedInUserID = 1;

axios.get(`${baseUrl}/users/${loggedInUserID}/posts/`)
.then((response) => {
    const posts = response.data;
    posts.forEach((post) => {
        const postHtml = `
        <div class="card" style="margin-top: 2rem;">
            <div class="card-body">
                <p class="card-text">${post.text_body}</p>
            </div>
            <div class="card-footer text-muted">
                ${post.created_at}
            </div>
        </div>
        `;

        $("#posts").append(postHtml);
    });
})
.catch((error) => {
    console.log(error);
});
```

### Implementing CORS in Controller
```javascript=
const express = require("express");
const app = express();

const User = require("./models/User");
const Post = require("./models/Post");

const bodyParser = require("body-parser");
app.use(bodyParser.json());

const cors = require("cors");
app.use(cors());
...
```

- now has required header
![](https://i.imgur.com/HWmuOCW.png)


### Building Profile Page
#### HTML file
```htmlembedded=
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Friendbook</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
</head>
<body>
    <div class="container">
        <nav class="nav">
            <a class="nav-link" href="/">Home</a>
            <a class="nav-link" href="/users/">All Users</a>
        </nav>

        <div class="row" style="margin-top: 2rem;">
            <div class="col-md-8 col-xs-12">
                <div id="user-profile">
                </div>

                <div id="posts">
                </div>
            </div>

            <div class="col-md-4 col-xs-12">
                <h2>Friends</h2>
                <ul id="friends-list" class="item-group" style="list-style: none; padding-left: 0;">
                </ul>
            </div>
        </div>
    </div>
    <script
        src="https://code.jquery.com/jquery-3.3.1.min.js"
        integrity="sha256-FgpCb/KJQlLNfOu91ta32o/NMZxltwRo8QtmkMRdAu8="
        crossorigin="anonymous"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js" integrity="sha384-UO2eT0CpHqdSJQ6hJty5KVphtPhzWj9WO1clHTMGa3JDZwrnQq4sF86dIHNDz0W1" crossorigin="anonymous"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js" integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM" crossorigin="anonymous"></script>
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <script>
        // JSCODE goes here
    
    </script>
</body>
</html>
```
#### JS Code
```javascript=
// js code
const baseUrl = "http://localhost:3000";
const loggedInUserID = 1;

const url = window.location.toString();
const userID = parseInt(url.split("/").slice(-1)[0]);
let posts;

axios.get(`${baseUrl}/users/${userID}`)
    .then((response) => {
        // append user profile
        const user = response.data;
        $("#user-profile").append(`
        <h1>${user.full_name}</h1>
        <p style="margin-top: 1rem;">${user.bio}</p>
        `);
    });

// fetch and append user posts
axios.get(`${baseUrl}/users/${userID}/posts/`)
    .then((response) => {
            posts = response.data;
            posts.forEach((post, index) => {
                const likeHtml = `
                <button class="btn btn-primary like-button" data-index=${index}>Like</button>
                `;

                const unlikeHtml = `
                <button class="btn btn-danger unlike-button" data-index=${index}>Unlike</button>
                `;

                const hasLiked = post.likers.map(liker => liker.id).includes(loggedInUserID);

                const postHtml = `
                <div class="card" style="margin-top: 2rem;">
                    <div class="card-body">
                        <p class="card-text">${post.text_body}</p>
                        ${ hasLiked ? unlikeHtml : likeHtml }
                        <h5 style="margin-top: 1rem;">Likers</h5>
                        <ul class="list-group">
                            ${
                                post.likers
                                    .map(liker => `
                                    <li class="list-group-item">
                                        <a href="/users/${liker.id}">${liker.full_name}</a>
                                    </li>
                                    `)
                                    .join("")
                            }
                        </ul>
                    </div>
                    <div class="card-footer text-muted">
                        ${post.created_at}
                    </div>
                </div>
                `;

                $("#posts").append(postHtml);
            });
        });

// fetch user's friends
axios.get(`${baseUrl}/users/${userID}/friends/`)
    .then((response) => {
        const friends = response.data;
        friends.forEach((friend) => {
            $("#friends-list").append(`
            <li class="list-group-item">
                <a href="/users/${friend.id}">${friend.full_name}<a/>
            </li>
            `);
        });
    });

// listens for like button clicks
// we have to use the .on method instead of $(".like-button").click because this
// supports listening to dynamically added like/unlike buttons.
// IMPORTANT: DO NOT USE arrow functions because then `this` will not refer to the button!
$(document).on("click", ".like-button", function() {
    const index = parseInt($(this).attr("data-index"));
    const post = posts[index];
    axios.post(`${baseUrl}/posts/${post.id}/likers/${loggedInUserID}`)
        .then((res) => {
            // change button to unlike on success
            const unlikeHtml = `
            <button class="btn btn-danger unlike-button" data-index=${index}>Unlike</button>
            `;
            $(this).replaceWith(unlikeHtml);
        });
});

// listens for unlike button clicks
$(document).on("click", ".unlike-button", function() {
    const index = parseInt($(this).attr("data-index"));
    const post = posts[index];

    axios.delete(`${baseUrl}/posts/${post.id}/likers/${loggedInUserID}`)
        .then((res) => {
            // change button to like on success
            const likeHtml = `
            <button class="btn btn-primary like-button" data-index=${index}>Like</button>
            `;
            $(this).replaceWith(likeHtml);
        });
});

```

### Login Page
#### HTML
```htmlembedded=
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Friendbook</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
</head>
<body>
    <div class="container">
        <nav class="nav">
            <a class="nav-link" href="/">Home</a>
            <a class="nav-link" href="/users/">All Users</a>
        </nav>

        <h1>Login</h1>
        <p>Don't have an account?</p>
        <a href="/register/" class="btn btn-primary">Register</a>
        <form id="login-form">
            <div class="form-group">
                <label for="username">Username</label>
                <input type="text" class="form-control" id="username">
            </div>
            <div class="form-group">
                <label for="password">Password</label>
                <input type="password" class="form-control" id="password">
            </div>
            <button type="submit" class="btn btn-primary">Login</button>
        </form>
    </div>
    <script
    src="https://code.jquery.com/jquery-3.3.1.min.js"
    integrity="sha256-FgpCb/KJQlLNfOu91ta32o/NMZxltwRo8QtmkMRdAu8="
    crossorigin="anonymous"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js" integrity="sha384-UO2eT0CpHqdSJQ6hJty5KVphtPhzWj9WO1clHTMGa3JDZwrnQq4sF86dIHNDz0W1" crossorigin="anonymous"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js" integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM" crossorigin="anonymous"></script>
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <script>
    // js code goes here
    </script>
</body>
</html>
```

#### JS Code
```javascript=
const baseUrl = "http://localhost:3000";
$("#login-form").submit((event) => {
    // prevent page reload
    event.preventDefault();

    const username = $("#username").val();
    const password = $("#password").val();
    const requestBody = {
        username: username,
        password: password
    };

    axios.post(`${baseUrl}/login/`, requestBody)
        .then((response) => {
            const token = response.data.token;
            const loggedInUserID = response.data.user_id;
            localStorage.setItem("token", token);
            localStorage.setItem("loggedInUserID", loggedInUserID);
            window.location.href = "/";
        })
        .catch((error) => {
            console.log(error);
        });
});
```

### Redirect if not logged in
- redirect if no token in localStorage

#### JS Code
```javascript=
// edit in script tag of index and user.html
const baseUrl = "http://localhost:3000";
const token = localStorage.getItem("token");
const loggedInUserID = parseInt(localStorage.getItem("loggedInUserID"));

if (token === null || isNaN(loggedInUserID)) {
    window.location.href = "/login/";
} else {
    // put your original code in the script tag here
}
```




###### tags: `BED` `DISM` `School` `Notes`