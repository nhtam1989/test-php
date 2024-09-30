# API Documentation for Keyword Ranking System

## Table of Contents
1. [Database Design](#database-design)
2. [ER Diagram](#er-diagram)
3. [API Endpoints](#api-endpoints)
    - [POST /api/keywords](#post-apikeywords)
    - [GET /api/keywords/results](#get-apikeywordsresults)
4. [API Workflow](#api-workflow)

---

## Database Design
We will design a database with 3 tables :

```sql
CREATE TABLE `Url`(
    `id` INT AUTO_INCREMENT PRIMARY KEY,
    `url` VARCHAR(255) NOT NULL,
    `createdAt` DATETIME DEFAULT CURRENT_TIMESTAMP
);
CREATE TABLE `Keywords`(
    `id` INT AUTO_INCREMENT PRIMARY KEY,
    `url_id` INT NOT NULL,
    `keyword` VARCHAR(100) NOT NULL,
    `createdAt` DATETIME DEFAULT CURRENT_TIMESTAMP,
    CONSTRAINT `keywords_url_id_fk` FOREIGN KEY (`url_id`) REFERENCES `Url` (`id`)
);

CREATE TABLE `SearchResult`(
    `id` INT AUTO_INCREMENT PRIMARY KEY,
    `keyword_id` INT NOT NULL,
    `search_engine` VARCHAR(10) NOT NULL COMMENT 'Google/Yahoo',
    `rank` VARCHAR(100) NOT NULL DEFAULT 'out of rank',
    `search_results` BIGINT NOT NULL,
    `createdAt` DATETIME DEFAULT CURRENT_TIMESTAMP,
    CONSTRAINT `search_result_keyword_id_fk` FOREIGN KEY (`keyword_id`) REFERENCES `Keywords` (`id`)
);
```

## ER Diagram

<!-- [Nhấp vào đây để xem sơ đồ](https://drawsql.app/teams/local-25/diagrams/test-allgrowlabo/embed) -->
![Wireframe Example](diagram_sql.png)


### Example Database

### Url Table
| id | url                      |  createdAt |
|----|-------                   |-------------|
| 1  | https://allgrow-labo.jp  | 2024-09-30 10:07:15 | 

### Keywords Table
| id | url_id | keyword   |  createdAt |
|----|------- |---------  |-------------|
| 1  | 1      | keyword 1 | 2024-09-30 10:07:15 | 
| 2  | 1      | keyword 2 | 2024-09-30 10:07:15 | 

### SearchResult Table
| id | keyword_id | search_engine | rank        | search_results | createdAt |
|----|-------     |-------------  |------       |-------------   |-------------|
| 1  | 1          | Google        | 1           | 500            | 2024-09-30 10:07:15 | 
| 2  | 1          | Yahoo         | 10          | 200            | 2024-09-30 10:07:15 | 
| 3  | 2          | Google        | 6           | 300            | 2024-09-30 10:07:15 | 
| 4  | 2          | Yahoo         | out of rank | 100            | 2024-09-30 10:07:15 | 

--- 

## API Endpoints

### API List
| HTTP Method | Endpoint      | Content-Type |
|-------------|---------------|-------------|
| POST        | /api/v1/search-ranking | Content-Type : application/json | 

Request Body
```json
{
    "url": "https://allgrow-labo.jp",
    "Keywords": ['keyword 1', 'keyword 2']
}
```

Response
```json

{
    "url": "https://allgrow-labo.jp",
    "keywords": [
        {
            "keyword": "keyword 1",
            "google_rank": 1,
            "google_results": 500,
            "yahoo_rank": 10,
            "yahoo_results": 200
        },
        {
            "keyword": "keyword 2",
            "google_rank": 6,
            "google_results": 300,
            "yahoo_rank": "out of rank",
            "yahoo_results": 100
        }
    ]
}

```
