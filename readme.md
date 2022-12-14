<p align="center">
  <img src="./assets/logo.png" alt="Cover Ignite Node">
</p>
<h2 align="center">Chapter II - Challenge</h2>
<h1 align="center">Users Management</h1>

<h1 align="center">
  <a href="./LICENSE.md">
  <img alt="License" src="https://img.shields.io/static/v1?label=license&message=MIT&color=91091e"/>
  </a>
</h1>
<br>

# âšī¸ Index

- [About the challenge](#đ-about-the-challenge)
  - [API Routes](##đ-API-Routes)
- [Tests Specification](#â´ī¸-tests-specification)
  - [Model Test](##đ-Model-Test)
  - [Repository Tests](##đ-Repository-Tests)
  - [UseCases Tests](##đ-UseCases-Tests)
  - [Routes Tests](##đ-Routes-Tests)
- [The extra mile](#âī¸-The-extra-mile)
- [Author](#-Author)
- [License](#đ-License)

<br>

# đ-About the challenge

In this Challenge we create an Users Management API.

The user needs to be an admin to make the list users works.

## đ-API Routes

### đ POST `/users`

The route must receive `name` and `email` inside the request body to be able to create an user.


### đ PATCH `/users/:user_id/admin`

The route must receive, in the request params, the user `id` and exchange this user to admin.

### đ GET `/users/:user_id`

The route must receive, in the request params, the user `id` and return the user's info found by the response body.

### đ GET `/users`

The route must receive, in the request header, a properties `user_id` with the user `id` and return a list with all users created.

The `id` must be used to validate if the user who is requesting the list is an admin. The list response only must be done if the user is an admin.

# â´ī¸-Tests Specification 

## đ-Model Test

### đ Should be able to create an user with all props

For this test, you must create a model with the properties below:
```json
{
  "id": "string",
  "name": "string",
  "admin": "boolean",
  "email": "string",
  "created_at": "Date",
  "updated_at": "Date",
}
```
The `admin` property should be started with `false` and the `id` should be automatically generated as `uuid`.

## đ-Repository Tests
### đ Should be able to create new users

For this test, the `create` method of UsersRepository file needs to receive the user's name and email to create an user from the model.

### đ Should be able to list all users

For this test, the `list` method of UsersRepository file return a list of all created users.

### đ Should be able to find user by ID

For this test, the `findById` method of UsersRepository file must receive the user `id` and return an user who has the same `id`.

### đ Should be able to find user by e-mail address

For this test, the `findByEmail` method of UsersRepository file must receive the user `email` and return the user who has the same `email`.

### đ Should be able to turn an user as admin

For this test, the `turnAdmin` method of UsersRepository must receive the whole user object, change the `admin` property to `true`, update the `updated_at` property and return the updated user.

## đ-UseCases Tests

### đ Should be able to create new users

For this test, the `execute` method of CreateUserUseCase file must receive the user `name` and `email` to be created, create an user through the repository's create method and return the created user.

### đ Should not be able to create new users when email is already taken

For this test, the `execute` method of CreateUserUseCase file must not allow an user to be created if exist an user with the same `email`.

If exist an user with the same email return the error message:
```tsx
throw new Error("Mensagem do erro");
```

### đ Should be able to turn an user as admin

For this test, the `execute` method of TurnUserAdminUseCase file must receive the user `id`, call the repository method wich change the user to `admin` and return the user after the change.

### đ Should not be able to turn a non existing user as admin

For this test, the `execute` method of TurnUserAdminUseCase file must not allow an `user` who does not exist to be changed in `admin`.

If the user does not exist return the error message:
```tsx
throw new Error("Mensagem do erro");
```
### đ Should be able to get user profile by ID

For this test, the `execute` method of ShowUserProfileUseCase file must receive the user `id`, call the repository's method wich search an user by `id` and return the user found.

### đ Should not be able to show profile of a non existing user

For this test, the `execute` method of ShowUserProfileUseCase file must not allow a non-existing user to be return.

If the user does not exist return the error message:
```tsx
throw new Error("Mensagem do erro");
```
### đ Should be able to list all users

For this test, the `execute` method of ListAllUsersUseCase file must recieve the user `id`, call the repository's method which return all created users and return this info.

### đ Should not be able to a non admin user get list of all users

For this test, the `execute` method of ListAllUsersUseCase must not allow an user who is not a `admin` access the created users.

If the user is not an `admin`, return a message error:
```tsx
throw new Error("Mensagem do erro");
```
### đ Should not be able to a non existing user get list of all users

For this test, the `execute` method of ListAllUsersUse Case file must not allow an user does not exist, access the created users list.

If the user does not exist, return a message error:
```tsx
throw new Error("Mensagem do erro");
```

## đ Routes Tests

## đ Route - [POST] /users
### đ Should be able to create new users

For this test, using the proper useCase, the route must create an `user` and return a status `201` with the created user object.

### đ Should not be able to create new users when email is already taken

For this test, if an error has occurred in useCase, return a response with status `400` and a json with an object `{ error: "error message" }`, where the value of the `error` property should be the message thrown by the error in useCase.

To catch errors thrown by other files, you can wrap the contents of the controller in a `try/catch`.

## đ Rota - [PATCH] /users/:user_id/admin
### đ Should be able to turn an user as admin

For this test, using the proper useCase, the route must change an user to `admin` and return the user changed int the response body.

### đ Should not be able to turn a non existing user as admin

For this test, if an error has occurred in useCase, return a response with status `404` and a json with an object `{ error: "error message" }`, where the value of the `error` property should be the message thrown by the error in useCase.

## đ Rota - [GET] /users/:user_id
### đ Should be able to get user profile by ID

For this test, using the proper useCase, the route must recieve the user `id` by route params and return the founded user object in the response body.

### đ Should not be able to show profile of a non existing user

For this test, if an error has occurred in useCase, return a response with status `404` and a json with an object `{ error: "error message" }`, where the value of the `error` property should be the message thrown by the error in useCase.

## đ Rota - [GET] /users
### đ Should be able to list all users

For this test, using the proper useCase, the route must recieve the `admin` user `id` from `user_id` request header and return a user list created.

### đ Should not be able to a non admin user get list of all users and Should not be able to a non existing user get list of all users

For these tests, if an error has occurred in useCase, return a response with status `400` and a json with an object `{ error: "error message" }`, where the value of the `error` property should be the message thrown by the error in useCase.

# âī¸ The extra mile

Implementation of extra features.

## đ Should not be able to create new users without an email or name

For this test, the `execute` method of CreateUserUseCase file must not allow an user to be created if the field `email` or `name` is empty.

If exist an user with the same email return the error message:
```tsx
throw new Error("Mensagem do erro");
```

<br>

# -Author
<img style="border-radius: 50%" src="https://avatars.githubusercontent.com/u/54655739?v=4/" width="100px;" alt="Picture"/>
<p><b>Maycon Queiroz, budding back-end developer.</b></p>
<a href="https://www.linkedin.com/in/maycon-queiroz-56572014a/">
  <img alt="Linkedin" src="https://img.shields.io/badge/-Linkedin -91091e?style=flat&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/maycon-queiroz-56572014a/" />
</a>&nbsp;
<a href="mailto:fmaycon@gmail.com">
  <img alt="Email" src="https://img.shields.io/badge/-Email-91091e?style=flat&logo=Gmail&logoColor=white&link=mailto:fmaycon@gmail.com" />
</a>&nbsp;
<br><br>

# đLicense
This project is under de MIT license. Look at the file [LICENSE](./LICENSE) for more information.
