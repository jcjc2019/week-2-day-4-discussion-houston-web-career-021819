# Domain Modelling Discussion Questions

### Discuss these questions with your fellow table mates and try to model some solutions to the questions  


##### Using Netflix as your model, think about/try to model some solutions for the following questions:

1 . What would a Users table look like? What columns do you think would be in the table?

CREATE TABLE users (
  id INTEGER PRIMARY KEY,
  user_name TEXT,
  email_address TEXT,
  password TEXT,
  payment_information TEXT,
  subscribed BOOLEAN,
  trial_account BOOLEAN,
  country TEXT,
  language TEXT,
  );

2 . As a user you should be able to look at a list of movies and select any individual movies to add to your Queue. How would you model the relationship between a User and their Queue of Movies? What kind of properties would a Queue have? What kind of relationships would a Queue have with other tables? _Be sure to be very clear about on which table(s) the foreign keys are found. Be sure your domain allows the same Movie to appear on many different user's queues_

CREATE TABLE queue (
  id INTEGER PRIMARY KEY,
  user_id INTEGER,               #user_id = users.id
  movie_id INTEGER,              #movie_id = movies.id
  watched TEXT/BOOLEAN?
  );

CREATE TABLE queue_#{user_id=users.id} (
  id INTEGER PRIMARY KEY,
  movie_id INTEGER,
  watched TEXT/BOOLEAN?
  );

3 . A Movie has a plot, title, rating, duration, actors/actresses, and reviews. How would you model each of these relationships with a Movie. What would would you call the relationship between an Actor and a Movie?

CREATE TABLE movies (
  id INTEGER PRIMARY KEY,
  plot TEXT,
  title TEXT,
  rating FLOAT,
  duration INTEGER
  );

CREATE apperances/cameos/roles (
  id INTEGER PRIMARY KEY,
  movie_id INTEGER,
  actor_id INTEGER
  );

CREATE movie_reviews (
  id INTEGER PRIMARY KEY,
  movie_id INTEGER,
  user_id INTEGER,
  review TEXT,
  user_rating FLOAT
  );

4 . As a user you should be able to leave a Review on a Movie. Would a Review be a property of a User or it's own table? Why? If a Reviewer does not have a direct relationship to a Movie, how can a Movie list the names of it's Reviewers? What would you call this relationship?

Reviews would be their own table. We have to break up the many to many relationship between users and movies they've reviewed. User to review is one to many, review to movie is many to one, breaking apart the many to many relationship between user and movie.

SELECT names FROM users
JOIN movie_reviews
ON movie_reviews.user_id = users.id
JOIN movies
ON movies.id = movie_reviews.movie_id
WHERE title = 'Black Panther';


<p class='util--hide'>View <a href='https://learn.co/lessons/week-2-day-4-discussion'>Domain Modelling</a> on Learn.co and start learning to code for free.</p>
