# social-media-comments-microservice
## comment microservice 

creating a new model
assigning model with the value parsed from fiber context

if comment does not contain any text then we are throwing an errors telling that the text inside model is empty

if the post id of the comment is empty / nil then we will say that post id is required

now we are going to create a new service named as comment service

this new comment service function takes db interface as a parameter

comment-repo is an attribute of commentservice which is assigned the result of the function after calling the function new data repository mongo


now a new-comment is created and the following properties are defined

owner user id is assigned by the value of current user id
so, we can say that the owner of that comment is the user with that owner-user-id

post id got the value of post-id of model

score is initialised to 0
(assuming that the score of a comment will determine how relevent the comment is)

owner-display-name contains the display-name of the owner 

owner-avatar is the avatar of the owner who has commented

(assuming this will be required while displaying the comment)

deleted is initialized to false
(assuming it will denote whether comment is deleted or not)

deleted date is assigned to 0

created date is assigned to the current time 

LastUpdated is assigned to 0

now as the new-comment is created the new-comment gets saved by calling saveComment function. 



userInfoReq is assigned with the value that is returned by the function getUserInfoReq passing c as a parameter.

getUserInfoReq decode current user using c and create userInfoReq which is returned.

userInfoReq takes the details such as user-id, username, avatar, displayname, system-role from the current user and stores all of them inside it.

now readPostAsync function is called passing post-id and user-info-req as parameters. Then the result is stored inside readPostChannel.

userHeader has been created which is a map where ket is of string data-type and value is an array of string and the following properties are assigned.
corresponding to "uid" key userId of currentUser is stored in form of string 
corresponding to "email" username of currentUser is assigned as a string.

corresponding to "avatar" avatar of current-user is assigned

corresponding to "displayname" display-name of current-user is assigned. 

corresponding to the "role" system-role of current-user is assigned.

Now let's see how to increase comment counter on post :

a goroutine is started

post-comment-url is assigned with the url string "posts/comment/count"

payload is extracted by using marshalling the fiber map and the postId of the payload gets the value of post-id of model.

Now it's time to see if there is any post-comment-error.

To check that a function named function call is called with the following parameters :

- http.MethodPut   -> method
- payload          -> bytes-req
- post-comment-url -> url
- use-headers      -> header

the url then gets prettified 
the payload is decoded by calling new-buffer.

A new http request is created by calling the function http.NewRequest with the following parameters

- method
- AppConfig.InternalGateway and pretty-url
- body-reader

digest is created with the help of payload-secret and it is added to the header

All the kay value pair from the header is added inside http-req

A new http client is created with name c.

now http call is made and the result is stored inside a variable res.

now the result data is extracted from the result body.

if data is empty or if there is any error while extracting the data or the status code is neither accepted or statusOK then we throw an error with a proper error message.

### create notification request

a go routine is created with the current user as parameter.
post is an empty post model notification

unmarshalling of result of post result takes place and the value is assigned to empty post

now we check if the owner of the post is same as the owner of the comment by comparing their user-id and if they are same then we return from that point.

a new notification-model is created with the following attributes :
owner-user-id is assigned with the value of currentUser.userId

owner-display-name is assigned with the value of current-user-display-name.

owner-avatar is assigned with the value of current-user-avatar
title is display-name of current-user

description is assigned as a string "commented on your post"

url is same as url

notifyReceiverUserId is the user-id of the owner that means that owner is the receiver and he / she will receive the notification.

target-id is the post-id of the model.

is-seen is initialized to false (assuming is-seen determine whether the owner of the post has seen the comment or not).

now this new notification model is marshalled and stored in notification-bytes.

notificaion-url is assigned as the string "/notifications"

the function `functionCall` is called with the following parameters :

- http.MehodPost
- notification-bytes
- notification-url
- user-headers

## delete comment handle

comment-id is decoded by using params.

if comment-id is empty that means no comment-id has been assigned so we will throw an error saying that comment-id is required

now post-id is decoded in the same way.

now we are going to create a new service called comment-service by calling the function new-coomment-service

now current-user is extracted by using c.Locals

now we call a function called delete-comment-by owner 

this function delte-comment-by-owner has two parameters :

owner-user-id and comment-id and both are of type uuid.

with the comment-id and owner-user-id filter is created and this filter is passed to a function DeleteComment




