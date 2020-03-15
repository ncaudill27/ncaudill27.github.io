---
layout: post
title:      "Order Up POS System Clone"
date:       2020-03-15 21:54:25 +0000
permalink:  order_up_pos_system_clone
---

___
I’d like to start off by saying JavaScript is amazing! When I realized it’s capabilities the first thing that came to mind was,

“I can finally build the POS I’ve always wanted to use.”

In the service industry one of the biggest points of concern when getting a new job is,

“I really hope their POS doesn’t suck.”

Most notably when hearing the disappointment in a manager’s tone, when they say,

“Yea we need to get around to changing that.”

A system that requires frequent changes and daily uptime should not be so difficult to update. Daily use during work hours is easy enough. But, is it possible to make a system that tracks inventory, adjusts item prices, and gives real time feedback, all from from the same user friendly interface? I aim to find out.
## Dependencies
* Rails 6.0.2.1
* Node v10.19.0
* Sqlite3 3.22.0 (for now)

## Main Features
* User friendly, intuitive interface
* Responsive element editing

## Getting Started
Having had previous troubles with Postgres and forcibly working on an unfamiliar environment I decided to get started with SQLite to make the first steps as easy as possible. Knowing I would have a 3-tier belongs_to/has_many relationship. Building out the API just enough to have 3 models and seed data (thank you [Faker](https://github.com/faker-ruby/faker) gem) seemed a logical beginning.

Doing my best to visualize from the users perspective this is the relationship model that made most sense:
```
class Category < ApplicationRecord
  has_many :subcategories
end

class Subcategory < ApplicationRecord
  belongs_to :category
  has_many :items
end

class Item < ApplicationRecord
  belongs_to :subcategory
end
```
Not only did this API structure seem easier to build but it placed a nice limitation on the user. In contrast to my original idea with a self-referential Category model. Where it would be quite easy for a system manager to conjure up some deep inheritance. Surely heading down the path of,

“Yea we need to get around to changing that.”

## Building the workflow

With the API in place and some data to play around with my first goal was to get everything on screen using click event listeners. In a way where clicking on a category would show it’s subcategories and clicking said subcategory would render the items it contains.

Then, everything rendering to the screen as it should, on to build the classic,

“My POS is better than yours” look.

Making a sidebar where Categories could be chosen to expand the Subcategories made most sense. Then rendering item cards on the main screen. The flow was coming along nicely so I decided to add a “cart” div where you could see items being added to the tab. Note: the cart is purely frontend fluff at the moment.

## Adding in the rest of CRUD
Ideally at this point is when there would be a magical “switch to manager view” but, alas adding edit and delete buttons to existing elements seemed the appropriate action. It was at this point I began to fully realize what I had signed up for. Scaling issues came on quickly and conceptual changes became more than a quick fix.

Having the “rough draft” layout made it easy to imagine how certain functionality could work. It also made it clear that a lot of what was added was simply to reach that MVP status. Nonetheless, it was an enjoyable process and I learned a lot on the way. Mainly that it’s easy to fall into anti-patterns and nice chunky functions.

Possibly the most important takeaway was how to write much neater event listeners
```
this.element.addEventListener('click', this.toggleSubmenu)

toggleSubmenu(e) {
    if (e.target.matches('.menu-item > h2')) {
        ...
	  }
}
```
Eventually gave way to
```
this.deleteBtn = this.element.querySelector('img.delete')
this.deleteBtn.addEventListener('click', ()=> subcategoriesAdapter.destroySubcategory(this.id))

destroySubcategory = subcategoryId => {
    fetch(`${this.baseUrl}/${subcategoryId}`, {
		...
		}
}
```

One fun feature I was able to get working was "saving" the state of the item cards on screen and rendering it again when needed.
```
static saveMainState = () => {
    Item.previousState = []
    let allCards = document.querySelectorAll('.card')
    allCards.forEach(card => {
        let item = Item.findById(card.dataset.itemId)
        Item.previousState.push(item)
    })
 }
 
static getMainState = () => {
    let main = document.querySelector('main')
    main.innerHTML = ''
    Item.previousState.map(item => main.appendChild(item.element))
}
```

Even though the foundation is in place it is obvious the project needs some serious maintainence. At this point I would really like to dive into adding users, logins, and separate the views. A normal user (employee) shouldn't be able to make changes to the system. However, it’s very clear that this is a good stopping point to go back, clean up, and comment extensively.

If I want this project to continue growing it’s important to make it easy to “pick up and go.” Hopefully paying that upkeep by making sure functions are small and responsible for one duty.

## Future Plans

Not only is the aforementioned separation of employee/manager flow critical, the cart is something I look forward to expanding. Even now in it’s basic state it’s clear it demands it’s own adapter. Doing so would also make it easier to allow the creation of multiple tabs at once. A must-have for any proper POS system.

It’s easy to see how that cart could easily translate to a backend Transactions class. Where once a cart is closed out and reaches a “paid for” state a new transaction is logged into the database storing items, and tab information.

The relationship betwixt Items and Subcategories needs to be adapted into a many-to-many to avoid duplication among different categories.

Once all those essentials are in place and the program can keep track of inventory and sold items. Even analytics could be put in place.

Overall, I’m very happy to have chosen a project that was familiar, do-able, and extensible.

