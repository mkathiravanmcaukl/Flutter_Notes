## Streams in flutter

--> In Dart, Streams are mainly categorized based on how data is delivered and how they behave when mulitple listeners subscribe

### Single-Subscription Streams

  -> A Stream that allows only one listener at a time.

  Behavior:

  -> After a listener subscribes, no other listener can subscribe.

  -> Commonly used for reading data once, like reading a file or an API response

Example:

        Stream<int> singleStream() async*{
            for(int i =1; i <=3; i++)
            {
                await Future.delayed(Duration(seconds: 5));
                yield i;
            }
        }
        void main() async{
          Stream<int> stream = singleStream();
          stream.listen((value){
              print("Listener 1: $value");
          });
        }

 ### Broadcast Streams

--> A stream that allows mulitple listeners to subscribe simultaneously.

Behavior:

-> Multiple widgets or components can listen at the same time.

-> Data events are sent to all active listeners.

Example:

        Stream<int> broadcastStream() async*{
            for(int i =1; i <=3; i++)
            {
                await Future.delayed(Duration(seconds: 5));
                yield i;
            }
        }
        void main() async{
          Stream<int> stream = broadcastStream().asBroadcastStream();
          stream.listen((value) => print("Listener 1: $value"));
          stream.listen((value) => print("Listener 2: $value"));
        }
