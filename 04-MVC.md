# MVC

- [MVC](#mvc)
  - [MVC - Models, Views and Controllers](#mvc---models-views-and-controllers)
  - [Models](#models)
  - [Views](#views)
  - [Controllers](#controllers)
  - [Conventional expectations](#conventional-expectations)

---

## MVC - Models, Views and Controllers

- Separation of presentation layber (what the user of the application sees in the browser/mobile device) and the business-logic and backend (invisible layer)

## Models

- User
- Post
- Article
- Stock
- ...

Typically these involve some sorts of persistence like table / DB

<br/>

## Views

Frontend of the app - html / css / ...

- home
- new
- friends
- my_profolio
- ...

- `xx.html.erb`

<br/>

## Controllers

Brain behind your app.

- users_controller
- posts_controller
- articles_controller
- stocks_controller

<br/>

## Conventional expectations

- Define a route that points to a `controller#action`
- Have an appropriately named controller, for example:
  - if dealing with layouts or static pages of the application, a name could be `pages_controller`
- Have an appropriately named action. For example:
  - if dealing with a homepage, the action/method could be named `home`
- If done this way, under views, rails will expect 
  - a `pages` folder (named for the pages controller);
  - a `home.html.erb` template (named for the home action)