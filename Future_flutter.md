## What is Future.any() and how does it work?

--> Future.any() takes a list of Futures and returns the result of the first feature that complete successfully.

--> If all Futures fail, it returns an error.

Example:

        import 'dart:async';
        
        Future<String> fetchFromCache() async {
          await Future.delayed(Duration(seconds: 2));
          return 'User from cache';
        }
        
        Future<String> fetchFromLocalDb() async {
          await Future.delayed(Duration(seconds: 1));
          return 'User from local DB';
        }
        
        Future<String> fetchFromNetwork() async {
          await Future.delayed(Duration(seconds: 3));
          return 'User from network';
        }
        
        void main() async {
          String user = await Future.any([
            fetchFromCache(),
            fetchFromLocalDb(),
            fetchFromNetwork(),
          ]);
          print(user); // Output: User from local DB
        }


## What is Future.microtask() and when would you use it?

--> Future.microtask() schedules a function to run as soon as possible after the current synchronous code completes, before any event queue tasks.

Example:

                import 'dart:async';
                
                void main() {
                  print('Start');
                
                  Future.microtask(() {
                    print('Microtask executed');
                  });
                
                  print('End');
                }
