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

## User Stories

TODO:
Items can only be added to cart if they are active

### Navigation

```
[item-link-nav]
title: Item Link Navigation
labels: items
story_text: As a visitor
    With the exception of an item's show page,
    Anywhere I see an item name on the site,
    I can click on the item name to go to that item's show page.

[merchant-link-nav]
title: Merchant Link Navigation
labels: merchants
story_text: With the exception of an merchant's show page,
    Anywhere I see an merchant name on the site,
    I can click on the merchant name to go to that merchant's show page.
```

### Cart & Order

```
[cart-indicator]
title: Cart Indicator
labels: cart
story_text: As a visitor
    I see a cart indicator in my navigation bar
    The cart indicator shows a count of items in my cart
    I can see this cart indicator from any page in the application

[create-cart]
title: Cart Creation
labels: cart
depends_on: cart-indicator
story_text: As a visitor
    When I visit an item's show page from the items index
    I see a link or button to add this item to my cart
    And I click this link or button
    I am returned to the item index page
    I see a flash message indicating the item has been added to my cart
    The cart indicator in the navigation bar increments my cart count

[cart-show]
title: Cart Show Page
labels: cart
depends_on: create-cart
story_text: As a visitor
    When I have added items to my cart
    And I visit my cart ("/cart")
    I see all items I've added to my cart
    Each item in my cart shows the following information:
      - the name of the item
      - the item image
      - the merchant I'm buying this item from
      - the price of the item
      - my desired quantity of the item
      - a subtotal (price multiplied by quantity)
    I also see a grand total of what everything in my cart will cost

[view-empty-cart]
title: Empty Cart Show Page
labels: cart
depends_on: empty-cart
story_text: As a visitor
    When I add NO items to my cart yet
    And I visit my cart ("/cart")
    I see a message that my cart is empty
    I do NOT see the link to empty my cart

[empty-cart]
title: Emptying Cart
labels: cart
depends_on: create-cart
story_text: As a visitor
    When I have items in my cart
    And I visit my cart ("/cart")
    And I click the link to empty my cart
    Then I am returned to my cart
    All items have been completely removed from my cart
    The navigation bar shows 0 items in my cart

[remove-cart-item]
title: Removing Item from Cart
labels: cart
depends_on: create-cart
story_text: As a visitor
    When I have items in my cart
    And I visit my cart
    Next to each item in my cart
    I see a button or link to remove that item from my cart
    - clicking this button will remove the item but not other items

[increase-cart-item-quantity]
title: Adding Item Quantity to Cart
labels: cart
depends_on: create-cart
story_text: As a visitor
    When I have items in my cart
    And I visit my cart
    Next to each item in my cart
    I see a button or link to increment the count of items I want to purchase
    I cannot increment the count beyond the item's inventory size

[decrease-cart-item-quantity]
title: Decreasing Item Quantity from Cart
labels: cart
depends_on: create-cart
story_text: As a visitor
    When I have items in my cart
    And I visit my cart
    Next to each item in my cart
    I see a button or link to decrement the count of items I want to purchase
    If I decrement the count to 0 the item is immediately removed from my cart

[checkout-link]
title: Link to Checkout
labels: cart, order
depends_on: create-cart
story_text: As a visitor
    When I have items in my cart
    And I visit my cart
    I see a button or link to Checkout
    When I click that button, I am taken to the new order page

[new-order]
title: New Order Page
labels: cart, order
depends_on: checkout-link
story_text: As a visitor
    When I check out from my cart
    On the new order page I see the details of my cart:
      - the name of the item
      - the merchant I'm buying this item from
      - the price of the item
      - my desired quantity of the item
      - a subtotal (price multiplied by quantity)
      - a grand total of what everything in my cart will cost
    I also see a form to where I must enter my shipping information for the order:
      - name
      - address
      - city
      - state
      - zip
    I also see a button to 'Create Order'

[create-order]
title: Order Creation
labels: order
depends_on: new-order
story_text: As a visitor
    When I fill out all information on the new order page
    And click on 'Create Order'
    An order is created and saved in the database
    And I am redirected to that order's show page with the following information:
      - My name and address (shipping information)
      - Details of the order:
        - the name of the item
        - the merchant I'm buying this item from
        - the price of the item
        - my desired quantity of the item
        - a subtotal (price multiplied by quantity)
        - a grand total of what everything in my cart will cost
        - the date when the order was created

[create-order-sadpath]
title: Order Creation, cont.
labels: order
depends_on: create-order
story_text: As a visitor
    From the order creation page
    When I click 'Create Order' without completing the shipping address form
    I see a flash message indicating that I need to complete the form for successful order creation
```

### Item Reviews

```
[item-reviews]
title: Reviews on Item Show Page
labels: reviews
story_text: As a visitor,
    When I visit an item's show page,
    I see a list of reviews for that item
    Each review will have:
    - title
    - content of the review
    - rating (1 to 5)

[create-review]
title: Review Creation
labels: reviews
depends_on: item-reviews
story_text: As a visitor,
    When I visit an item's show page
    I see a link to add a new review for this item.
    When I click on this link, I am taken to a new review path
    On this new page, I see a form where I must enter:
    - a review title
    - a numeric rating that can only be a number from 1 to 5
    - some text for the review itself
    When the form is submitted, I should return to that item's
    show page and I should see my review text.

[create-review-sadpath]
title: Review Creation, cont.
labels: reviews
depends_on: item-reviews
story_text: As a visitor,
    When I fail to fully complete the new review form, but still try to submit the form
    I see a flash message indicating that I need to complete the form in order to submit a review

[review-stats]
title: Review Statistics
labels: reviews, statistics
story_text: As a visitor
    When I visit an item's show page,
    I see an area on the page for statistics about reviews:
    - the top three reviews for this item (title and rating only)
    - the bottom three reviews for this item  (title and rating only)
    - the average rating of all reviews for this item

[edit-review]
title: Edit a Review
labels: reviews
depends_on: item-reviews
story_text: As a visitor,
    When I visit an item's show page
    I see a link to edit the review next to each review.
    When I click on this link, I am taken to an edit review path
    On this new page, I see a form that includes:
    - title
    - numeric rating
    - text of the review itself
    I can update any of these fields and submit the form.
    When the form is submitted, I should return to that item's
    show page and I should see my updated review

[delete-review]
title: Delete a review
labels: reviews
depends_on: item-reviews
story_text: As a visitor,
    When I visit an item's show page,
    I see a link next to each review to delete the review.
    When I delete a review I am returned to the item's show page
    Then I should no longer see that review.
```

### Merchant

```
[delete-merchant]
title: Controlling Merchant Destruction
labels: merchant
story_text: As a visitor
    If a merchant has items that have been ordered
    I can not delete that merchant
    Either:
      - there is no button visible for me to delete the merchant
      - if I click on the delete button, I see a flash message indicating that the merchant can not be deleted.

[merchant-manipulation-sadpath]
title: Flash Messages for Merchant Create and Update
labels: merchant
story_text: As a visitor
    When I am updating or creating a new merchant
    If I try to submit the form with incomplete information
    I see a flash message indicating which field(s) I am missing

[merchant-stats]
title: Merchant Statistics
labels: merchant, statistics
story_text: As a visitor
    When I visit a merchant's show page
    I see statistics for that merchant, including:
      - count of items for that merchant
      - average price of that merchant's items
      - Distinct cities where my items have been ordered
```

### Item

```
[delete-item-reviews]
title: Deleting Items Deletes its Reviews
labels: items, reviews
story_text: As a visitor
    When I delete an item
    All reviews associated with that item are also deleted

[delete-item-orders]
title: Items with Orders Cannot be Deleted
labels: items, orders
story_text: As a visitor
    If an item has been ordered
    I can not delete that item
    Either:
      - there is no button visible for me to delete the item
      - if I click on the delete button, I see a flash message indicating that the item can not be deleted.

[item-manipulation-sadpath]
title: Flash Message for Item Create and Update
labels: items
story_text: As a visitor
    When I am updating or creating a new item
    If I try to submit the form with incomplete information
    I see a flash message indicating which field(s) I am missing
```


### Extensions

```
[review-sort]
title: Sortable Reviews
labels: reviews, extension
story_text: As a visitor,
    When I visit an item's show page to see their reviews,
    I see additional links to sort their reviews in the following ways:
    - sort reviews by highest rating, then by descending date
    - sort reviews by lowest rating, then by ascending date

[ext-merchant-stats]
title: More Merchant Statistics
labels: merchant, statistics, extension
story_text: As a visitor,
    When I visit an merchant's show page
    I see the top 3 highest rated items for that merchant (by average rating)

[order-crud]
title: Order Update and Delete
labels: order, extension
story_text: As a visitor
    When I check out
    I see a flash message with a randomly generated, 10 digit verification code associated with that order
    NEWLINE
    I can use that verification code to search for an order through the nav bar.
    If an order is found, I am redirected to a verified order page ('/verified_order')
    On that verified order page, I can:
      - click a link to delete the order
      - update the shipping address for an order
      - remove items from the order
```

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


### Merchant User Stories
```
[merchant-users-index]
title: Merchant Sees Their Users
labels: merchant
story_text: As a Merchant User
    When I visit my dashboard
    I see a link to see 'Merchant Users'
    When I click this link
    I am taken to my merchants users page
    And I see all users assigned to my Merchant
    For each user I see:
      - Name
      - Email
      - A link to remove that user from this merchant

[merchant-removes-user]
title: Merchant Removes User
labels: merchant
depends_on: merchant-users-index
story_text: As a Merchant User
    When I visit my merchant's users page
    I see a link or button to remove a user from the merchant
    When I click that link or button
    I am returned to my merchant's users page
    And I no longer see that user
    NEWLINE
    Now, when the user that I removed attempts to log in, they will be logged in as a regular.

[merchant-adds-user]
title: Merchant Adds User
labels: merchant
depends_on: merchant-users-index
story_text: As a Merchant User
  When I visit my merchant's users page
  I see a form to add a new user to the merchant
  Then I fill in the form with an existing user's email address
  And click 'Add User to Merchant'
  Then I am redirected back to my merchant's users page
  And I see that user listed along with the other merchant users for my merchant.
  NEWLINE
  I can only add a user who exists, is not an admin user, and is not assigned to a merchant.
  Now, when the user that I added logs in, they will be logged in as a merchant user.

[merchant-items-placeholder-image-notification]
title: Merchant Sees Items that Need Images
labels: merchant, item
story_text: As a Merchant User
    When I visit my dashboard
    I see an area listing all items that are using a placeholder image
    Each item name is a link to that item's edit page
    When I click on that link
    And update the item with an image
    I am returned to my Items index
    When I next visit my dashboard, that item is no longer listed as needing an image

[merchant-unfulfilled-revenue]
title: Merchant Sees Unfulfilled Revenue
labels: merchant, item
story_text: As a Merchant User
    When I visit my dashboard
    I see statistics showing:
      - How many orders are unfulfilled
      - How much revenue those unfulfilled orders would generate for my merchant

[merchant-sees-unfulfillable-orders]
title: Merchant Sees Unfulfillable Orders
labels: merchant, item, order
story_text: As a Merchant User
    When I visit my dashboard
    In my list of orders
    I see a warning message (Inventory Conflict) next to any order that has an order_item quantity that exceeds my available inventory for that item

[merchant-sees-unfulfillable-order-combos]
title: Merchant Sees Unfulfillable Order Combinations
labels: merchant, item, order
story_text: As a Merchant User
    When I visit my dashboard
    In my list of orders
    If an item has been ordered more than once, and the sum of those order_item quantities exceed the available item inventory
    I see a warning next to all affected orders indicating 'Multiple Order Conflict'

[merchant-adds-bulk-discount]
title: Merchant Can Add a Bulk Discount
labels: merchant, bulk_discount
depends_on: merchant-bulk-discount-index
story_text: As a Merchant User
    When I visit my merchant's discount index
    I see a link or button to Add a Bulk Discount
    When I click that link or button
    I am taken to a new bulk-discount form where I enter the following information:
      - name
      - amount of the bulk-discount in dollars/cents (ex: .5 means the bulk-discount is for $0.05 off an item's price)
      - quantity needed to activate the bulk discount
    When I click "Create Discount"
    I am redirected back to my merchant's discount index

[merchant-bulk-discount-index]
title: Merchant sees all bulk discounts
labels: merchant, bulk_discount
story_text: As a Merchant User
    When I visit my dashboard
    I see a link or button labeled 'Discounts'
    When I click that link or button
    I am taken to a page where I can see all my merchant's existing discounts
    For each discount, I see:
      - Name
      - Amount
      - Quantity Needed to activate the discount
      - Link or button to edit the discount
      - Link or button do delete the discount

[merchant-edits-bulk-discount]
title: Merchant Edits Discount
labels: merchant, bulk_discount
story_text: As a Merchant User
    When I visit my merchant's discounts page
    And click 'Edit' next to a discount
    I am taken to a form to edit the discount (the form prepopulates with the current discount information)
    On that form, I can edit the:
      - Name
      - Amount
      - Quantity Needed
    When I click 'Update Discount'
    I am returned to my merchant's discounts page
    And I see the updated information
    NEWLINE
    Updating a discount does not change any existing order_item prices

[merchant-deletes-bulk-discount]
title: Merchant Deletes Discount
labels: merchant, bulk_discount
story_text: As a Merchant User
    When I visit my merchant's discounts page
    And click 'Delete' next to a discount
    The discount is deleted and I am returned to the merchant's discounts page
    NEWLINE
    Deleting a discount does not change any existing order_item prices

[user-orders-with-bulk-discount]
title: User Activates a Bulk Discount
labels: order, bulk_discount
story_text: As a Regular User
    When a merchant has a discount
    And I add items to my cart from that merchant, and the quantity meets the requirements for the bulk discount
    I see an updated cost per item (the discounted cost)
    When I click Check Out, the order_item subtotal and order grand total reflect the discounted price.
    NEWLINE
    If I have items in my cart from more than one merchant, the discount will only apply to items from the merchant that has the discount.
    If I add multiple items from the merchant with the bulk discount, only the items which meet the discount quantity will have a reduced price - the items which do not meet that quantity will be the stated price.
```


------------------

# Solo Project
## Learning Goals
### Databases
* Write migrations to alter existing database tables
