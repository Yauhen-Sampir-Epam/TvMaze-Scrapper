# TvMaze-Scrapper Api
API based on microservices architecture.
Project consist of three independent microservices:
- Cast
- MazePage
- Shows

## Microservices overview
* Cast: `/casts?ids=[showIds]`
* MazePage: `/shows?page=[pageNumber]&from=[from]&to=[to]` where "from" and "to" optional parameters
* Shows: `/shows?page=[pageNumber]` Every page consists of 10 items

Every microservice completely independent. Cast and MazePage used Microsoft SQL Server, but we can set up for every single microservice his own technology stack (e.x. For better cache performance we can use [Redis](https://github.com/antirez/redis) or whatever decided)

## Technology
* [Nancy](https://github.com/NancyFx/Nancy) - web framework for microservices
* [Polly](https://github.com/App-vNext/Polly) - lightweight library to improve fault tolerance when interacting with other microservices
* [Dapper](https://github.com/StackExchange/Dapper) - lightweight library which extends IDbConnection interface
* [ASP .NET Core](https://github.com/aspnet/Home) - framework for building internet connected applications

## System requirements
* REST API gives access to shows and cast information
* Some data cached in storage
* Paginating available
* List of the cast ordering by birthday

## Summary
All services was published to windows virtual machine which located in Azure.
Right now user have access only for **Shows** microservice which communicate with others (MazePage and Cast).

To retrieve shows user can make request to the following URLs:
* http://tvmazescrapper.westeurope.cloudapp.azure.com/shows
* http://tvmazescrapper.westeurope.cloudapp.azure.com/shows?page=1
