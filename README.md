Prerequisites
=============

1. Node.js

http://nodejs.org/

2. Heroku toolbelt

https://toolbelt.heroku.com/

3. Postgresql

	$ sudo apt-get install postgresql

Tutorial
========

Clone this repo:

	$ git clone https://github.com/FTraian/node-express-postgresql-heroku-tutorial.git 	

Create a Heroku app. Be careful as <app-name> is global on Heroku so another user might already have the 'test' name:

	$ cd node-express-postgresql-heroku-tutorial
	$ heroku create <app-name>

Add Postgresql to your app:

	$ heroku addons:add heroku-postgresql:dev

Get DB details: 

	$ heroku config | grep HEROKU_POSTGRESQL

They will look as: HEROKU_POSTGRESQL_IVORY_URL: postgres://user:password@ec2-54-235-156-5.compute-1.amazonaws.com:5432/database

Promote the DB as primary DB:

	$ heroku pg:promote HEROKU_POSTGRESQL_IVORY_URL
You should now be able to reference it as DATABASE_URL but due to a bug in heroku it's not working at the moment. Instead we will use the full connection sring in web.js.

In order to use DB from local machine set PGSSLMODE variable:

	$ export PGSSLMODE=require

Create table and add some data:

	$ heroku pg:psql

 	> CREATE TABLE MyTable (id int NOT NULL, name varchar(255) NOT NULL, PRIMARY KEY(id))
 	> INSERT into MyTable VALUES (1, 'First USer'), (2, 'Second User');

Install required modules: 

	$ npm install

Start application locally: 

	$ foreman start

Access app at: http://localhost:5000

View the logs:

	$ heroku logs

Deploy app to heroku:

	$ git push heroku master

Access remote app:

	$ heroku open