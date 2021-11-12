# `Adding secure space`  API Test Guide using Postman

### Prerequisites

1. `Migrate` the database.

2. Using a specific API to get the IP address of the browser, such as `https://api.ipify.org?format=json`:

   ![](https://drive.google.com/uc?id=1zOuJQjdZSxXGu5QsHHtYJne3fP-GLo5k)

3. Using a specific API to get lists of all countries, states and cities on Earth, such as:

   ![](https://drive.google.com/uc?id=1cKcGN04rH2fFX8QrzIHXfY_fOCg_LtCl)

   

4. Don't forget to log in the application using route `/api/auth/login_check` to get the JWT token.

5. In the front-end, user must select `country` in the list first, then `state`, then `city`. It means:

   + User can not select `state` if she don't select `country`
   + User can not select `city` if she don't select `state`

### Creating secured location

Creating a secured location looks like below:

![creating](https://drive.google.com/uc?id=1wjwslDgeuaRjGgUmmNBrmjXJFPe-CH1f)

**_Some contraints_**:

- If any of input parameters `(city, state, country)` existed in the database, a validation failed message will be thrown.

- If a `city` of a `state` is already existed in the database, and a user wants to add the whole `state` without a specific `city`, a validation failed message will be thrown. At that time, user must remove the existed `city` (using route `/api/secure-space/{id}/delete`, keep reading this guide to see how to delete a secured location).

- And there are some more contraints to make sure user does not mess up the database.

### Editing a secured location

Editing a secured location using route `http://localhost:1437/api/secure-space/{id}/edit` looks like below (`id` = the id of `UserSecureLocation` entity):

![editing](https://drive.google.com/uc?id=1lL3kty6-zUPv9XYVJGYlct_Ljs44AX_9)

  **_Some constraints_**:

+ This operation also has some contraints like the Creating operation above.

### Deleting a secured location

Deleting a secured location using route `http://localhost:1437/api/secure-space/{id}/delete` looks like below (`id` = the id of `UserSecureLocation` entity):

![deleting](https://drive.google.com/uc?id=1RxhRmte0JbajgDN-5auI51B4SqeIRUsr)

### Checking the logged user is whether or not on the secured location. If not, log her out immediately.

**Step 1:** Log the user in.

**Step 2**: Sending  a `GET` request to route  `http://localhost:1437/api/check-user-location` to check if the logged user is under a secured location. If not, the user will be logged out immediately.

---

--END--
