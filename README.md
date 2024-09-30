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

[Nhấp vào đây để xem sơ đồ](https://drawsql.app/teams/local-25/diagrams/test-allgrowlabo/embed)

![Mô tả hình ảnh](https://drawsql.app/teams/local-25/diagrams/test-allgrowlabo/embed)
