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


## Difference between Future.value() and Future.sync()

--> Future.value() creates a future that completes immediately with the given value, regardless of whether the value is available synchronously or asynchronously.

--> Future.sync() executes a function synchronously and returns a future. If the function returns a value, the future completes with that value. If the function throws an error, the future completes with that error.
    If the function returns a future, Future.sync() waits for that future to complete.


Example:

                Future<UserProfile> getUserProfile() {
                  if (cache.hasProfile) {
                    // Return cached profile as a future
                    return Future.value(cache.profile);
                  }
                  // Otherwise, fetch from network
                  return fetchProfileFromNetwork();
                }


                Future<UserProfile> parseProfile(String jsonString) {
                  return Future.sync(() {
                    // This might throw if JSON is invalid
                    return UserProfile.fromJson(jsonDecode(jsonString));
                  });
                }

