[![Build Status](https://travis-ci.org/mapuri/serf-event.svg?branch=master)](https://travis-ci.org/mapuri/serf-event)

# serf-event
A golang lib for writing serf event generators and handlers.

## Goal
- Have a more formal (verifiable) way of defining and generating serf events in **Go**!
- eliminate some/most boilerplate code for getting a serf event handler logic ready in **Go**!

## Status
Being  implementated

## Requirements
- serf agent should be running (`-event-handlers` flag shall not be specified for handler process written using this library)

## Writing an event handler

The event routers supports regex based handler match with ability  for cretaing SubHandler, to inderit common path-prefix

```
import serf-event

func main() {
se = serf-event.NewHandler()
se.AddHandler("foo", fooHandler())
subSe = se.NewSubHanddler("bar/")
subSe.AddHandler("event1", barEvent1Handler())
...
...

# serf native events are supported
se.AddJoinHandler(joinHandler())
se.AddLeaveHandler(joinHandler())
...
...

# serf queries
se.AddResponder("", query1Responder())

se.Serve()
}
```

## Writing a event generator

Event generators can be useful for code that is able to consume the events generated by it's own logic and hence can be useful for sharing event structures, without having to explicitly import serf client code.

```
func main() {
se = serf-event.NewGenerator()

err = se.PostEvent("", bytes)

resp, err  = se.PostQuery("", bytes)

}
```
