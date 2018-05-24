# TvMaze-Scrapper Api
API based on microservices architecture.
Project consist of three independent microservices:
- Cast
- MazePage
- Shows

## Every microservice has his own API.
* Cast: `/casts?ids=[showIds]`
* MazePage: `/shows?page=[pageNumber]&from=[from]&to=[to]` where "from" and "to" optional parameters
* Shows: `/shows?page=[pageNumber]` Every page consists of 10 items

As mentioned every microservice completely independent. Cast and MazePage used Microsoft SQL Server, but we can set up for every single microservice his own technology stack (e.x. We can cache objects in [Redis](https://github.com/antirez/redis) or whatever you need)

## Technology
* [Nancy](https://github.com/NancyFx/Nancy) - The web framework used
* [Polly](https://github.com/App-vNext/Polly) - library to apply policies such as Retry, Circuit Breaker, Timeout etc.
* [Dapper](https://github.com/StackExchange/Dapper) - lightweight library which extends IDbConnection interface. It's very simple framework and it's just for microservices.
* [Asp .NET Core](https://github.com/aspnet/Home) - framework for building internet connected applications

## Requirements for the system
* REST API gives access to shows and cast information
* Some data cached in storage
* Paginating available
* List of the cast has ordering

## Summary
All services was published to windows virtual machine which located in Azure.
Right now user have access only for Shows microservice which communicate with two others.

To retrieve shows user can make request to the following URLs:
* http://tvmazescrapper.westeurope.cloudapp.azure.com/shows
* http://tvmazescrapper.westeurope.cloudapp.azure.com/shows?page=1
