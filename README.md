# DBAssignment7_NormalizationAndIndex
## Exercise 1

#### Mention which violation there are to:

* First normal form (if any)
// VLAD answer here

* Second normal form (if any)

// VLAD answer here
* Third normal form (if any)

// VLAD answer here


The database state is in violation of the 3rd normal form, as the fields relation to the address of the customer and office are dependent on each other and can be abstracted to it's own "address" table to avoid data duplication.

The same can be done for the first and last name fields on the customers and employees by making a "persons" table that has the fields they share.
