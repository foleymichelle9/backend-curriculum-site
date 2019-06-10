# Solo Project - Tiny Shop

## Learning Goals
### Rails
* Implement CRUD functionality for a resource using forms (form_tag or form_for), buttons, and links
* Use MVC to organize code effectively, limiting the amount of logic included in views and controllers
* Create routes for
  * standalone resources
  * nested resources
* Template a view in Rails using a templating language (eg, `erb`)
* Implement CRUD functionality for nested resources


### ActiveRecord
* Create instance methods on a Rails model that use ActiveRecord associations
* Use built-in ActiveRecord methods to:
  * create, read, update, and destroy records in a database
  * create records with relationships to other records in a database

### Databases
* Describe Database Relationships, including the following terms:
  * Primary Key
  * Foreign Key
  * One to Many
* Write migrations to create tables and relationships between tables
* Describe ORMs and their advantages and use cases

### Testing and Debugging
* Write feature tests utilizing:
  * RSpec and Capybara
  * CSS selectors to target specific areas of a page
* Use Pry or Byebug in Rails files to get more information about an error
* Use `save_and_open_page` to view the HTML generated when visiting a path in a feature test
* Utilize the Rails console as a tool to get more information about the current state of a development database
* Use `rails routes` to get additional information about the routes that exist in a Rails application

### Styling
* Create basic Web Pages using the following tags
  * `<h1>`, `<h2>`, etc.
  * `<p>`
  * `<body>`
  * `<a>` and the `href` attribute
  * `<img>` and the `src` attribute
  * `<div>`
  * `<section>`
  * `<ul>`, `<ol>`, and `<li>`
  * `<form>`
  * `<input>`
* Select HTML elements using classes and ids

### Web Applications
* Describe the HTTP request/response cycle
* Describe the different parts of HTTP requests and responses


## Tables and Relationships
* Merchants
  * have many items
  * Attributes
    * name
    * Address
    * City
    * State
    * Zip

* Items
  * belong to merchants
  * Attributes
    * name
    * active?
    * price
    * description
    * image
    * inventory
    * merchant_id


## High Level Tasks
* Merchant Index, Show
  * Instance methods using relationships
  * ex: number of items per merchant
* Item Index, Show
  * Instance methods using relationships
  * ex: merchant that sells the item
* CRUD Merchant
* CRUD Item (nested under a merchant)


## Rubric Notes
* Make `within` a requirement


------------------


# Paired Project

## Learning Goals
### Rails
* Use path helpers
* Describe use cases for a model that inherits from ApplicationRecord vs. a PORO
* Make use of flash messages
* Use Inheritance from ApplicationController or a student created controller to store methods that will be used in multiple controllers
* Use POROs to logically organize code for objects not stored in the database


### ActiveRecord
* Use built-in ActiveRecord methods to:
  * create queries that calculate, select, filter, and order data from a single table


### Databases
* Describe Database Relationships, including the following terms:
  * Many to Many
  * Join Table

### Testing and Debugging
* Write feature tests utilizing
  * Sad Path Testing
* Write model tests with RSpec including validations, and class and instance methods

### Web Applications
* Explain how Cookies/Sessions are used to create and maintain application state
* Describe and implement ReSTful routing
* Identify use cases for, and implement non-ReSTful routes
* Identify the different components of URLs(protocol, domain, path, query params)

## Tables and Relationships
* Existing: Merchant, Item
  * item has many order items
  * item has many orders
  * item has many reviews
* Orders
  * has many order items
  * has many items
  * attributes
  * name (of the person who made the order)
  * address
  * city
  * state
  * zip
* OrderItems
  * belongs to item
  * belongs to order
  * price (price of item at time of order)
  * quantity
* Reviews
  * belongs to item
  * title
  * description
  * rating


## High Level Tasks
* Use POROs/sessions to create a cart
  * visitor can add items to their cart
  * v can add/reduce number of specific item in cart
  * v can clear cart
  * cart should be visible on all pages
* Allow visitor to create an order by checking out
* Order show page
  * including subtotals, grand total, ship to address, and merchant
* CRUD reviews (nested under an item) (recommend pairing to review this concept)
  * using flashes to indicate to user when something went wrong
* Update Merchant/Item CRUD for sad-path (flash messaging)
* Single Table Statistics
  * Add to existing pages
* Extension - Order UD with verification code
  * visitor would get verification code upon creation of the order, would need to use that code to update or delete the order later.

------------------

# Group Project

## Learning Goals
### Rails
* Create routes for namespaced routes
* Implement partials to break a page into reusable components
* Use Sessions to store information about a user and implement login/logout functionality
* Use filters (e.g. `before_action`) in a Rails controller
* Limit functionality to authorized users
* Use BCrypt to hash user passwords before storing in the database

### ActiveRecord
* Use built-in ActiveRecord methods to join multiple tables of data, calculate statistics and build collections of data grouped by one or more attributes

### Databases
* Design and diagram a Database Schema
* Write raw SQL queries (as a debugging tool for AR)


## Tables and Relationships
* Existing: Merchants, Items, Orders, OrderItems, Reviews
  * Orders will now belong to user (instead of the address nonsense)
  * Reviews belong to a user
  * Orders will have a status (pending, packaged, shipped, cancelled)
  * Order Items will have a fulfilled indicator
  * Merchants have many reviews through items

* Users
  * have one merchant (as in, this person works for a merchant/shop)
  * have many orders
    * have many order items through orders
    * have many items through order items
  * have many reviews
  * attributes
    * role
    * name
    * address fields
    * merchant_id
    * password
    * email


## High Level Tasks
* Authentication
  * visitor can register as a user
  * visitor can log in
* As a registered user
  - Create orders through cart checkout
  - Cancel pending order
  - CRUD their profile (excluding merchant id and role)
  - log out
  - CRUD their reviews (for items they have ordered)

* As an admin user
  - ship an order
  - can assign a user to a merchant or remove a user from a merchant
  - and all merchant responsibilities
  - and all user responsibilities
  - some sort of statistics !

* As a 'merchant' user
  - fulfill order items
  - can add user to the merchant (using email as identifier)
  - can remove users from the merchant
  - CRUD only their items
    * can not delete item that has been ordered
  - some sort of statistics !

* Merchant index - will show all users who work for that merchant
* User profile page
  - including their orders
* Admin and Merchant dashboards
  - statistics
  - links to accomplish their role's tasks


------------------

# Solo Project
## Learning Goals
### Databases
* Write migrations to alter existing database tables
