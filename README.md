# Today I Learned by *Raul Alejandro Almanza Serrano*

Ruby and Rails official documentation reading personal journal

# Week 1

## Thu 23, July 2020 *[ Welcome to Rails ]*
Rails is a web framework that uses ruby as a programming language, this framework is based on MVC pattern to create dynamic web applications in an easy way.

Understanding the MVC pattern is key to understanding Rails. MVC divides your application into three layers: Model, View, and Controller, each with a specific responsibility.

Rails uses Active Record as a primary class to handle the communication between database and model, taking into account MVC pattern. Active Record represent each row into database as an object.

The Controller layer is responsible for handling incoming HTTP requests and providing a suitable response. Usually this means returning HTML, but Rails controllers can also generate XML, JSON, PDFs, mobile-specific views, and more. 

## Fri 24, July 2020 *[ Ruby on Rails modules ]*
RoR has some main modules/classes such as:
- **ActionCable:** integrates WebSockets with the rest of your Rails application. It allows for real-time features to be written in Ruby in the same style and form as the rest of your Rails application, while still being performant and scalable.
- **ActionMailer:** Allows you to send emails from your application using mailer classes and views.
- **ActiveJob:** Framework for declaring jobs and making them run on a variety of queuing backends. These jobs can be everything from regularly scheduled clean-ups, to billing charges, to mailings.
- **ActiveModel:** Library that containis various modules used in developing classes that need some features present on Active Record. Some of these modules are explained below.

# Week 2

## Mon 27, July 2020 *[ Ruby on Rails modules part 2 ]*
- **ActionPack:** Action Pack is a framework for handling and responding to web requests. It provides mechanisms for routing, defining controllers that implement actions, and generating responses by rendering views. It consists on some modules such as:
  - ActionDispatch: parses information about the web request, handles routing as defined by the user, and does advanced processing related to HTTP such as MIME-type negotiation, decoding parameters in POST, PATCH, or PUT bodies, handling HTTP caching logic, cookies and sessions.
  - ActionController: provides a base controller class that can be subclassed to implement filters and actions to handle requests. The result of an action is typically content generated from views.

Dispatch functionality is activated by default and Action View rendering is implicitly triggered by Action Controller.

## Tue 28, July 2020 *[ Ruby on Rails modules part 3 ]*
- **ActionText:** brings rich text content and editing to Rails. It includes the Trix editor that handles everything from formatting to links to quotes to lists to embedded images and galleries. The rich text content generated by the Trix editor is saved in its own RichText model that's associated with any existing Active Record model in the application. Any embedded images (or other attachments) are automatically stored using Active Storage and associated with the included RichText model.

- **ActionView:** Action View is a framework for handling view template lookup and rendering, and provides view helpers that assist when building HTML forms, Atom feeds and more. Template formats that Action View handles are ERB (embedded Ruby, typically used to inline short Ruby snippets inside HTML), and XML Builder.

## Wed 29, July 2020 *[ Ruby on Rails modules part 4 ]*
- **ActiveRecord:** connects classes to relational database tables to establish an almost zero-configuration persistence layer for applications. In the context of an application, these classes are commonly referred to as models. Models can also be connected to other models; this is done by defining associations.

  some of the major features:
    - Associations between objects defined by simple class methods.
    - Aggregations of value objects.
    -Validation rules that can differ for new or existing objects.
    - Callbacks available for the entire life cycle (instantiation, saving, destroying, validating, etc.).
    - Inheritance hierarchies.
    - Transactions.
    - Reflections on columns, associations, and aggregations.
    - Database abstraction through simple adapters.
    - Database agnostic schema management with Migrations.

## Thu 30, July 2020 *[ Ruby on Rails modules part 5 ]*
- **ActiveStorage:** Active Storage makes it simple to upload and reference files in cloud services like Amazon S3, Google Cloud Storage, or Microsoft Azure Storage, and attach those files to Active Records. Supports having one main service and mirrors in other services for redundancy. It also provides a disk service for testing or local deployments, but the focus is on cloud storage.

  Files can be uploaded from the server to the cloud or directly from the client to the cloud.

  Image files can furthermore be transformed using on-demand variants for quality, aspect ratio, size, or any other MiniMagick or Vips supported transformation.

# Week 3

## Mon 3, August 2020 *[ AbstractController ]*
- **ActionNotFound:** Raised when a non-existing controller action is triggered.
- **Base:** is a low-level API. Nobody should be using it directly, and subclasses (like ActionController::Base) are expected to provide their own render method, since rendering means different things depending on the context.
- **Calbacks:** Abstract Controller provides hooks during the life cycle of a controller action. Callbacks allow you to trigger logic during this cycle. Calling the same callback multiple times will overwrite previous callback definitions.
- **UrlFor:** Includes url_for into the host class (e.g. an abstract controller or mailer). The class has to provide a RouteSet by implementing the _routes methods. Otherwise, an exception will be raised.

  Note that this module is completely decoupled from HTTP - the only requirement is a valid _routes implementation.

## Tue 4, August 2020 *[ ActionCable part 1 ]*
- **Channel Base:** The channel provides the basic structure of grouping behavior into logical units when communicating over the WebSocket connection.
  
  Channel instances are long-lived. A channel object will be instantiated when the cable consumer becomes a subscriber, and then lives until the consumer disconnects. This may be seconds, minutes, hours, or even days.

  Unlike subclasses of ActionController::Base, channels do not follow a RESTful constraint form for their actions. Instead, Action Cable operates through a remote-procedure call model. You can declare any public method on the channel (optionally taking a data argument), and this method is automatically exposed as callable to the client.


## Wed 5, August 2020 *[ ActionCable part 2 ]*
- **Channel Naming:** Returns the name of the channel, underscored, without the Channel ending. If the channel is in a namespace, then the namespaces are represented by single colon separators in the channel name.
- **Channel PeriodicTimers:** Periodically performs a task on the channel, like updating an online user counter, polling a backend for new status messages, sending regular “heartbeat” messages, or doing some internal work and giving progress updates.
- **Channel Streams:** allow channels to route broadcastings to the subscriber. A broadcasting is, as discussed elsewhere, a pubsub queue where any data placed into it is automatically sent to the clients that are connected at that time. It's purely an online queue, though. If you're not streaming a broadcasting at the very moment it sends out an update, you will not get that update, even if you connect after it has been sent.

## Thu 6, August 2020 *[ ActionController part 1 ]*
- **Api:** API Controller is a lightweight version of ActionController::Base, created for applications that don't require all functionalities that a complete Rails controller provides, allowing you to create controllers with just the features that you need for API only applications.
  
  Normally, ApplicationController is the only controller that inherits from ActionController::API. All other controllers in turn inherit from ApplicationController.
  
  - **Renders:** The default API Controller stack includes all renderers, which means you can use render :json and brothers freely in your controllers. Keep in mind that templates are not going to be rendered, so you need to ensure your controller is calling either render or redirect_to in all actions, otherwise it will return 204 No Content.
  - **Redirects:** Redirects are used to move from one action to another. You can use the redirect_to method in your controllers in the same way as in ActionController::Base.
  - **Adding New Behavior:** In some scenarios you may want to add back some functionality provided by ActionController::Base that is not present by default in ActionController::API, for instance MimeResponds. This module gives you the respond_to method. Adding it is quite simple, you just need to include the module in a specific controller or in ApplicationController in case you want it available in your entire application.

## Fri 7, August 2020 *[ ActionController part 2 ]*
- **Base:** Action Controllers are the core of a web request in Rails. They are made up of one or more actions that are executed on request and then either it renders a template or redirects to another action. An action is defined as a public method on the controller, which will automatically be made accessible to the web-server through Rails Routes.

  Actions, by default, render a template in the app/views directory corresponding to the name of the controller and action after executing code in the action.

  - **Requests:** For every request, the router determines the value of the controller and action keys. These determine which controller and action are called. The remaining request parameters, the session (if one is available), and the full request with all the HTTP headers are made available to the action through accessor methods. Then the action is performed.
  - **Parameters:** All request parameters, whether they come from a query string in the URL or form data submitted through a POST request are available through the params method which returns a hash.
  - **Sessions:** Sessions allow you to store objects in between requests. This is useful for objects that are not yet ready to be persisted, such as a Signup object constructed in a multi-paged process, or objects that don't change much and are needed all the time, such as a User object for a system that requires login. The session should not be used, however, as a cache for objects where it's likely they could be changed unknowingly.
  - **Responses:** Each action results in a response, which holds the headers and document to be sent to the user's browser. The actual response object is generated automatically through the use of renders and redirects and requires no user intervention.
  - **Renders:** Action Controller sends content to the user by using one of five rendering methods. The most versatile and common is the rendering of a template. Included in the Action Pack is the Action View, which enables rendering of ERB templates. It's automatically configured. 
  - **Redirects:** Redirects are used to move from one action to another. For example, after a create action, which stores a blog entry to the database, we might like to show the user the new entry.
  - **multiple redirects:** An action may contain only a single render or a single redirect. Attempting to try to do either again will result in a DoubleRenderError.

# Week 4

## Tue 11, August 2020 *[ ActionController part 3 ]*
- **Caching:** Caching is a cheap way of speeding up slow applications by keeping the result of calculations, renderings, and database calls around for subsequent requests.
- **DataStreaming:** Methods for sending arbitrary data and for streaming files to the browser, instead of rendering.
- **DefaultHeaders:** Allows configuring default headers that will be automatically merged into each response.
- **EtagWithFlash:** When you're using the flash, it's generally used as a conditional on the view. This means the content of the view depends on the flash. Which in turn means that the ETag for a response should be computed with the content of the flash in mind. This does that by including the content of the flash as a component in the ETag that's generated for a response.

## Wed 12, August 2020 *[ ActionController part 4 ]*
- **EtagWithTemplateDigest:** When our views change, they should bubble up into HTTP cache freshness and bust browser caches. So the template digest for the current action is automatically included in the ETag.
- **FormBuilder:** Override the default form builder for all views rendered by this controller and any of its descendants. Accepts a subclass of ActionView::Helpers::FormBuilder.
- **Helpers:** The Rails framework provides a large number of helpers for working with assets, dates, forms, numbers and model objects, to name a few. These helpers are available to all templates by default.

  In addition to using the standard template helpers provided, creating custom helpers to extract complicated logic or reusable functionality is strongly encouraged. By default, each controller will include all helpers. These helpers are only accessible on the controller through #helpers

## Thu 13, August 2020 *[ ActionController part 5 ]*
- **HttpAuthentication::Digest:**  The authenticate_or_request_with_http_digest block must return the user's password or the ha1 digest hash so the framework can appropriately hash to check the user's credentials. Returning nil will cause authentication to fail.

  Storing the ha1 hash: MD5(username:realm:password), is better than storing a plain password. If the password file or database is compromised, the attacker would be able to use the ha1 hash to authenticate as the user at this realm, but would not have the user's password to try using at other sites.
- **ImplicitRender:** Handles implicit rendering for a controller action that does not explicitly respond with render, respond_to, redirect, or head.
  For API controllers, the implicit response is always 204 No Content.

  For all other controllers, we use these heuristics to decide whether to render a template, raise an error for a missing template, or respond with 204 No Content:

  First, if we DO find a template, it's rendered. Template lookup accounts for the action name, locales, format, variant, template handlers, and more (see render for details).
