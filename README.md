# Project 1: Shared shopping list

<<<<<<< Updated upstream
The application has been deployed to Render at: [shopping-list-project.onrender.com](shopping-list-project.onrender.com)



## 

## 

### 



The name of the application

A brief description of the application

Guidelines for running the application locally (you can assume that participants have docker-compose).






Inside services, there are 2 different implementations of services. 
Application has been first locally developed with arrays instead of database, this has been left there as legacy code or for test running an app, without containers. 
For running arrayServices it is necessary to switch from dbListSvc/dbItemSvc to arrayListSvc/arratItemService inside listService.js and itemService.js. After that app can be run with  deno run --allow-net --allow-read --allow-env app.js .
=======
This application simplifies the creation and maintenance of shopping lists. Users can create new
lists, deactivate lists, add items to lists, and mark items as collected. Basic statistics are
also provided.

### Views

1. **Main Page:**
    - Contains links to the lists page and displays statistics on the number of created
lists and items, including deactivated lists and collected items.

2. **Lists Page:**
    - Allows the creation of new lists, displays all active lists, and provides the option to 
deactivate lists. Clicking on a list name takes the user to the individual list page. 
Includes a navigational link to the main page.

3. **Individual List Page:**
    - Shows all items created for a specific list. Users can add new items, and each item can 
be marked as collected. Includes a navigational link to the lists page.

## Application Structure and Technologies

The application follows a three-tier architecture with Deno as the server, a web browser as the client, 
and PostgreSQL powered by PostgresJS as the database. Additionally, it adheres to a layered architecture 
with views, controllers, services, and a database layer.


The application is placed in the shopping-list directory as root.

### Technology Stack

- **Runtime:** Deno
- **Database Migration:** Flyway
- **End-to-End Tests:** e2e-playwright
- **Database:** PostgreSQL
- **Views:** Eta
- **Styling:** Eta Layout, Bootstrap (v4.5.2), Google Fonts, Font Awesome (v6.1.2)

---

## Accessing the application

The application has been deployed to Render and can be viewed and tested at: [shopping-list-project.onrender.com](shopping-list-project.onrender.com)


### Running the application locally 

The application utilizes Docker for local deployment.Follow these steps:

1. Build the Docker image and start the container: `docker-compose up --build`.
2. Access the application in your web browser: [http://localhost:7777](http://localhost:7777).




### Troubleshooting

There might be a few issues at first with starting a project. Here are few possible reasons and solutions:

#### Different operating systems

This container image was created for Ubuntu 23.04. For different operating system like MacOs, you might need to
use different image for Deno and Playwright. 

- Open Dockerfile in shopping-lists folder and change first line from `FROM denoland/deno:alpine-1.37.0` to `FROM lukechannings/deno:v1.37.0` 
- Open Dockerfile in e2e-playwright folder and change first line from `FROM mcr.microsoft.com/playwright:v1.38.0-focal` to `FROM mcr.microsoft.com/playwright:v1.38.0-vrt-arm64`


#### Container already in use

It is also possible that Docker is clashing with  previously build images and containers. If that's
the case, here are few possible solutions:
- Stop all containers with - `docker compose stop`
- Remove previously build images - `docker image prune -a`
- Change the name of the containers in docker-compose.yml and project.env file. The most common
issue is with database container.

```
// docker-compose.yml

// ...
  database:
    container_name: database-p1       <-- change the name
// ...
```
also
```
project.env

# Database configuration for Flyway (used for database migrations)
FLYWAY_USER=username
FLYWAY_PASSWORD=password
FLYWAY_URL=jdbc:postgresql://database-p1:5432/database     <-- here 

# Database configuration for Deno's PostgreSQL driver
PGUSER=username
PGPASSWORD=password
PGHOST=database-p1                           <-- and here (use the same name)
PGPORT=5432
PGDATABASE=database
```




---
### Array Service

Within the services, two implementations exist. Initially, the application was developed with 
arrays instead of a database. 

```
./services/

├── itemService.js
├── listService.js
│
├── arrayServices
│   ├── itemService.js
│   └── listService.js
│
└── dbServices
    ├── itemService.js
    └── listService.js
```


For running **arrayServices**, switch from `dbListSvc/dbItemSvc` 
to `arrayListSvc/arrayItemService` inside `listService.js` and `itemService.js`.

*listService.js*

```js
/**** Switch between database and array based service ***/
// const implementor = arrayListSvc;
const implementor = dbListSvc;
```

*itemService.js*

```js
/**** Switch between database and array based service ***/
//const implementor = arrayItemSvc;
const implementor = dbItemSvc;
```

To run the app without containers, use: `deno run --allow-net --allow-read --allow-env app.js`.


>>>>>>> Stashed changes
