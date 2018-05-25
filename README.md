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
Right now user have access to all of them using the following API:
* To retrieve shows user can make request to the following URLs:
  * http://tvmazescrapper.westeurope.cloudapp.azure.com/shows
  * http://tvmazescrapper.westeurope.cloudapp.azure.com/shows?page=1
* To retrieve just shows from **shows** microservice you can make following request:
  * http://tvmazescrapper.westeurope.cloudapp.azure.com:65373/shows?page=0&from=10&to=20
* To retrieve **cast** from show or shows you can make next request:
  * http://tvmazescrapper.westeurope.cloudapp.azure.com:52348/casts?ids=[815,816,819] where 815,816,817 show id
