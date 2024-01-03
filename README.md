Install the dependencies by running the following command:

```
npm install
```
In the server.js` file, the Express server uses the MySQL2 library to connect to MySQL and run queries.


The serverСonfig function runs when the server is started. It connects to the MySQL database. It also has some helper functions that are used for CRUD operations.


The `index.html` file in the public folder contains the HTML, CSS, and JavaScript for our DHTMLX Gantt chart. We load the DHTMLX Gantt chart JavaScript and CSS from a CDN and initialize the Gantt chart with the init method.

Run the local dev server using npm start. You’ll see a basic empty Gantt chart.

Now create a `.env` file in the root folder and add the following lines for connecting to the MySQL database that we’ll create:

```
HOST=localhost
PORT=1337
MYSQL_USER=root
PASSWORD=password
DATABASE=dhtmlx
```

Don’t forget to add the root password for your MySQL server.

Setting up a MySQL database locally

Now let’s set up a MySQL database locally.

We’ll install MySQL Server and MySQL Workbench. MySQL Workbench is a MySQL GUI that we’ll use to create a database with tables for the Gantt data and to run queries. Download MySQL Server and MySQL Workbench from the MySQL community downloads page. If you’re using Windows, you can use the MySQL Installer to download the MySQL products. Use the default configurations when configuring MySQL Server and Workbench. Make sure that you configure the MySQL Server to start at system startup for convenience.

Open the MySQL Workbench desktop application. Open the local instance of the MySQL Server that you configured.

We’ll write our MySQL queries in the query tab and execute the queries by pressing the yellow lightning bolt button.

Creating a MySQL database for the DHTMLX data: Adding tables and adding example data

Let’s run some MySQL queries in MySQL Workbench to create, use, and populate a database for our DHTMLX Gantt. Execute the following query to create a database called dhtmlx:


```
CREATE DATABASE dhtmlx;
```

Run the following query so that we set our newly created database for use:

```
USE dhtmlx;
```

Let’s create the two tables that we’ll need for our DHTMLX Gantt chart data: gantt_tasks and gantt_links:

```
CREATE TABLE `gantt_tasks`
(
    `id`         int(11)      NOT NULL AUTO_INCREMENT,
    `text`       varchar(255) NOT NULL,
    `start_date` datetime     NOT NULL,
    `duration`   int(11)      NOT NULL,
    `progress`   float        NOT NULL,
    `parent`     int(11)      NOT NULL,
    `sortorder`  int(11)      NOT NULL,
    PRIMARY KEY (`id`)
);
```


```
CREATE TABLE `gantt_links`
(
    `id`     int(11)    NOT NULL AUTO_INCREMENT,
    `source` int(11)    NOT NULL,
    `target` int(11)    NOT NULL,
    `type`   varchar(1) NOT NULL,
    PRIMARY KEY (`id`)
);
```

Now add some example tasks data to the gantt_tasks table:

```
INSERT INTO `gantt_tasks` (id, text, start_date, duration, progress, parent, sortorder)
VALUES (1, 'Project #1', '2022-11-05 00:00:00', 10, 0.8, 0, 11);
INSERT INTO `gantt_tasks` (id, text, start_date, duration, progress, parent, sortorder)
VALUES (2, 'Task #1', '2022-11-05 00:00:00', 6, 0.5, 1, 7);
INSERT INTO `gantt_tasks` (id, text, start_date, duration, progress, parent, sortorder)
VALUES (3, 'Task #2', '2022-11-07 00:00:00', 8, 0.7, 1, 9);
INSERT INTO `gantt_tasks` (id, text, start_date, duration, progress, parent, sortorder)
VALUES (4, 'Task #3', '2022-11-13 00:00:00', 2, 0, 1, 10);
INSERT INTO `gantt_tasks` (id, text, start_date, duration, progress, parent, sortorder)
VALUES (5, 'Task #1.1', '2022-11-05 00:00:00', 3, 0.34, 2, 3);
INSERT INTO `gantt_tasks` (id, text, start_date, duration, progress, parent, sortorder)
VALUES (6, 'Task #1.2', '2022-11-08 00:00:00', 3, 0.5, 2, 11);
INSERT INTO `gantt_tasks` (id, text, start_date, duration, progress, parent, sortorder)
VALUES (7, 'Task #2.1', '2022-11-07 00:00:00', 3, 0.2, 3, 11);
INSERT INTO `gantt_tasks` (id, text, start_date, duration, progress, parent, sortorder)
VALUES (8, 'Task #2.2', '2022-11-10 00:00:00', 5, 0.9, 3, 11);
```

```
INSERT INTO `gantt_links` (id, source, target, type)
VALUES (6, 5, 6, '0');
INSERT INTO `gantt_links` (id, source, target, type)
VALUES (7, 7, 8, '0');
```

You’ll be able to view the example tasks data by running the following query:

```
SELECT * FROM gantt_tasks;
```
<img width="1190" alt="CleanShot 2024-01-03 at 12 08 19@2x" src="https://github.com/bryntum/dhtmlx-to-bryntum-gantt-starter/assets/37709578/ff90d10f-a04f-4673-9695-04504a25c825">

and the example link data by running the following query:

```
SELECT * FROM gantt_links;
```
<img width="452" alt="CleanShot 2024-01-03 at 12 10 23@2x" src="https://github.com/bryntum/dhtmlx-to-bryntum-gantt-starter/assets/37709578/2d0d3b0e-8c04-42c4-90b6-08d1a660e08c">

