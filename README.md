# Wellness Tracker

## Project Summary
Our project entails creating a database application for fitness tracking that will help users monitor and improve their fitness and health. Users of the website will be able to set and track fitness goals as well as gain insights into their fitness advancement.

## Project Description
### Objectives
Our objective is to develop a database application for fitness tracking that will enable users to quickly perform several operations on their fitness data. Users will be able to add new fitness metrics, monitor their development over time, edit already-entered data, and remove records as necessary. By utilizing the Fitbit dataset, we hope to give users accurate and thorough information about their fitness routines, empowering them to make wise decisions about their health and wellbeing. The application will also offer tips for enhancing fitness levels based on the users' data and goals.

### Usefulness
Our fitness tracking database will be helpful for anyone interested in monitoring their fitness progress and enhancing their general health and wellness. Users of the database will be able to track their daily step total, calories burned, walking distance, and other metrics, enabling them to set and meet fitness objectives. Our database will give users precise and in-depth information about their fitness routines by utilizing data from Fitbit fitness trackers, empowering them to decide on their health and wellness routines.

Users will benefit from our database's interactive interface because it will allow them to easily view and analyze their data. Users will be able to track and visualize their fitness progress over time, giving them actionable insights and advice to improve their wellness routine.

### Dataset
This dataset was created by participants in a distributed survey via Amazon Mechanical Turk between December 3, 2016, and December 5, 2016. Fitbit fitness trackers collect a variety of fitness metrics, including step count, calories burned, total distance walked, and many more. Thirty eligible Fitbit users agreed to the submission of their personal tracker data for these metrics and many more. This data set's primary goal is to develop a better understanding of Fitbit users' exercise routines.

Data set link: [Fitbit Fitness Tracker Data](https://www.kaggle.com/datasets/arashnic/fitbit)

We will be using `dailyActivity_merged.csv` from this Kaggle Fitbit Fitness Tracker dataset.

## Conceptual Diagram/Schema
The database is designed to capture and store a user's daily health and fitness data such as activity, sleep, and weight. The main table, `dailyActivity`, is split into several tables to understand the data better:

- `daily_calories`: Tracks a user's daily calorie intake.
- `steps`: Records the total number of steps taken by a user on a given day.
- `minutes`: Records a user's active minutes on a given day, broken down by type (very active, fairly active, lightly active, sedentary).
- `distances`: Records the distance traveled by a user on a given day, broken down by type (total, tracker, logged activities, very active, moderately active, lightly active, sedentary).
- `sleeping`: Stores a user's sleep data such as total sleep records, total minutes asleep, and total time spent in bed.
- `weight_log`: Contains data related to weight tracking, including columns for ID, Date, WeightKg, WeightPounds, Fat, BMI, and IsManualReport.

All entities have a primary key made up of the combination of `Id` and `ActivityDate` to establish relationships between them.

## Database
### Constraints
Several constraints exist in the database to ensure data integrity. The primary keys in the tables ensure uniqueness. Foreign key constraints reference the `daily_calories` table in the `steps`, `minutes`, and `distances` tables to ensure consistency. All columns in the tables are set to NOT NULL.

### Views, Functions, and Procedures
We have planned to use views and functions for tasks such as finding average steps, average distance, average sleep taken, and average calories for each person to gain more insights from the visualizations. More views and functions will be created based on the application requirements.

### Code
The SQL file attached contains all of the codes for creating the database and building queries.

## Web App Architecture
### Data Storage
Currently, our data is stored stand-alone, and later we will migrate to the cloud.

### Backend Languages
To build the backend, we will be using R and SQL, as we are developing our entire application in RShiny.

### Database Access
We are using a Postgres database, and we are connecting that to R using the following packages:
```R
install.packages("RPostgreSQL")
install.packages("RPostgres")
library(DBI)

db <- "postgres"
db_host <- "localhost"
db_port <- "5432"
db_user <- "<your_user>"
db_pass <- "<your_password>"

conn <- dbConnect(
  RPostgres::Postgres(),
  dbname = db,
  host = db_host,
  port = db_port,
  user = db_user,
  password = db_pass
)

dbGetQuery(conn, "SELECT * FROM dailyCalories_merged LIMIT 5")
```

Only the fitness specialist (Admin of our application) has the ability to delete records; no other users have this capability. Users can only perform create, read, and update operations on their own data.

## Front-end Layout
For the front end, we will be using R Shiny.

## Deployment
Our application is deployed on the shiny server.

## Interactivity
Users can log in, view insights on their fitness goals, update and add new activity details, and register for new accounts.

## Web App Layout
### Initial Layout
When a user first visits our website, they will see the Login page with fields for their email address and password and a navigation menu.

### Menu Panel
The menu panel is located in the upper right corner and includes navigation buttons such as Home, Login, Your Fitness Insights, Update Details, and Logout.

### Pages/Tabs
We have five pages: Home, Login, Your Fitness Insights, Update Details, and Register. We will be using tabs to switch between them.

### Color Schema
For now, we are using the default schema provided by RShiny.

### Page Content
- **Home**: Provides basic information about the application.
- **Login**: Contains a form for email ID and password.
- **Register**: Fields for full name, email ID, password, and confirm password.
- **Your Insights**: Displays various insights on user data through visualizations.
- **Update Details**: Displays user data and allows CRUD operations.
- **Logout**: Logs the user out of the session.



## References
- [Fitbit Fitness Tracker Data](https://www.kaggle.com/datasets/arashnic/fitbit)

