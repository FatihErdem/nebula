
# The Nebula Project

This project is developed for Malwarebytes Nebula project.

This project contains 3 main components.

 1. Nebula-API
 2. Nebula-ReviewConsumer
 3. Nebula-Notification

## Nebula-API
This project is responsible for REST API. [Repository link](https://github.com/FatihErdem/nebula-api)

You can create review via HTTP POST request. After review creation it sends created review to `Nebula-ReviewConsumer` for process review. It puts the object to RabbitMQ queue. 

After status finalizing it gets objects from review update queue and put email send queue for sending email.

## Nebula-ReviewConsumer
This project is responsible for process created reviews.  [Repository link](https://github.com/FatihErdem/nebula-consumer)

It gets objects from review created queue and process for inappropriate words and decide status of the review. This status can be `APPROVED` or `DECLINE`. After finalizing the review status it puts the review status to RabbitMQ queue.

## Nebula-Notification
This projects is responsible for sending email. [Repository link](https://github.com/FatihErdem/nebula-notification)

It gets objects from email queue and send email.

### Project Structure

![Nebula Architecture](https://i.imgur.com/QME60HB.jpg?1)

# How to Install

## Prerequisites
 1. Docker
 2. Java 8
 3. Postman

## How to Install

 1. You should run `docker-compose up` command in cloned directory. After download and startup Docker containers execute following commands.
 2. `java -jar api.jar > /dev/null 2>&1 &`
 3. `java -jar reviewconsumer.jar > /dev/null 2>&1 &`
 4. `java -jar notification.jar > /dev/null 2>&1 &`

After these you are ready to go. You can use below Postman Collection export for tryouts.

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/6fc34eeabab2ca8d87da)

## Queries
You can query inserted or updated reviews with:
`SELECT * FROM production.productreview WHERE productreviewid = :id`

