Active for Laravel
==================

[![Build Status](https://travis-ci.org/dwightwatson/active.png?branch=master)](https://travis-ci.org/dwightwatson/active)

Active is a helper package for Laravel that makes it easy to recoginse the current path or route, useful for adding 'active' classes (like those used in the Boostrap framework) and performing other actions only when a certain route is active. It also includes helpers for retrieving the current controller and action names.

## Installation

First, simply require the package through Composer.

```sh
composer require watson/active
```

Next, add the service provider in your `config/app.php` file.

`Watson\Active\ActiveServiceProvider::class`

If you'd like to use the Facade instead of the helper functions, add it to the `aliases` array.

`'Active' => Watson\Active\Facades\Active::class`

## Using Active

### Helper functions

Active ships with a couple of helper functions which make it easy to use without the facade or creating an instance of your own.

```php
active()

is_active()
```

### Using `active()`

You pass an array of routes or paths you want to see are the current page, and if any match this function will return the string `active`, for Bootstrap. Alternatively, you can pass a custom return string as the second argument.

```php
active(['login', 'users/*', 'posts.create'], 'active-class');
```

In this example, the function will return the string `active-class` if the current path is `login`, starts with `users/` or if the name of the current route is `posts.create`.

Do note that a number of argument types are provided: you can use a path string, you can use a path string with a wildcard (using the `*`) and you can also use named routes.

You can use this function with your links to give them an active state.

```php
<a href="{{ route('posts.index') }}" class="{{ active('posts.index') }}">All posts</a>
```

### Using `is_active()`

This works much the same as `active()`, you can pass the paths and routes to it but instead it will return a boolean if the current page matches. 

```php
@if (is_active('posts/*'))
    You're looking at a blog post!
@endif
```

### Additional helpers

Two additional functions are provided to get the current controller and action, if your routing is being handled by a controller for a request. These functions will return the lowercase controller/action name, without the method of the request. Here is an example for a request that is routed to `FooController@getBar':

    $controller = controller_name(); // foo

    $action = action_name(); // bar