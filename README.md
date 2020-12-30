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
select * from users where age > 10;

COALESCE
---------------------------------
select * from users where coalesce(age, 15) > 10; // 15 is the default if age is null


WHERE AND NULL
------------------------------------
select * from users where age is null;


UPDATE
-------------------------------------
update users
set age = 20, // or age + 1
  last_name = 'tom'
where id = 1; // doesnt have to be 3 lines

DELETE
---------------------------------------
delete from users
where id = 3;
// you can do conditions as well

REFERENCES or ForeignKey
----------------------------------------
basically connecting one table to another table user to post, usually you reference the primary key on the other table

-- 1 to many relationship or 1 to m --

create table posts(
  id serial primary key,
  title text not null,
  body test default 'something',
  creatorID int referenceees users(id) not null
);

// creatorID references the prev table

insert into posts (title, body, creatorID)
values ('first post', 1)

insert into posts (title, body, creatorID)
values ('second something post', 1)


INNER JOINS - getting info from two tables
------------------------------------------
select first_name from users
inner join posts on users.id = posts.creatorID

-- inner join only gets users wtih posts created or if the factors are true
-- x * (y,z) = (x,y), (x,z)

LEFT JOIN
-----------------------------------------
select first_name from users
left join posts on users.id = posts.creatorID

-- this also grabs other users who don't have posts -- '

GIVE COLUMNS ALIAS
---------------------------------------

select u.id, p.id post_id, first_name, title from users u -- also post_id is a alias for p.id
inner join posts p on u.id = p.creatorId  -- posts p , posts is referred to p now

WHERE
---------------------------------------
have access to both tables when there is a join

select u.id, p.id post_id, first_name, title from users u
inner join posts p on u.id = p.creatorId
where u.id = 1;
-- all rows where u.id is 1

LIKE
--------------------------------------
% = pattern matches anynumber of chars

select u.id, p.id post_id, first_name, title from users u
inner join posts p on u.id = p.creatorId
where p.title like '%second%' -- any number of characters before or after the word second

-- %post .. it has to end with the word post --
-- post% .. " " starts with post
-- %post% .. anywhere
-- %my%post% is also valid
it is case sensitive

ilike -- ignores case sensitivit


 -- 1 to many with posts, single post can have many comments
 -- 1 to many with users, single user can have many comments
create table comments (
  id serial primary key,
  message text not null,
  post_id int references posts(id) -- this references what post id the comment
  creator_id int references user(id)



)
