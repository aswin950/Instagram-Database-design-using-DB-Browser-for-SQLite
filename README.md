# Instagram-Database-design-using-DB-Browser-for-SQLite
Instagram Database design using DB Browser for SQLite.

Requirements:

Download DB Browser for SQLite - https://sqlitebrowser.org/

Design ER Diagrams using this website https://draw.io

# Project Overview
Instagram provides mobile phone-based photography sharing services. It allows its users to take photos, add effects, and share content online and over various social networks. It was founded by Stanford graduates Kevin Systrom and Mike Krieger and is now owned by Facebook. The name Instagram is a combination of “instant camera” and “telegram”.
As of June 2020, Instagram had 1 billion monthly users. Prior to this, Instagram had 800 million active users as of September 2017.
# Introduction
•	I have chosen Instagram app as the project topic because everyone uploads and shares images with their friends and family and follows each other.  
•	Instagram is one of the most popular social network applications worldwide.
•	As of January 2021, India and the United States were the two countries with the most Instagram users with 140 million users.
•	Past research has found that photos with people’s face receive more likes and comments.  
•	Ongoing research continues to find how media content on the platform affects user engagement.  
•	Link to the application: www.instagram.com
# Use-case
•	Users Signup and log in using the credentials which you gave during sign up.
•	Add your name, and description and choose the type of account that is required.  
•	Search the profile you wanted to lookup by using their username.
•	Instagram users can continue using it even without uploading any media content.  

I have used Instagram in the past to see the pictures taken by professional photographers. I chose Instagram as my project because I like seeing the beautiful pictures of our planet in this application.
# Business Analysis

•	Instagram Users

Once the Instagram account is signed in and the users start to use the application it can recommend users with whom to follow. Once a user starts to follow other users on Instagram, their new posts will appear in the feed tab. Users can also search for users whom they want to follow. Since Instagram is now owned by Facebook, it will suggest to follow your friends from Facebook to follow them on Instagram.

•	Role of Instagram Analysts

1.	Keep track of active and inactive users.
2.	Keep track of user engagement with the content.
3.	Keep track of comments, hashtags, likes.
4.	Giving the Instagram users an option to connect with their Facebook account.
5.	Showings relevant advertisement to users that they are likely to engage.
6.	Keep track of words that are reported.

# Business Rules
•	Each USER can upload many IMAGES.
•	Each USER likes many IMAGES.
•	Every USER should have a different USERNAME.
•	One USER can write many COMMENTS.
•	One IMAGE can have many LIKES and
•	One IMAGE can have many COMMENTS.

# Relationship Table

<img width="562" alt="image" src="https://user-images.githubusercontent.com/61600236/152581977-212ca683-21a5-4a7e-8bd8-b952a1e22bcd.png">

# Entity Relationship Diagram

<img width="540" alt="image" src="https://user-images.githubusercontent.com/61600236/152582129-4bbaeb2a-0811-4e82-9f94-b20ba62b40ed.png">

# Creating tables for database - Creating USERS table

CREATE TABLE "USERS" (
"id" INTEGER.
"username" VARCHAR(30) NOT NULL UNIQUE,
"password"
VARCHAR(40) NOT NULL,
"created time"
DATETIME DEFAULT CURRENT TIMESTAMP,
PRIMARY KEY('id" AUTOINCREMENT)
);

<img width="409" alt="image" src="https://user-images.githubusercontent.com/61600236/152582829-6224ac37-b07f-4ab2-b46c-c0ba530d48cb.png">

INSERTING VALUES TO USERS TABLE with the below code:
INSERT INTO USERS(username, password) VALUES ('newentry','enterednow'). 

The above query inserts username and password to the USERS table and id and created time appear automatically as we declared in the create table statement.

<img width="378" alt="image" src="https://user-images.githubusercontent.com/61600236/152582959-dba22eb1-77a7-4626-857e-c0e16d91178a.png">

Similar to the above create table statement we can create and insert values to the tables in the database.

# Creating IMAGE table
CREATE TABLE "IMAGE" (
"id" INTEGER,
"image_ur]" VARCHAR(150) NOT NULL,
"FK user id" INTEGER NOT NULL,
"created time" DATETIME DEFAULT CURRENT TIMESTAMP.
PRIMARY KEY('id" AUTOINCREMENT),
FOREIGN KEY("FK_user _id") REFERENCES "USERS" ("id")
);

<img width="404" alt="image" src="https://user-images.githubusercontent.com/61600236/152583224-d6db5d62-bb66-4d80-8bbc-085062cc01d7.png">

Query to insert values to IMAGE table
INSERT INTO IMAGE(image_url, FK_user_id) VALUES ('https://twitter.com/klrahul11/photo', 7)

<img width="536" alt="image" src="https://user-images.githubusercontent.com/61600236/152583316-a43c81f8-d7fa-44ee-ab4b-d11644eb8653.png">

The above query inserts the mentioned values into the IMAGE table of the database. Foreign keys are created in such a way that helps us in extracting the data from the database. Similarly other tables can also be constructed with the use of foreign keys with the help of the Entity Relationship Diagram. And insert statement is used to insert values to the tables with necessary changes according to the table we insert.

# Retrieving Information from Database
-- display all the image url with username 'hardikpandya'
SELECT username,image _url
FROM USERS
LEFT JOIN IMAGE
ON USERS.id = IMAGE.FK user id
WHERE username = 'hardikpandya'

<img width="397" alt="image" src="https://user-images.githubusercontent.com/61600236/152583484-7ad247be-f0db-4ac8-ad97-230972101b86.png">

The above query displays all the image URLs of the user with the username hardikpandya. Similarly, when the username hardikpandya is replaced with another username, all their image URL will be displayed. This also proves one of the business rules where one user can have many images. The above query uses a JOIN statement and combines the USERS table and IMAGE table. The information extracted from the database can be used for analysis and metrics.

# Analytics and Metrics - Most Liked image with username and image_url

- most liked image with username and image_url
SELECI username,IMAGE.id as IMAGE_ID,IMAGE.image_url,
COUNT(*) AS TOTAL
FROM IMAGE
JOIN LIKES
ON LIKES.FK image_id =IMAGE.id
JOIN USERS
ON IMAGE.FK user id = USERS.id
GROUP BY IMAGE.id
ORDER BY total DESC
LIMIT l:

<img width="433" alt="image" src="https://user-images.githubusercontent.com/61600236/152583595-822d59ef-c7e2-4e18-80c9-e30881e06a9c.png">

The above query displays the image with the greatest number of likes along with the id of the image, image url and username of the user who uploaded the image. The above query uses a JOIN statement to combine the LIKES table, IMAGE table and USERS table. I have used the GROUP BY, ORDER BY and LIMIT statement to get the required output from the database. This query explains one of the business rules of the project which is one image can have many likes.

# Analytics and Metrics - Instagram users who liked all images
- users who liked all images
SELECT USERS.id as USER ID,username,
Count(*) AS num of likes
FROM USERS
JOIN LIKES
ON USERS.id = LIKES.FK user id
GROUP BY LIKES.FK user id
HAVING num of likes = (SELECT Count(*)
FROM IMAGE);

<img width="433" alt="image" src="https://user-images.githubusercontent.com/61600236/152583760-2de80113-1a44-4720-a47a-d00662e2cc2d.png">

The above query helps us in finding the user who liked every image in the database along with their user id and the number of likes the user has made. This defines one of the business rules which is one user can like many images. In this query, I have combined the USERS table and LIKES table and used the GROUP by statement in order to find the number of likes.

# Analytics and Metrics - Instagram users with no images in their profile
- select users with no images
SELECT username as USERNAME. USERS.id as USER
FROM USERS
LEFT JOIN IMAGE
ON USERS.id = IMAGE.FK user id
WHERE IMAGE.id IS NULL

<img width="408" alt="image" src="https://user-images.githubusercontent.com/61600236/152584562-12c31eaa-f0eb-4819-b19b-d58433b5bf29.png">

Although our business rules state one user can have images, it is not mandatory for a user to have images in their profile. This can be mentioned as one of the features of Instagram. Users of Instagram may continue using Instagram without uploading any images. The above select statement displays all the USERS who have not uploaded any images along with their user id. LEFT JOIN statement is used to combine the USERS table and IMAGE table and ORDER BY is used to display users in ascending order.

# Instagram Architecture

Instagram works with 3 tier architectures to have safety an display all images which are directly retrieved from the Instagram Data center. Although Instagram used AWS as cloud storage, moving forward they made their own data center to store images and videos. Below are the 3 layer and the advantages of 3 tier architecture.


• Presentation Layer: This is top-level in a three-tier architecture. It is commonly referred to as Graphical User Interface. In this case, for Instagram front-end mobile application and a website. This is where the users interact and input the data.
•	Business/ Service Layer: The input from the user is sent to this layer and the data is uploaded to the storage platform. The input data is stored in the database according to the business rules.
•	Data Layer: NoSQL Database Server.
# Advantages of 3 tier Architecture
•	Security: Since there is no direct interaction between client & server, we can restrict unauthorized access.
•	Integrity: As we have a Service layer between client and server-side data corruption could be removed.

# Instagram Metrics
•	Instagram metrics tell us about the engagement with the photos and the users who engage with them.
•	User engagement with likes, Comments, Profile Clicks for advertisers.
•	Follower Growth: Follower Growth after promoting with advertisement. This will show the follower count before and after the promotion of the Instagram profile.
•	Instagram users can add up to 30 hashtags on each post.
•	When relevant hashtags are used, it helps to keep the engagement in check.

# Privacy & Security Features

The following are the some of the important privacy & security features of Instagram.
•	Private Account.
•	Block Accounts.
•	Block Commenters.
•	Report Posts.
•	Report Accounts.
•	Remove a follower.
•	Two- Factor Authentication.
•	Download your data, a copy of your comments, posts, and messages.
•	Delete posts, remove or archive your posts and it will be not shown in your profile.
•	Instagram Security team should not a user by email when it is logged in a new device and in a new location.
Link: about.instagram.com/community/safety


# Future Ideas & Lessons Learnt:
•	Created complex queries to retrieve information from the database using JOINs.
•	Learnt about the architecture design of Instagram.
•	Learnt about the Metrics along with the security and privacy features of the application.
•	Add actual pictures to the server in the current database.
•	With the help of a new domain and a server space make a website that can do the functions of this database with a better database design.

# References
1.)	Constine, J. (2018, June 20). Instagram hits 1 billion monthly users, up FROM 800M in September. Retrieved from techcrunch.com/2018/06/20/instagram-1-billion-users/

2.)	Blogger, C. (2020, May 07). Three tier system architecture for business applications. Retrieved from codeauthority.com/Blog/Entry/three-tier-architecture
