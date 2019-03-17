# DB-ASSIGNMENT

## Ex1

### 1.Normal form violation
* Whether the materialised view has a primary key or not depends on the implementation. However the table does have the customerNumber column with unique values so this could be set as primary key.
* Eventhough the names and address has been concated one could still argue that those columns are a single domain.

### 2.Normal form violation
To access this I assume that customerNumber is implemented as the primary key in the materialized view.
* The column *repCity* is dependant on the column *repZip*. Thats why if a new city name was associated with the zipcode this would have to be updated in every row with that zipcode. This breaks the 2nd normal form that "all non-key columns are dependant on all of the tables primary key".

### 3.Normal form violation
* Columns starting with *rep* does not describe the customerNumber.Means columns does not belong to this table in order to live up to the 3rd normal form.

## Ex2

Here we use the customerName and the contactPhone as a primary key because both origins from columns that does not allow null. It is also rather unlikely (though not impossible) that to (people with the same name) = (phone number registered). If to people shares the same phone no they might also live together on same address which is why *contactName, custCity* and *custCountry* is not included in the primary key. This does not change above mentioned normal forms violations.

### Also, mention if there are any new issues with normal forms.

## Ex3

### 3.1: Write a safe update statement that change the repPhone column from oldNumber (say 12345678) to newNumber (say 87654321).

    USE classicmodels;
    START TRANSACTION;

    UPDATE CustomerOverview SET repPhone="87654321"
    WHERE repPhone="12345678";

    COMMIT;

The statement uses a transaction which disables MySQLs autocommit and rolls back the changes if something goes wrong before the transaction is committed.

### 3.2: Write an update of repEmail which do not update properly (do not update it everywhere it should)

    USE classicmodels;
    UPDATE CustomerOverview SET repPhone="87654321"
    WHERE repPhone="12345678" LIMIT 1;

So it is supposed to update the repPhone where the repPhone is 12345678 but it only updates the first row that meets that condition. The statement is also not atomic.

## Ex4
![Query execution plan]
(https://raw.githubusercontent.com/ark1979/DB-Assignment7/master/b%2B%20tree%20diagram.png)

### Explain how the index is used to find "Handji Gifts& Co" - that is, the path through the tree to get to the right row.
* Compared in terms of alphabetic order: 'Australian Collectors, Co.', 'Down Under Souveniers, Inc', 'GiftsForHim.com'.
* Since H comes after 'GiftsForHim.com' we then take a look at the last branch.
* We find 'GiftsForHim.com' and get the row index
* We get the value from the table index
