# DB_labs Atrashonok Yulia 153501
# Blog
# Functional requirements
1. User Registration and Authentication
2. User Profile Management
3. Post CRUD for User and Admin
4. Comments create for User
5. Likes CRUD for User
6. Users should be able to follow other users.
7. Users should be able to subscribe to different payment plans offered by the system.
8. User actions logging
# Use cases
1. Admin:
   - Manage Subscription Plans:
     - Create new subscription plans.
     - Update or delete existing subscription plans.
   - View and moderate comments on all blog posts.
2. Authorized User:
   - Create an Account:
     - Register as a new user.
   - Manage Profile:
     - Update personal information.
     - View account details.
   - Manage Posts:
     - Create a new blog post.
     - Edit or delete existing blog posts.
     - View and moderate comments on their blog posts.
   - Interact with Posts:
     - Like or unlike a blog post.
     - Comment on blog posts
   - Follow other users.
   - Subscribe to a payment plan.
3. Unauthorized User:
   - Browse Posts:
     - View a list of blog posts.
     - Read the content of a blog post.
     - View comments on a blog post.
   - Search and Filter Posts
   - View Advertisements
   - Sign Up
   - Login
# Enities
### User 
  * user_id INT PRIMARY KEY NOT NULL
  * username VARCHAR(255) NOT NULL
  * email VARCHAR(255) NOT NULL UNIQUE
  * password VARCHAR(255) NOT NULL
  * created_at TIMESTAMP NOT NULL
  * last_login TIMESTAMP NOT NULL
  * FOREIGN KEY (plan_id) REFERENCES Subscription_Plan(plan_id) NOT NULL

### Post 
  * post_id INT PRIMARY KEY NOT NULL
  * title VARCHAR(255) NOT NULL
  * content TEXT NOT NULL
  * created_at TIMESTAMP NOT NULL
  * updated_at TIMESTAMP NOT NULL
  * FOREIGN KEY (user_id) REFERENCES User(user_id) NOT NULL
  
### Profile (One-to-one with User)
  * profile_id INT PRIMARY KEY NOT NULL
  * bio TEXT
  * avatar_url VARCHAR(255) NOT NULL
  * FOREIGN KEY (user_id) REFERENCES User(user_id) NOT NULL

### Comment 
  * comment_id INT PRIMARY KEY NOT NULL
  * content TEXT NOT NULL
  * created_at TIMESTAMP NOT NULL
  * updated_at TIMESTAMP NOT NULL
  * FOREIGN KEY (user_id) REFERENCES User(user_id) NOT NULL
  * FOREIGN KEY (post_id) REFERENCES Post(post_id) NOT NULL

### Tag 
  * tag_id INT PRIMARY KEY NOT NULL
  * name VARCHAR(255) NOT NULL UNIQUE

### Like 
  * like_id INT PRIMARY KEY NOT NULL
  * FOREIGN KEY (user_id) REFERENCES User(user_id) NOT NULL
  * FOREIGN KEY (post_id) REFERENCES Post(post_id) NOT NULL

### Bookmark 
  * bookmark_id INT PRIMARY KEY NOT NULL
  * note TEXT
  * FOREIGN KEY (user_id) REFERENCES User(user_id) NOT NULL
  * FOREIGN KEY (post_id) REFERENCES Post(post_id) NOT NULL

### Follow
  * follow_id INT PRIMARY KEY NOT NULL
  * subscribed_at TIMESTAMP NOT NULL
  * FOREIGN KEY (follower_id) REFERENCES User(user_id) NOT NULL
  * FOREIGN KEY (following_id) REFERENCES User(user_id) NOT NULL

### Advertisement 
  * ad_id INT PRIMARY KEY NOT NULL
  * title VARCHAR(255) NOT NULL UNIQUE
  * content TEXT NOT NULL
  * image_url VARCHAR(255) 
  * start_date DATE NOT NULL
  * end_date DATE  NOT NULL

### Subscription_Plan 
  * plan_id INT PRIMARY KEY  NOT NULL
  * name VARCHAR(255)  NOT NULL UNIQUE
  * description TEXT  NOT NULL
  * price DECIMAL(10, 2)  NOT NULL
  * duration INT  NOT NULL

### Payment 
  * payment_id INT PRIMARY KEY NOT NULL
  * payment_date DATE  NOT NULL
  * FOREIGN KEY (user_id) REFERENCES User(user_id) NOT NULL
  * FOREIGN KEY (plan_id) REFERENCES Subscription_Plan(plan_id) NOT NULL
