
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

## How to Install

## Prerequisites
 1. Docker
 2. Java 8
 3. Postman
