# PostgreSQL Movies Database
This project is a simple implementation of a **PostgreSQL database** for storing movie data, created as part of my **Codecademy off-platform project.** The database contains a table for movies, with columns for film name, release year, runtime, category, rating, and box office earnings.

## Project Overview
The goal of this project was to practice using PostgreSQL locally by creating a database, building a table, and inserting data. The project follows these main steps:

**Creating the Table:** Created a table named films to store movie details.
**Inserting Data:** Inserted movie records with basic details such as name and release year.
**Adding Supplementary Information:** Added additional attributes like runtime, category, rating, and box office earnings.
**Dealing with Duplicates:** Implemented a strategy to remove duplicate movie entries.
**Adding Constraints:** Applied constraints to ensure data integrity.

## Steps to Set Up

1. **Setting Up the Database**
I created a new PostgreSQL database using the CREATE DATABASE SQL command.
A table called films was created to store movie data, with columns for name (TEXT) and release_year (INTEGER).
2. **Inserting Movie Data**
Movie records were inserted into the films table using INSERT INTO SQL commands.
Movies inserted included:
The Matrix (1999)
Monster's Inc. (2001)
Call Me By Your Name (2017)
3. **Adding More Movie Attributes**
Additional columns were added to the films table to store more detailed movie information:
runtime (INTEGER)
category (TEXT)
rating (DECIMAL)
box_office_earnings (BIGINT)
This was done using ALTER TABLE and ADD COLUMN.
4. **Handling Duplicates**
After adding data, I discovered that duplicate movie entries were inserted. This happened due to a lack of constraints on movie names and release years.
To resolve this, I used the following query to remove duplicate rows, keeping the first occurrence:
sql
Copy
Edit
DELETE FROM films
WHERE ctid NOT IN (
    SELECT MIN(ctid)
    FROM films
    GROUP BY name, release_year
);
This query checks for duplicate name and release_year pairs and deletes the redundant rows.
5. **The "Monster's Inc." Apostrophe Issue**
While inserting data, an issue arose with the movie Monster’s Inc. due to the apostrophe in the title.
Initially, the apostrophe was causing errors in queries, and NULL values were being inserted into certain fields.
The issue was fixed by correctly escaping the apostrophe: Monster\s Inc. instead of Monster’s Inc..
Once fixed, the relevant data was successfully added to the database.
6. **Adding Constraints**
To ensure data integrity and prevent issues with duplicate data, a UNIQUE constraint was added to the name column to prevent movies with the same name from being inserted.
The following SQL statement was used to add the constraint:
sql
Copy
Edit
ALTER TABLE films
ADD CONSTRAINT unique_name UNIQUE (name);
This constraint ensures that each movie title is unique in the database.
7. **Updating Data**
After adding the supplementary information, I updated the movie records with the appropriate runtime, category, rating, and box_office_earnings using UPDATE statements.

## Challenges Faced

**Duplicate Entries:** After inserting data, I encountered an issue with duplicate movie records. I solved this by running a DELETE query to remove duplicates while preserving the first entry.

**Apostrophe in Movie Title:** The apostrophe in Monster’s Inc. caused issues when inserting data. This was resolved by properly escaping the apostrophe (Monster\s Inc.) to avoid errors and NULL values in the table.

## Running the Project

### To run this project on your own machine:

**Set Up PostgreSQL:** Install PostgreSQL on your local machine.
**Create a Database:** Create a new database named movies_db.
**Create the films Table:** Run the SQL script to create the films table.
**Insert Data:** Use INSERT statements to add movie records.
**Add Additional Columns:** Use ALTER TABLE to add more attributes for each movie.
**Handle Duplicates:** Use the provided query to remove duplicate records.
**Add Constraints:** Apply constraints to ensure data integrity.

## Conclusion

This project helped me practice and deepen my understanding of SQL, particularly PostgreSQL. I learned how to set up a database locally, create tables, insert and update data, handle duplicates, and apply constraints to ensure the quality of the data. This project is a great starting point for anyone looking to gain hands-on experience with relational databases.

