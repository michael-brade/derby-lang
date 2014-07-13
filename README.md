Derby Lang
==========

A translation library for [Derby JS](http://derbyjs.com).
It uses [messageformat.js](https://github.com/SlexAxton/messageformat.js) rather than gettext.
Refer to messageformat.js for the advantages of using messageformat and how to format translation strings.

Installation
------------

    $ npm install derby-lang --save

Server Usage
------------

In your server file, add the middleware:

    var lang = require('derby-lang').server;

    expressApp
      // ...
      // ...
      .use(lang())

Add a dictionary:

    // ..
    // ..
    .use(function (req, res, next) {
      var model = req.getModel();
      model.set('$lang.dict', {
        en: {'Hello world.': 'Hello world.'},
        es: {'Hello world.': 'Hola mundo.'}
      });
      next();
    });

Optionally, use [derby-lang-fs](https://github.com/psirenny/derby-lang-fs)
to define a dictionary with `*.json` files.

App Usage
---------

In your view functions:

    var lang = require('derby-lang').app;
    app.proto.t = lang.translate();

In your view:

    <p>{{t($lang.dict, 'en', ['Hello World.'])}}</p>

Locale
------

It's up to you to manage what locale to display.
You can use [derby-locale](https://github.com/psirenny/derby-locale)
to automatically select the best locale for a user given the ones you support, their browser preference, etc.

Dictionary
----------

A dictionary is just an object with translation strings.
It may be stored in the database rather than set during a middleware route.
You could subscribe to a dictionary and use ShareJS views to return only the languages the user will see.
