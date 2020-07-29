# Today I Learned by *[Raul Alejandro Almanza Serrano]*

Ruby and Rails official documentation reading personal journal

## Week 1

### Thu 23, July 2020 *[Welcome to Rails]*
Rails is a web framework that uses ruby as a programming language, this framework is based on MVC pattern to create dynamic web applications in an easy way.

Understanding the MVC pattern is key to understanding Rails. MVC divides your application into three layers: Model, View, and Controller, each with a specific responsibility.

Rails uses Active Record as a primary class to handle the communication between database and model, taking into account MVC pattern. Active Record represent each row into database as an object.

The Controller layer is responsible for handling incoming HTTP requests and providing a suitable response. Usually this means returning HTML, but Rails controllers can also generate XML, JSON, PDFs, mobile-specific views, and more. 

### Fry 24, July 2020 *[Ruby on Rails modules]*
RoR has some main modules/classes such as:
- **ActionCable:** integrates WebSockets with the rest of your Rails application. It allows for real-time features to be written in Ruby in the same style and form as the rest of your Rails application, while still being performant and scalable.
- **ActionMailer:** Allows you to send emails from your application using mailer classes and views.
- **ActiveJob:** Framework for declaring jobs and making them run on a variety of queuing backends. These jobs can be everything from regularly scheduled clean-ups, to billing charges, to mailings.
- **ActiveModel:** Library that containis various modules used in developing classes that need some features present on Active Record. Some of these modules are explained below.

### Mon 27, July 2020 *[Ruby on Rails modules part 2]*
- **ActionPack:** Action Pack is a framework for handling and responding to web requests. It provides mechanisms for routing, defining controllers that implement actions, and generating responses by rendering views. It consists on some modules such as:
  - ActionDispatch: parses information about the web request, handles routing as defined by the user, and does advanced processing related to HTTP such as MIME-type negotiation, decoding parameters in POST, PATCH, or PUT bodies, handling HTTP caching logic, cookies and sessions.
  - ActionController: provides a base controller class that can be subclassed to implement filters and actions to handle requests. The result of an action is typically content generated from views.

Dispatch functionality is activated by default and Action View rendering is implicitly triggered by Action Controller.
