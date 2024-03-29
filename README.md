# DBAssignment7_NormalizationAndIndex
## Exercise 1

### Mention which violation there are to:

#### First normal form (if any)
##### Answer

* There are no first normal form violations because we have identified primary keys for each table used and no multivalued attributes.

#### Second normal form (if any)
##### Answer

* There are no second normal form violations because there are no partial dependencies (mainly because each table has only one primary key)

#### Third normal form (if any)
##### Answer

* The database state is in violation of the 3rd normal form through transitional dependencies, as the fields relation to the address of the customer and office are dependent on each other and can be abstracted to it's own "address" table to avoid data duplication.

* The same can be done for the first and last name fields on the customers and employees by making a "persons" table that has the fields they share.


## Exercise 2

Assume we did not include the customerNumber in the table. What could be a key, and do we get the same violations of the normal forms?

#### Answer

*  Given that we did not use the composite-key which is "customerNumber", the best alternative "key" to use would then be "customerName". This would result in the violations staying the same in the normal forms. 

## Exercise 3

##### Q1
Write a safe update statement that change the repPhone column from oldNumber (say 12345678) to newNumber (say 87654321).

#### Answer

```sql

UPDATE customeroverview
SET repPhone = '+1 666 999 1984'
WHERE customerName = 'Scandinavian Gift Ideas'  AND customerNumber <> 0;

```

Updating the repPhone changes all the numbers for the representatives located in the same city. That points to the fact that repPhone is dependent of the repCity and not to the repName.


* View before execution
![picture](https://github.com/FarkIst/DBAssignment7_NormalizationAndIndex/blob/master/img/UpdateNoB4.PNG)

* View after execution
![picture](https://github.com/FarkIst/DBAssignment7_NormalizationAndIndex/blob/master/img/UpdateNoAfter.PNG)

##### Q2
Write an update of repEmail which do not update properly (do not update it everywhere it should)

#### Answer

```sql

UPDATE CustomerOverview
SET repEmail = 'bananaspliffy@smuk.com'
WHERE custCity = 'Auckland';

```


## Exercise 4
In this exercise we will assume we have materialized this query into a table `tblEx4Sydney`.

```sql
with my_cust as
   (select customerNumber,
       customerName,
       customers.country as custCountry,
       offices.city      as repCity
    from employees
       inner join customers on employees.employeeNumber = customers.salesRepEmployeeNumber
       inner join offices on employees.officeCode = offices.officeCode)
select *
from my_cust
where repCity = 'Sydney'
```

Assume we have an index on customerName, and assume a fan-out in the B+ tree of 4. 

**Draw** a representation of of the B+ tree with index and leaf nodes, as well as the actual table data. The drawing must be a combination of Figure 1.1 and 1.2 from [Anatomy of an SQL index](https://use-the-index-luke.com/sql/anatomy).
