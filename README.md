# mysql-postgres

## practice with sql and postgres

where postgres is located  -- (~)$ ls /etc/postgresql/10/main/
see if running --  service postgresql status

to run first time -- sudo su postgres

then command line tool type -- psql (then your are in a shell)

when in shell -- \l (will tell you what db's are there), \du (tells users)
create user -- createuser -s brian (creates superuser brian)
change password -- ALTER USER brian WITH PASSWORD 'brian';

cancel out of shell -- \q


dbeaver - gui for working with db
file, new, postgres - to start new

CREATE TABLE
---------------------------------------
create table users (
  id serial primary key, // dont change the id
  first_name varchar(255) not null,
  last_name text
  age int
  email text unique not null
)

drop table users // delete db

insert into users (first_name, last_name, age, email);
values
('bob', 'lastname', 19, 'bob@bob.com') // adding info into the db, you can leave out columns and they will be null


SELECTS
-------------------------------
select first_name from users;  // see data in db

select first_name, last_name from users;

select * from users;  // will see all the rows for the db table

alter table users drop colum age; // gets rid of age column
alter table users add column age int;


WHERE
--------------------------------
select * from users where id = 3 or id = 4;
select * from users where id = 3 and first_name = 'bob';
select * from users where id in (3, 4, 5); // 3 users will return
select * from users where where age > 10;

COALESCE
---------------------------------
select * from users where where coalesce(age, 15) > 10; // 15 is the default if age is null


