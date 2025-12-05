## Streams in flutter

--> In Dart, Streams are mainly categorized based on how data is delivered and how they behave when mulitple listeners subscribe

### Single-Subscription Streams

  -> A Stream that allows only one listener at a time.

  Behavior:

  -> After a listener subscribes, no other listener can subscribe.

  -> Commonly used for reading data once, like reading a file or an API response
