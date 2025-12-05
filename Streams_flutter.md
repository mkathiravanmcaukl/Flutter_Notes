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

 ### Difference between Stream.listen() and await for loop in flutter?

 --> In Flutter (Dart), both Stream.listen() and await for loops are used to handle events from a Stream, but they differ in usage and behavior:

 #### Stream.listen()

--> Registers a callback that is called every time the stream emits a value. The callback is non-blocking and runs asynchronously. You can cancel the subscription, pause, or resume it.Useful for event-driven code, e.g.,      UI updates, where you want to react to each event as it arrives.

Example:

        Stream<int> numberStream = Stream.periodic(Duration(seconds: 1), (count) => count);
        
        void main() {
          numberStream.listen((number) {
            print('Received number: $number');
          });
        }

  #### await for loop

  --> Used inside an async function to process each event sequentially. The loop waits for each event before continuing, making it easier to write sequential logic. You cannot pause or cancel the loop directly (but you can break out of it). Useful for processing streams where you need to handle each event in order, possibly with async/await logic.

Example:

        Stream<int> numberStream = Stream.periodic(Duration(seconds: 1), (count) => count);
        
        Future<void> processNumbers() async {
          await for (var number in numberStream) {
            print('Processing number: $number');
            // You can use await here for async operations
          }
        }
        
        void main() {
          processNumbers();
        }
