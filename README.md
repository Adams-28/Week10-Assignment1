# Week 10 Assignment 1: Modeling Database Relationships with JPA (Library System)

## Database Relationship Diagram

```text
AUTHORS
-------
id (PK)
name
   |
   | 1
   |
   | N
BOOKS
-----
id (PK)
title
author_id (FK)
publisher_id (FK, UNIQUE)
   |                      |
   | 1                    | 1
   |                      |
   | 1                    | N
PUBLISHER             BOOK_GENRES
---------             -----------
id (PK)               book_id (FK)
publisher_name        genre_id (FK)
contract_date              |
                           | N
                           |
                           | 1
                         GENRES
                         ------
                         id (PK)
                         name
```

## Relationship Explanations

### One-to-Many: Author and Book

The One-to-Many relationship was chosen for the author since a single author can write many books, but each book can only contain one author.

The `Author` entity uses `@OneToMany`, while the `Book` entity uses `@ManyToOne`. The `Book` entity owns the relationship because its table contains the `author_id` foreign key.

### One-to-One: Book and Publisher

The One-to-One relationship was chosen because each book should have one publisher and vice versa.

The `Book` entity owns the relationship and uses `@JoinColumn` to store the `publisher_id` foreign key whereas the Publisher entity uses 'mappedBy'

### Many-to-Many: Book and Genre

The Many-to-Many relationship was chosen because each book can have multiple genres, and the same genre can apply to multiple books.

The `Book` entity defines the relationship using `@ManyToMany` and `@JoinTable`.

The `Genre` entity uses `mappedBy' = "genres"` to specify it is the non-owning side

## FetchType Choices

`FetchType.LAZY` was selected for all the relationships to as it is not necessary to load every associated entity if they are not needed.

For example, retrieving an author does not require immediately loading all their books.

This helps with reducing unnecessary database queries and improving efficiency

## Testing Output

When running the LibrarySystemApplication the following output should be displayed to show each of the entities working correctly:

```text
--- Authors and Books ---

Author: Timothy Zahn
 Book: Star Wars: Heir to the Empire
 Publisher: Bantam Spectra
 Contract Date: 1991-05-01
 Genres:
   - Space Opera
   - Science Fiction

 Book: Cobra Alliance
 Publisher: Baen Books
 Contract Date: 2009-12-01
 Genres:
   - Space Opera
   - Science Fiction

Author: Christie Golden
 Book: World of Warcraft: Before the Storm
 Publisher: Pocket Books
 Contract Date: 2009-04-21
 Genres:
   - Epic Fantasy
   - Adventure

 Book: Arthas: Rise of the Lich King
 Publisher: Del Rey
 Contract Date: 2018-06-12
 Genres:
   - Epic Fantasy
   - Adventure
```
