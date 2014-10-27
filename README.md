# GoDDD [![wercker status](https://app.wercker.com/status/4622d397d47d1fa763372d7772722603/s/master "wercker status")](https://app.wercker.com/project/bykey/4622d397d47d1fa763372d7772722603)

This is an attempt to port the [DDD Sample App](http://dddsample.sourceforge.net/) to Go. The purpose is to explore how to write idiomatic Go applications using Domain-Driven Design.

I will update this README along the way, as I gain more insights. Therefore, the implementation may be different from the information in this document.

This project is __not__ intended as a tutorial or guide on how to do DDD in Go. It is meant to be a learning experience.

## Design

The purpose of this sample is because I wanted to learn Go and to see how well it can be used with Domain Driven Design. When faced with design challenges, I will lean towards the more idiomatic solution.

[Read more](https://gist.github.com/marcusolsson)

### Other thoughts ...

- How can we use the zero-initialization idiom effectively in DDD? What does a zero-initialized Itinerary mean?
- Concurrency is one area where Go shines, but initial thought is to keep it out of the domain model. This might be interesting if concurrency is a explicit part of the model.

## REST API

The application exposes a REST API.

### Try it out!

If you just want to run the server application on you machine, it is not necessary to clone the repository. 

1. Make sure you have your `$GOPATH` environment set.

    `export GOPATH=$HOME/go`

2. Get the latest version by running:

    `go get -u github.com/marcusolsson/goddd`

    or by cloning the repository to:
    
    `$GOPATH/src/github.com/_username_/goddd`

3. Run it!:

    `$GOPATH/bin/goddd -port 8080` or `go run main.go -port 8080`

### Deploying the application

_Note:_ ~~The `appengine.go` is used to deploy it on Google App Engine. If you want to deploy it to your own project, edit the `app.yaml` to point to your own project.~~ 

_Update:_ I have switched over to Heroku since it feels less intrusive (plus better wercker integration).

__Read more:__

- [Deploy Go applications to App Engine](https://cloud.google.com/appengine/docs/go/)
- [Deploy Go applications to Heroku](http://blog.wercker.com/2013/07/10/deploying-golang-to-heroku.html)


### Cargos

#### GET /cargos
Returns a list of all currently booked cargos.

#### GET /cargos/:id
Returns a cargo with a given tracking ID.

#### POST /cargos
Books a cargo.

| URL Param | Description |
|:----------|:------------|
|origin=[string]|UN locode of the origin|
|destination=[string]|UN locode of the destination|
|arrivalDeadline=[timestamp]|Timestamp of the arrival deadline|

#### POST /cargos/:id/change_destination
Updates the route of a cargo with a new destination.

| URL Param | Description |
|:----------|:------------|
|destination=[string]|UN locode of the destination|

#### GET /cargos/:id/request_routes
Requests the possible routes for a booked cargo.

#### POST /cargos/:id/assign_to_route
Assigns the cargo to a route. Typically one of the routes returned by `/cargos/:id/request_routes`.

### Locations

#### GET /locations
Returns a list of the registered locations.

## Copyright

Copyright © 2014 Marcus Olsson. See [LICENSE](LICENSE) for details.
