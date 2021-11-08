# Demo

This is the tutorial from Gwendolyn Faraday.  

## Auto-logout API Test Guide using Postman
#### First of first: run `php bin/console doctrine:migrations:migrate` to migrate the database
**_Step 1:_**
+ **Login**: sending `GET` request to [/api/auth/login_check](http://localhost:1437/api/auth/login_check) to get the login token.

**_Step 2:_**
+ **Set the auto logout parameters**:
    + add params `(interval, timezone)` to the route `/api/user-expire-setting`. For example:
| Interval | Timezone |
| -------- | -------- |
| 30 second | Asia/Ho_Chi_Minh |
| 2 hour | Europe/Kiev |
| 5 day | America/New_York |  
    + Attach the login token you got in step 1 and send `POST` a request to [/api/user-expire-setting](http://localhost:1437/api/user-expire-setting). You'll get a success message in the response.  
    + Notice: interval type is available in second, hour, day and must be singular. For example:  
| OK | NG |
| ---- | --- |
| 70 second | 70 seconds |
| 5 hour | 5 hours |
| 10 day | 10 days |

**_Step 3:_**  
+ Logout current user by sending a `DELETE` request to [/api/users/logout](http://localhost:1437/api/users/logout) (The log-in expiration feature will be valid for the next login)

**_Step 4:_**
+ Log user in again (follow step 1) to get the login token
+ Attaching the login token to route [/api/check-active](http://localhost:1437/api/check-active) and give it a heartbeat signal by sending a `POST` request every 5 seconds.
`Tips: You should set the interval to be less than a minute (60 second). So you don't need to wait so long to see the result`
+ After a few of `check-active` request, you should send some request to a specific route such as `/api/comments` or something else to check whether or not the user is remaining login status.
+ Keep sending `POST` request to `/api/check-active` every a few of second (5 second or 1 second, it's up to you).
When the current timestamp reaches the log-in expiration time that you set in step 2, you will get a message `Invalid JWT token`.
+ Try to send a `GET` request to route `/api/comments` again, you will get the message `Invalid JWT token`. It means the user's login session is expired.

That's all!
| sdfdf | sdfsdf |
| ----- | ------ |
| sdf | sdfdf |

sdfsdfsdf
