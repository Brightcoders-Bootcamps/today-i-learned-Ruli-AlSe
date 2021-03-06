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

## Fri 14, August 2020 *[ ActionController part 6 ]*
- **Instrumentation:** Adds instrumentation to several ends in ActionController::Base. It also provides some hooks related with process_action. This allows an ORM like Active Record and/or DataMapper to plug in ActionController and show related information.
- **Live:** There are a few caveats with this module. You cannot write headers after the response has been committed (Response#committed? will return truthy). Calling write or close on the response stream will cause the response object to be committed. Make sure all headers are set before calling write or close on your stream.
  - **SSE:** This class provides the ability to write an SSE (Server Sent Event) to an IO stream. The class is initialized with a stream and can be used to either write a JSON string or an object which can be converted to JSON.

# Week 5

## Mon 17, August 2020 *[ ActionController part 6 ]*
- **MimeResponds:** The public controller methods respond_to may be called with a block that is used to define responses to different mime-types. In this usage, the argument passed to the block (format above) is an instance of the ActionController::MimeResponds::Collector class. This object serves as a container in which available responses can be stored by calling any of the dynamically generated, mime-type-specific methods such as html, xml etc on the Collector. Each response is represented by a corresponding block if present.
- **Parameters:** Allows you to choose which attributes should be permitted for mass updating and thus prevent accidentally exposing that which shouldn't be exposed. Provides two methods for this purpose: require and permit. The former is used to mark parameters as required. 

## Tue 18, August 2020 *[ ActionController part 7 ]*
- **ParamsWrapper:** Wraps the parameters hash into a nested hash. This will allow clients to submit requests without having to specify any root elements. This functionality is enabled in config/initializers/wrap_parameters.rb and can be customized.
  On Active Record models with no :include or :exclude option set, it will only wrap the parameters returned by the class method attribute_names.
- **Rescue:** This module is responsible for providing rescue_from helpers to controllers and configuring when detailed exceptions must be shown.

## Wed 19, August 2020 *[ ActionController part 8 ]*
- **Streaming:** By default, Rails renders views by first rendering the template and then the layout. The response is sent to the client after the whole template is rendered, all queries are made, and the layout is processed.
  Streaming inverts the rendering flow by rendering the layout first and streaming each part of the layout as they are processed. This allows the header of the HTML (which is usually in the layout) to be streamed back to client very quickly, allowing JavaScripts and stylesheets to be loaded earlier than usual.
  Streaming may be considered to be overkill for lightweight actions like new or edit. The real benefit of streaming is on expensive actions that, for example, do a lot of queries on the database.
  In such actions, you want to delay queries execution as much as you can.

- **Strong Parameters:** It provides an interface for protecting attributes from end-user assignment. This makes Action Controller parameters forbidden to be used in Active Model mass assignment until they have been explicitly enumerated.

## Thu 20, August 2020 *[ ActionDispatch part 1 ]*
- **AssertionResponse:** This is a class that abstracts away an asserted response. It purposely does not inherit from Response because it doesn't need it. That means it does not have headers or a body.
- **Assertions:** Has two important modules...
  - **ResponseAssertions:** A small suite of assertions that test responses from Rails applications.
  - **RoutingAssertions:** Suite of assertions to test routes generated by Rails and the handling of requests made to them.
- **Callbacks:** Provides callbacks to be executed before and after dispatching the request.

## Fri 21, August 2020 *[ ActionDispatch part 2 ]*
- **Cookies:** Cookies are read and written through ActionController#cookies.
  The cookies being read are the ones received along with the request, the cookies being written will be sent out with the response. Reading a cookie does not get the cookie object itself back, just the value it holds.
- **DebugExceptions:** This middleware is responsible for logging exceptions and showing a debugging page in case the request is local.
- **DebugLocks:** This middleware can be used to diagnose deadlocks in the autoload interlock.
- **FileHandler:** This middleware returns a file's contents from disk in the body response. When initialized, it can accept optional HTTP headers, which will be set when a response containing a file's contents is delivered. This middleware will render the file specified in env["PATH_INFO"] where the base path is in the root directory. 

# Week 6

## Mon 24, August 2020 *[ ActionDispatch part 3 ]*
- **Flash:** The flash provides a way to pass temporary primitive-types (String, Array, Hash) between actions. Anything you place in the flash will be exposed to the very next action and then cleared out. This is a great way of doing notices and alerts, such as a create action that sets flash[:notice] = "Post successfully created" before redirecting to a display action that can then expose the flash to its template. Actually, that exposure is automatically done.

- **HostAuthorization:** This middleware guards from DNS rebinding attacks by explicitly permitting the hosts a request can be sent to.
  When a request comes to an unauthorized host, the response_app application will be executed and rendered. If no response_app is given, a default one will run, which responds with +403 Forbidden+.

## Tue 25, August 2020 *[ ActionDispatch part 4 ]*
- **Http:** This module works with this other submodules...
  - **FilterParameters:** Allows you to specify sensitive parameters which will be replaced from the request log by looking in the query string of the request and all sub-hashes of the params hash to filter. Filtering only certain sub-keys from a hash is possible by using the dot notation: 'credit_card.number'. If a block is given, each key and value of the params hash and all sub-hashes are passed to it, where the value or the key can be replaced using String#replace or similar methods.
  - **Headers:** Provides access to the request's HTTP headers from the environment. Note that when headers are mapped to CGI-like variables by the Rack server, both dashes and underscores are converted to underscores. This ambiguity cannot be resolved at this stage anymore. Both underscores and dashes have to be interpreted as if they were originally sent as dashes.
  - **UploadedFile:** Models uploaded files. The actual file is accessible via the tempfile accessor, though some of its interface is available directly for convenience. Uploaded files are temporary files whose lifespan is one request. When the object is finalized Ruby unlinks the file, so there is no need to clean them with a separate maintenance task.

## Wed 26, August 2020 *[ ActionDispatch part 5 ]*
- **PublicExceptions:** When called, this middleware renders an error page. By default if an HTML response is expected it will render static error pages from the /public directory. For example when this middleware receives a 500 response it will render the template found in /public/500.html. If an internationalized locale is set, this middleware will attempt to render the template in /public/500.<locale>.html. If an internationalized template is not found it will fall back on /public/500.html.
- **Reloader:** ActionDispatch::Reloader wraps the request with callbacks provided by ActiveSupport::Reloader callbacks, intended to assist with code reloading during development. By default, ActionDispatch::Reloader is included in the middleware stack only in the development environment; specifically, when config.cache_classes is false.

## Thu 27, August 2020 *[ ActionDispatch part 6 ]*
- **RemoteIp:** This middleware calculates the IP address of the remote client that is making the request. It does this by checking various headers that could contain the address, and then picking the last-set address that is not on the list of trusted IPs.
- **RequestId:** Makes a unique request id available to the action_dispatch.request_id env variable (which is then accessible through ActionDispatch::Request#request_id or the alias ActionDispatch::Request#uuid) and sends the same id to the client via the X-Request-Id header.
- **Response:** Represents an HTTP response generated by a controller action. Use it to retrieve the current state of the response, or customize the response. It can either represent a real HTTP response (i.e. one that is meant to be sent back to the web browser) or a TestResponse. 
  Response is mostly a Ruby on Rails framework implementation detail, and should never be used directly in controllers. Controllers should use the methods defined in ActionController::Base instead. Nevertheless, integration tests may want to inspect controller responses in more detail, and that's when Response can be useful for application developers. 

# Week 7

## Tue September 1, 2020 *[ ActionDispatch part 7 ]*
- **Routing:** The routing module provides URL rewriting in native Ruby. It's a way to redirect incoming requests to controllers and actions. This replaces mod_rewrite rules. Best of all, Rails' Routing works with any web server. Routes are defined in config/routes.rb.
  - **PolymorphicRoutes:** Polymorphic URL helpers are methods for smart resolution to a named route call when given an Active Record model instance. They are to be used in combination with ActionController::Resources.

    These methods are useful when you want to generate the correct URL or path to a RESTful resource without having to know the exact type of the record in question.
- **SSL:** This middleware is added to the stack when config.force_ssl = true, and is passed the options set in config.ssl_options. It does three jobs to enforce secure HTTP requests:
  - **TLS redirect:** Permanently redirects http:// requests to https:// with the same URL host, path, etc. Enabled by default. Set config.ssl_options to modify the destination URL.
  - **Secure cookies:** Sets the secure flag on cookies to tell browsers they must not be sent along with http:// requests. Enabled by default.
  - **HTTP Strict Transport Security (HSTS):** Tells the browser to remember this site as TLS-only and automatically redirect non-TLS requests.

## Wed September 2, 2020 *[ ActionDispatch part 8 ]*
- **Session:** Has following modules...
  - **CacheStore:** A session store that uses an ActiveSupport::Cache::Store to store the sessions. This store is most useful if you don't store critical data in your sessions and you don't need them to live for extended periods of time.
  - **CookieStore:** This cookie-based session store is the Rails default. It is dramatically faster than the alternatives.
  Sessions typically contain at most a user_id and flash message; both fit within the 4K cookie size limit. A CookieOverflow exception is raised if you attempt to store more than 4K of data.
  - **MemCacheStore:** A session store that uses MemCache to implement storage.
- **ShowExceptions:** This middleware rescues any exception returned by the application and calls an exceptions app that will wrap it in a format for the end user.
  The exceptions app should be passed as parameter on initialization of ShowExceptions. Every time there is an exception, ShowExceptions will store the exception in env, rewrite the PATH_INFO to the exception status code and call the Rack app.

## Thu September 3, 2020 *[ ActionDispatch part 9 ]*
- **Static:** This middleware will attempt to return the contents of a file's body from disk in the response. If a file is not found on disk, the request will be delegated to the application stack. This middleware is commonly initialized to serve assets from a server's public/ directory.
- **TestResponse:** Integration test methods such as ActionDispatch::Integration::Session#get and ActionDispatch::Integration::Session#post return objects of class TestResponse, which represent the HTTP response results of the requested controller actions.

## Fri September 4, 2020 *[ ActionMailbox part 1 ]*
- **Base:** The base class for all application mailboxes. Not intended to be inherited from directly. Inherit from ApplicationMailbox instead, as that's where the app-specific routing is configured. Application mailboxes need to overwrite the #process method, which is invoked by the framework after callbacks have been run. The callbacks available are: before_processing, after_processing, and around_processing. The primary use case is ensure certain preconditions to processing are fulfilled using before_processing callbacks.

# Week 8

## Mon September 8, 2020 *[ ActionMailbox part 2 ]*
- **InboundEmail:** The InboundEmail is an Active Record that keeps a reference to the raw email stored in Active Storage and tracks the status of processing. By default, incoming emails will go through the following lifecycle:
  - **Pending:** Just received by one of the ingress controllers and scheduled for routing.
  - **Processing:** During active processing, while a specific mailbox is running its process method.
  - **Delivered:** Successfully processed by the specific mailbox.
  - **Failed:** An exception was raised during the specific mailbox's execution of the #process method.
  - **Bounced:** Rejected processing by the specific mailbox and bounced to sender.

  Once the InboundEmail has reached the status of being either delivered, failed, or bounced, it'll count as having been #processed?. Once processed, the InboundEmail will be scheduled for automatic incineration at a later point.

## Tue September 9, 2020 *[ ActionMailbox part 3 ]*
- **IncinerationJob:** You can configure when this IncinerationJob will be run as a time-after-processing using the config.action_mailbox.incinerate_after or ActionMailbox.incinerate_after setting.

  Since this incineration is set for the future, it'll automatically ignore any InboundEmails that have already been deleted and discard itself if so.
- **Router:** Encapsulates the routes that live on the ApplicationMailbox and performs the actual routing when an inbound_email is received.
  - **Route:** Encapsulates a route, which can then be matched against an inbound_email and provide a lookup of the matching mailbox class. See examples for the different route addresses and how to use them in the ActionMailbox::Base documentation.
