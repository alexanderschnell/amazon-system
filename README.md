# AmazonSystem

A console-based Amazon-style store written in Java. It loads a real product catalogue from CSV and lets you manage customers, credit, wishlists, carts, purchases and product reviews from a colour-coded terminal menu.

> 📚 **School project:** Assignments 01 & 02 for *Level 2 Object-Oriented Programming* (Nov 2024). It's kept here as an archive and is not actively maintained.

## Features

**Admin**
- Load the product catalogue from `Sample-Amazon-Products-v2.csv`. The parser handles quoted fields, commas inside names and currency symbols.
- List and search products.
- Add and list customers.

**User**
- **Credit:** add funds to a customer as cash, check or card.
- **Wishlist:** add, remove and list products.
- **Cart:** add and remove items, view the cart, and buy everything in it using the customer's credit.
- **Comments:** review products. Customers can only comment on products they have actually bought.

All input is validated, and errors are reported through a custom `AmazonException`.

## Design

The assignment focused on core OOP concepts:

| Concept | Where |
|---|---|
| Abstract class + inheritance | `AmazonCredit` → `AmazonCash`, `AmazonCheck`, `AmazonCard` |
| Interface | `AmazonPayable`, implemented by `AmazonCart` |
| Composition | `AmazonCustomer` holds credits, wishlist, cart, purchases and comments |
| Custom exceptions | `AmazonException` |
| Utility / validation layer | `AmazonSystemUtil` |
| Menu controller | `AmazonManager` (entry point) |

```
src/amazonSystem/
├── AmazonManager.java          # main menu + program flow
├── AmazonProduct*.java         # product, category, sub-category, CSV-backed list
├── AmazonCustomer.java
├── AmazonCredit.java           # abstract payment type
│   ├── AmazonCash.java
│   ├── AmazonCheck.java
│   └── AmazonCard.java
├── AmazonCart.java / AmazonCartItem.java
├── AmazonComment.java
├── AmazonPayable.java
├── AmazonException.java
├── AmazonSystemUtil.java
└── Test*.java / AllTests.java  # JUnit 5 test suite
```

## Running it

Requires Java 17+.

```bash
java -jar AmazonSystem.jar
```

Keep `Sample-Amazon-Products-v2.csv` in the same folder, then choose **A** to load the product list.

Or open the project in Eclipse or IntelliJ and run `AmazonManager`.

## Tests

`AllTests` runs the JUnit 5 suite: `TestCart`, `TestComments`, `TestCredits` and `TestWishlist`. These cover the wishlist, cart, credit and comment rules.

## Screenshots

Branching and commit history from development:

![Branches](GitHub%20Screenshots/BranchScreenshot.png)
![Commit history](GitHub%20Screenshots/CommitHistory.png)
