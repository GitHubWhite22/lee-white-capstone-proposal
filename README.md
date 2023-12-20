# Project Title

whitespace

## Overview

whitespace is a site for visitors to find hand knitting patterns to make clothing accessories for men and women.

### Problem

I produce high quality knitwear accessories which are highly sought after by people who see them. The problem is, I don't have the time to personally knit items for everyone who would like to own something of mine. A few people have talked me into custom orders for them, and though it's rewarding to see how happy they are, it's extremely time-consuming and not economical for me to fulfill knitwear orders on a one-to-one basis.

### User Profile

Any skill level of hand knitter will be able to select and purchase a pattern from my website to be able to produce a high quality clothing accessory. The pattern will give specific guidance about which fibers can be used with which tools to create the best product. The person who purchases the pattern might be someone who's a knitter themselves, or they can find someone to follow the pattern and make the item for them.

### Features

-Site visitors will be able to sort the patterns to suit their skill level, choosing from beginner, easy, intermediate or advanced level patterns.

-Site visitors will be able to sort the patterns according to which season they are knitting for, the choices being winter, fall/spring or summer.

-Site visitors will be able to sort the patterns according to type of fibre, a very personal choice that can make or break one's enjoyment of the production process. They will be able to choose between merino, alpaca, cotton or silk.

-Site visitors will be able to navigate from links on the header to social media accounts linked to the page, where they can see more photos of the knitwear.

-Site visitors will be able to view available patterns in a gallery on the landing page that features a product photo, price, materials and skill level needed for production.

-Site visitors will be able to contact the site owner through contact details, most likely an email address, posted on the bottom of the landing page.

-Site visitors will be able to add products to a shopping cart from the gallery or from a sorted list, then navigate to the SHOPPING CART page to review their selections and total before purchasing.

-Site visitors will receive a pdf of the patterns they have purchased once they have paid for the items in their cart.

## Implementation

### Tech Stack

- React
- TypeScript
- MySQL
- Express
- Client libraries:
  - react
  - react-router
  - axios
- Server libraries:
  - knex
  - express

### APIs

- No external API's will be used for this sprint, but might be added later so that site users can access libraries of knit stitches and/or videos of stitches or techniques.

### Sitemap

THE LANDING PAGE WILL INCLUDE THE FOLLOWING:
-a HEADER with the website name, a subheader to describe the products available, social media links and a shopping cart.
-a SIDEBAR that allows site users to select their skill level, preferred season to knit an item for (spring/fall, winter or summer), and preferred fibre choice. These selections will help to screen out patterns that don't have these selected qualities.
-a GALLERY of photos of finished examples of the hand knit item patterns; the price of each pattern will be included underneath the photo, along with the skill level, season for wear and fibre.

### Mockups

\*Please refer to the attached screenshots of the sitemap.

#### Home Page

![](HomePage.png)

### Data

FOR THE HOME PAGE:

Data will be stored initially in json files, with the potential to be changed to data tables that would be served through migrations and seeds to the client side using knex and express, if time allows.

I will populate the json files more or less as follows:

{
"pattern": {
"id": "id number of pattern",
"name": "Pattern Name",
"description": "Description of knitting pattern",
"designer": "Lee White",
"price": TBD,
"difficulty": "Intermediate",
"season": "Fall/Spring",
"fibre": ["Merino", "Alpaca", "Cotton", "Silk", "Other"],
"materials": {
"yarn": "Yarn brand and type",
"needle_size": "Recommended needle size",
"other_tools": ["Stitch markers", "Tapestry needle", "Scissors"]
},
}
}

The file will include details about the knitting pattern such as pattern name, description, designer, price, difficulty level, season for wear, fibre types, and materials needed.

Placeholder values will be replaced with the values from the patterns I'm adding to the site.

FOR THE SHOPPING CART:

document.addEventListener('DOMContentLoaded', function () {
const addToCartButtons = document.querySelectorAll('.add-to-cart');
const cartItemsList = document.getElementById('cart-items');
const checkoutButton = document.getElementById('checkout-btn');

addToCartButtons.forEach(button => {
button.addEventListener('click', addToCart);
});

checkoutButton.addEventListener('click', proceedToCheckout);

function addToCart(event) {
const patternElement = event.target.closest('.pattern');
const patternId = patternElement.dataset.id;
const patternName = patternElement.dataset.name;
const patternPrice = parseFloat(patternElement.dataset.price);

    const cartItem = { id: patternId, name: patternName, price: patternPrice };

    // Send a POST request to the server to add the item to the cart
    fetch('/api/add-to-cart', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(cartItem),
    })
      .then(response => response.json())
      .then(data => {
        console.log(data.message);
        // Update the displayed cart items
        displayCartItems();
      })
      .catch(error => console.error('Error adding item to cart:', error));

}

function displayCartItems() {
// Fetch the cart items from the server
fetch('/api/checkout')
.then(response => response.json())
.then(items => {
cartItemsList.innerHTML = '';

        items.forEach(item => {
          const li = document.createElement('li');
          li.className = 'checkout-item';
          li.textContent = `${item.name} - $${item.price.toFixed(2)}`;
          cartItemsList.appendChild(li);
        });
      })
      .catch(error => console.error('Error fetching cart items:', error));

}

function proceedToCheckout() {
// Redirect to the checkout page or perform additional actions
// For now, simply log the cart items to the console
fetch('/api/checkout')
.then(response => response.json())
.then(items => {
console.log('Cart Items for Checkout:', items);
// Perform additional actions, e.g., redirect to the checkout page
})
.catch(error => console.error('Error fetching cart items for checkout:', error));
}

// Display cart items when the page loads
displayCartItems();
});

### Endpoints

The data will be screened by the radio button choices of the site visitor. HTTP GET methods will retrieve data from the json file/SQL.

POST HTTP request methods will take input from the radio buttons and calculate which selections to screen out of the visitor's view. The remaining choices will be visible in the Gallery.

### Auth

Login functionality will not be part of the scope of this project, though it may be included in nice-to-haves.

## Roadmap

- Create client

  - react project with routes and boilerplate pages

- Create server

  - express project with routing, with placeholder 200 responses

- Create migrations

- Populate database with infomation from individual patterns, aka 'items', for sale on the site

- Create seeds with knitting pattern item data

- Deploy client and server projects so all commits will be reflected in production

- Design client side to using CSS and Flexbox making an easy to navigate, uncluttered page.

The following will all exist on the Homepage:

-Feature: Header
-page title and description with cart and social media links

- Feature: Sidebar
  -radio buttons for three different sections allow users to choose preferred characteristics of patterns they wish to view for potential purchase.

  GET endpoints could be used here.
  The sections are:git
  -skill level (GET skill_level)
  -season (GET season)
  -fibre type (GET fibre_type)

  The results of these choices will appear in the Gallery

- Feature: Gallery
  Images of the items/patterns for sale will have subheadings of price, skill level, season, and fibre type.
  Clicking on an image will give the visitor the option to 'add to cart.'

- Bug fixes

- DEMO DAY

## Nice-to-haves

Link to external API's will not be integral to the functioning of this project, but it would be nice in future to have such links so that site visitors could access external libraries containing instructions for specific knit stiches, or videos demonstrating skills needed to complete the items they've purchased. Of course, all of this information will be provided on the pattern they've purchased, but it can be nice to have access to more than one point of reference, especially for those new to hand knitting.

User login would be nice as an add on.

#### Single Item Page

![](SingleItemPage.png)  
SINGLE ITEM PAGE:
-clicking on a gallery item will lead to an individual item page, where more photos of the item will be available, alongside a more specific breakdown of required tools and optional fibre choices.

#### Shopping Cart Page

![](ShoppingCart.png)
SHOPPING CART PAGE:
-while moving through the website, the user will have the option to add to or delete items from their cart. When they select the shopping cart option from the header, they will be taken to the shopping cart page, where they will be able to review the items in their cart before deciding whether or not to make a purchase.
