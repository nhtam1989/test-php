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
    `id` BIGINT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
    `url` VARCHAR(255) NOT NULL,
    `createdAt` DATETIME DEFAULT CURRENT_TIMESTAMP
);
CREATE TABLE `Keywords`(
    `id` BIGINT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
    `url_id` BIGINT NOT NULL,
    `keyword` VARCHAR(100) NOT NULL,
    `createdAt` DATETIME DEFAULT CURRENT_TIMESTAMP,
    CONSTRAINT `keywords_url_id_foreign` FOREIGN KEY (`url_id`) REFERENCES `Url` (`id`)
);

CREATE TABLE `SearchResult`(
    `id` BIGINT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
    `keyword_id` BIGINT NOT NULL,
    `search_engine` VARCHAR(10) NOT NULL COMMENT 'Google/Yahoo',
    `rank` VARCHAR(100) NOT NULL DEFAULT 'out of rank',
    `search_results` BIGINT NOT NULL,
    `createdAt` DATETIME DEFAULT CURRENT_TIMESTAMP,
    CONSTRAINT `search_result_keyword_id_foreign` FOREIGN KEY (`keyword_id`) REFERENCES `Keywords` (`id`)
);
```

## ER Diagram
![Mô tả hình ảnh](link-đến-hình-ảnh)
