---
layout: post
title:      " Invoices with React & Redux"
date:       2021-05-18 01:42:36 +0000
permalink:  invoices_with_react_and_redux
---

For my last project at Flatiron School, I built an application that can create and manage invoices.

Setting up the backend API was a quick process with Ruby on Rails. My models are all set up with ActiveRecord and include an Account, an Invoice and an Item. An Account has many invoices and an Invoice has many items. My application handles data persistence with PostgreSQL.
For this project, I used Active Model Serializer to render my application data in JSON. Active Model Serializer provdes a basic serializer implementation that allows you to easily control how a given object is going to be serialized, On initialization, it expects two objects as arguments, a resource and options. For example:
```
PostSerializer.new(@post, :scope => current_user).to_json
```
My routes and controllers are nested under `/api/v1` and I used `gem cors` to handle [Cross-Origin Resource Sharing (CORS)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS/Errors//), making cross-origin AJAX possible. When using this gem, make sure to uncomment the following in your application's `config/initializers.cors.rb` file:
```
Rails.application.config.middleware.insert_before 0, Rack::Cors do
  allow do
    origins '*'

    resource '*',
      headers: :any,
      methods: [:get, :post, :put, :patch, :delete, :options, :head]
  end
end
```

The front-end for this application is built using React. I used the `create-react-app` generator to start the project. My aplication uses a single HTML page to render my react-redux application, and follows a RESTful routing pattern making use of `react-router` to render different pages of the application.
[React Router](https://reactrouter.com/) is a collection of navigational components that compose declaratively with your application.

To respond to, and modify state change, I used the Redux middleware.
**Middleware** is software that bridges gaps between other applications, tools, and databases in order to provide unified services to users. It is commonly characterized as the glue that connects different software platforms and devices together.
**Redux** middleware provides a third-party extension point between dispatching an action, and the moment it reaches the reducer. It is used for logging, crash reporting, talking to an asynchronous API, routing, and more.

Sending data to, and receiving data from a server is handled using async actions and `redux-thunk` middleware.
**Redux Thunk** middleware allows you to write action creators that return  a function instead of an action. The thunk can be used to delay the dispatch of an action, or to dispatch only if a cetain condition is met. The inner function receives the store methods `dispatch` and `getState` as parameters. For example, an action creator that returns a function to perform asynchronous dispatch:
```
const INCREMENT_COUNTER = 'INCREMENT_COUNTER';
 
function increment() {
  return {
    type: INCREMENT_COUNTER
  };
}
 
function incrementAsync() {
  return dispatch => {
    setTimeout(() => {
      // Yay! Can invoke sync or async actions with `dispatch`
      dispatch(increment());
    }, 1000);
  };
}
```
All of the data manipulation for the application is handled by my backend API.

Another great learning process. 
