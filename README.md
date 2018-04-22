# SporkPin

https://sporkpin.herokuapp.com/

Credits located in about page.

Name was changed from FriendsEat to SporkPin because FriendsEat was taken.

Link to project video : https://youtu.be/36hp20LKq-k

  
### Team Members
  - Kevin Raghubir
  - Tirth Shah
  - Junil Patel


### A description of web application
  - We&#39;re constantly looking for good places to eat, but quick searches on google gives you restaurants with reviews that might not be relatable or interesting to your needs. So instead of just reading random reviews, how can a user have reviews that are trusted, reliable and relatable? We want to help provide a platform for people to find trustworthy reviews that are specifically provided by their friends. This will allow people to discover new restaurants and also help speed the progress of finding constructive reviews. Now you won&#39;t have to look through Yelp, Google and other platforms before making a decision. FriendsEat will give you with a one stop shop of all the trustworthy reviews you need to go out and enjoy your night out. Not only will it give reviews, but it will also provide with a list of items the friends ordered, ratings and pictures of food from that restaurant. This will provide the user reliable reviews from people they already know, instead of strangers.


### A description of the key features that will be completed by the Beta version
  - User management
    - Full implementation of sign up/in/out
  - Google maps
    - Ability to find certain restaurants based upon some criteria based on the current location
  - Reviews and  ratings
    - Ability to post and see reviews and ratings made by your friends on the chosen restaurant
    - Ability to endorse other friend&#39;s comments


### A description of additional features that will be complete by the Final version
  - Twitter tweets
    - Use the twitter api to pull tweets related to certain restaurants to see what others are saying about it.
  - Instagram Pictures
    - Use the instagram api to pull images based on the tagged location of the images


### A description of the technology that you will use
  - Geolocation
    - Used to find location of users upon sign in
  - Google maps api
    - Used to easily visualize locations
    - Find nearby restaurants that friends have went to
  - Front End
    - Bootstrap
      - Used to make the site clear and simple on all devices
    - React Framework
  - Backend
    - Express Node.js
    - MongoDB
      - Used to manage all data needed by the project


### A description of the top 5 technical challenges
  - Integrate Twitter live feed based on a search query
  - Integrate Instagram photos based on a location tag on instagram
  - Integrate Google Maps (Easily view location of restaurants on the map and provide directions)
  - Learning and implementing React to manage the DOM and Bootstrap to support multiple devices
  - Adding multi language support



# SporkPin REST API Documentation

## SporkPin API

### Create

- description: POST method to sign in a user
- request: `POST /signin/`
    - content-type: `application/json`
    - body: object
      - username: (string) name of user
      - password: (string) the user's password
- response: 200
    - content-type: `application/json`
    - body: object
      - "user " + username + " signed in"
- response: 500
    - body: username does not exists
- response: 401
    - body: access denied
```
$ curl -X POST
       -H "Content-Type: `application/json`"
       -d '{"username":"junil","password":"patel"}'
       -c cookie.txt
       https://sporkpin.herokuapp.com/signin/

```

- description: POST method to sign up a new user
- request: `POST /signup/`
    - content-type: `application/json`
    - body: object
      - username: (string) name of user
      - password: (string) the user's password
      - email: (string) the user's email
      - city: (string) the user's city
      - bio: (string) the user's bio
      - picture: (file) the user's profile picture
- response: 200
    - content-type: `application/json`
    - body: object
      - "user " + username + " signed up"
- response: 500
    - body: username does not exists
- response: 409
    - body: "username " + username + " already exists"
```
$ curl -X POST
       -H "Content-Type: `application/json`"
       -d '{"username":"junil","password":"patel","email":"junp@gmail.com","city":"Toronto","bio":"I like food","picture":picture}'
       -c cookie.txt
       https://sporkpin.herokuapp.com/signup/
```

- description: POST a new review
- request: `POST /api/reviews/`
    - content-type: `application/json`
    - body: object
      - content: (string) the content of the review
      - restaurant_id: (string) the restaurant id
- response: 200
    - content-type: `application/json`
    - body: object
      - _id: (string) the review id
      - content: (string) the content of the review
      - author: (string) the authors username
      - lastlike: (string) the author of the last like
      - likes: (int) number of likes
```
$ curl -X POST
       -b cookie.txt
       -H "Content-Type: `application/json`"
       -d '{"content":"Nice food!","restaurant_id":"xXBAVK0s1234"}
       https://sporkpin.herokuapp.com/api/reviews/'
```

### Read

- description: Sign out
- request: `GET /signout/`
- response: 200
    - page redirect(/)
```
$ curl -b cookie.txt
       -c cookie.txt
       https://sporkpin.herokuapp.com/signout/
```

- description: retrieve all reviews of a restaurant, given restaurant_id
- request: `GET /api/reviews/restaurant/:restaurant_id/`
- response: 404
    - body: "Restaurant id:" + restaurant_id + " does not exist!"
- response: 200
    - content-type: `application/json`
    - body: list of objects
      - _id: (string) the review id
      - content: (string) the content of the review
      - author: (string) the authors username
      - lastlike: (string) the author of the last like
      - likes: (int) number of likes
```
$ curl -b cookie.txt
       https://sporkpin.herokuapp.com/api/reviews/restaurant/xXBAVK0s1234/
```

- description: retrieve all friend reviews of a restaurant, given restaurant_id
- request: `GET /api/reviews/friends/restaurant/:restaurant_id/`   
- response: 404
    - body: "Restaurant id:" + restaurant_id + " does not exist!"
- response: 200
    - content-type: `application/json`
    - body: list of objects
      - _id: (string) the review id
      - content: (string) the content of the review
      - author: (string) the authors username
      - lastlike: (string) the author of the last like
      - likes: (int) number of likes
```
$ curl -b cookie.txt
       https://sporkpin.herokuapp.com/api/reviews/friends/restaurant/xXBAVK0s1234/
```

- description: retrieve all reviews of a user, given username
- request: `GET /api/reviews/users/:username/`
- response: 404
    - body: "Username:" + username + " does not exist!"   
- response: 200
    - content-type: `application/json`
    - body: list of objects
      - _id: (string) the review id
      - content: (string) the content of the review
      - author: (string) the authors username
      - lastlike: (string) the author of the last like
      - likes: (int) number of likes
```
$ curl -b cookie.txt
       https://sporkpin.herokuapp.com/api/reviews/users/junil/
```

- description: retrieve user info
- request: `GET /api/users/:username/` 
- response: 409
    - body: "Username:" + username + " does not exist!"  
- response: 200
    - content-type: `application/json`
    - body: object
      - _id: (string) the username
      - email: (string) the user's email
      - city: (string) the user's city
      - bio: (string) the user's bio
      - picture: (file) the user's profile picture
      - friends (list of strings) list of friends names
```
$ curl -b cookie.txt
       https://sporkpin.herokuapp.com/api/users/junil/
```

- description: retrieve friends list
- request: `GET /api/users/friends/:username/` 
- response: 409
    - body: "Username:" + username + " does not exist!"  
- response: 200
    - content-type: `application/json`
    - body: (list of strings) list of friend names
```
$ curl -b cookie.txt
       https://sporkpin.herokuapp.com/api/users/friends/junil/
```

- description: retrieve requests list
- request: `GET /api/users/requests/:username/`
- response: 409
    - body: "Username:" + username + " does not exist!"   
- response: 200
    - content-type: `application/json`
    - body: (list of strings) list of usernames
```
$ curl -b cookie.txt
       https://sporkpin.herokuapp.com/api/users/requests/junil/
```

### Update

- description: like a review
- request: `Patch /api/reviews/like/:reviewId/`
- response: 404
    - body: "Review id: " + reviewId + " does not exist"
- response: 200
    -body: username + " and " + (review.like) + " others have liked this!"
```
$ curl -b cookie.txt 
       -H "Content-Type: application/json" 
       -X PATCH
       https://sporkpin.herokuapp.com/api/reviews/like/1234/
```

- description: add a friend
- request: `Patch /api/users/addFriend/:username/`
- response: 404
    - body: "Username:" + username + " does not exist!" 
- response: 409
    - body: "Request to:" + username + " has already been sent" 
- response: 200
    -body: Sent Patch
```
$ curl -b cookie.txt 
       -H "Content-Type: application/json" 
       -X PATCH
       https://sporkpin.herokuapp.com/api/users/addFriend/junil/
```

- description: accept a request
- request: `Patch /api/users/acceptFriend/:username/`
- response: 200
    -body: Sent Patch
```
$ curl -b cookie.txt 
       -H "Content-Type: application/json" 
       -X PATCH
       https://sporkpin.herokuapp.com/api/users/acceptFriend/junil/
```

- description: reject a request
- request: `Patch /api/users/rejectFriend/:username/`
- response: 200
    -body: Sent Patch
```
$ curl -b cookie.txt 
       -H "Content-Type: application/json" 
       -X PATCH
       https://sporkpin.herokuapp.com/api/users/rejectFriend/junil/
```

- description: remove a friend
- request: `Patch /api/users/removeFriend/:username/`
- response: 200
    -body: Sent Patch
```
$ curl -b cookie.txt 
       -H "Content-Type: application/json" 
       -X PATCH
       https://sporkpin.herokuapp.com/api/users/removeFriend/junil/
```

### Delete

- description: delete a comment given the comment id
- request: `DELETE /api/reviews/:id/`
- response: 200
    - content-type: `application/json`
    - body: object
      - _id: (string) the review id
      - content: (string) the content of the review
      - author: (string) the authors username
      - lastlike: (string) the author of the last like
      - likes: (int) number of likes
- response: 403
    - body: forbidden
- response: 404
    - body: "Review id: " + reviewId + " does not exist"
```
$ curl -X DELETE
       -b cookie.txt
       https://sporkpin.herokuapp.com/api/reviews/1234/
```
