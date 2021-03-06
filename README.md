# Getting Started with SQL

### Install postgres : 
-brew install postgres

-Heed the post-install notes. There may be something like: 
  "To have launchd start postgresql at login:"
  <blockquote>
        ln -sfv /usr/local/opt/postgresql/*.plist ~/Library/LaunchAgents
  </blockquote>

-Then to load postgresql now:
  <blockquote>
    launchctl load ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist
  </blockquote>
  
But most importantly, you should run : 

<blockquote>
 postgres -D /usr/local/var/postgres
</blockquote>

Running brew info postgres can help you see what your options are after the setup screens are gone. 


Now Postgres should be running.  
You can check to see whether or not psql is running by looking at all system processes related to postgres: 
ps aux | grep postgres

nmuta           34650   0.0  0.0  2463676   3260 s003  S+    7:37AM   0:00.01 psql postgres
nmuta           30961   0.0  0.0  2455484   3276 s002  S+    6:26AM   0:00.01 psql postgres
nmuta           35738   0.0  0.0  2432772    652 s004  S+    8:38AM   0:00.00 grep --color=auto psql

notice that the last matching "process" is actually the search we just did, so ruling that one out, we have two matching processes.  

To get into the psql terminal as the default user, type: 
psql postgres 

You should now see a command prompt.: 
        postgres=# 

In the terminal now, we can see the defaults that ship with postgres, but we don't have any user created databases yet. 

### list databases: 
\l
(backslash and then the letter “l” as in lemon

Use the above command to list the current databases. 

Now , create a new database with the command below: 

### create database: 
CREATE DATABASE mydatabase; 

Now list your databases again, and you should see the database that you created. 

Once we've created a database, even if its empty, we have to "connect" to it in order to do queries: 

### connect to a database: 
\c mydatabase; 


Even though we don't want to drop the database yet, later we can drop it with this command: 
### drop database:
DROP DATABASE demodb1;


## Importing a Database

To exit the postgres cli ( command line interface) , do \q ; 

We can import a database from the standard bash window. 

Navigate to where world.sql is stored ( should be in the repo you cloned). 

### import a database (outside of the psql command prompt, from terminal ) : 
psql mydatabase < world.sql

OR 
psql mydatabase < ~/path/to/file/world.sql  ( if you're in a different directory) . 


Although we will not be using it now, we can also dump from terminal:
### dump (export) a database: (outside of the psql command prompt, from terminal ) : 
pg_dump mydatabase > new_file_name.sql


Ok, so now we can go back into the terminal and view our data. 
        psql postgres


### describe tables: 
\dt;

### describe one table:
\d tablename; 


Now , we are ready to start doing some queries. 


Before we continue, install PGCommander. 

PGCommander is useful because not only is it cleaner than using the psql cli, it allows you to export and save queries. 


Here are some ways that we can do CRUD in SQL : 

##QUERIES: 

- Insert

INSERT into tbl values('fred', 'scott', 'denver', 'colorado'); 
INSERT into tbl ('name', 'city') values ('fred', 'denver');

- Select
SELECT * from tbl; 
SELECT * from tbl WHERE column_name  = ‘desired_value’ ; 
SELECT name from tbl where weight = (select max(weight) from tbl)
SELECT name from products where price > 5.00 

- Update
UPDATE televisions SET cost=5000, discount='20' WHERE id=25;

- Delete
DELETE from country WHERE code='SSD' ; 

- JOIN
SELECT customer.name from customers INNER JOIN purchases ON purchases.customer_id = customer.id
SELECT customer.tag as customer_tag, purchase.tag as purchase_tag from customers INNER JOIN purchases ON purchases.customer_id = customer.id


- CREATING A NEW TABLE 
CREATE TABLE Persons
(
PersonID int,
LastName varchar(255),
FirstName varchar(255),
Address varchar(255),
City varchar(255)
);




### fyi: a list of data types in postgres:
http://www.postgresql.org/docs/9.1/static/datatype.html



### South Sudan data:
'SSD', 'South Sudan', 'Africa', 'Eastern Africa', 193, 2014, 193000, 72, 5796, 400, 'South Sudan', 'Federal Presidential Republic', 'Salva Kiir Mayardit', 4075, 'SS';

 


##EXERCISES: 

PLEASE LOCALLY SAVE all of your queries after inserting them. 

Since this data was created, a new country, South Sudan, is now part of the global map.  Using the above "South Sudan data", 
add South Sudan to the list of countries. 

Insert a new country called "Atlantis", using modified South Sudan data. Make the country code "ATL" , and an  independence date of 1

Update Atlantis after you create it changing the to "ATS" and changing the independence date to 2015

Select all countries who have more than 156 million people

Select the country wtih the highest gross national product 

Select all of the countries and their capitals in one query 

Going back to your Mongo associations assignment, create some tables and then do a join to join one or more tables. 

When you have finished doing the join query, export that query and then email me the query 

Delete Atlantis from the country table







