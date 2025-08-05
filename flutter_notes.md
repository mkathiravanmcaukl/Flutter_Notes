## Difference between async/await, isolates and compute method

Here’s a concise explanation of the differences between `async/await`, isolates, and the `compute` method in Flutter:

### 1. **Async/Await**:
- **Purpose**: Used for asynchronous programming to handle tasks like I/O operations (e.g., API calls, file reading).
- **Execution**: Runs on the **main thread** (UI thread).
- **Use Case**: For non-blocking tasks that don’t require heavy computation.
- **Example**:
  ```dart
  Future<void> fetchData() async {
    final data = await fetchFromApi();
    print(data);
  }
  ```

### 2. **Isolates**:
- **Purpose**: Used for heavy computational tasks to avoid blocking the main thread.
- **Execution**: Runs on a **separate thread** (isolate) with its own memory.
- **Use Case**: For CPU-intensive tasks like data processing or image manipulation.
- **Example**:
  ```dart
  import 'dart:isolate';

  void heavyTask(SendPort sendPort) {
    sendPort.send('Task Complete');
  }

  Future<void> runIsolate() async {
    final receivePort = ReceivePort();
    await Isolate.spawn(heavyTask, receivePort.sendPort);
    print(await receivePort.first);
  }
  ```

### 3. **Compute Method**:
- **Purpose**: A helper function to run a function in a separate isolate.
- **Execution**: Simplifies isolate usage by managing communication and setup.
- **Use Case**: For lightweight, one-off computational tasks.
- **Example**:
  ```dart
  import 'package:flutter/foundation.dart';

  int heavyComputation(int value) {
    return value * 2;
  }

  Future<void> runCompute() async {
    final result = await compute(heavyComputation, 10);
    print(result); // Output: 20
  }
  ```

### Key Differences:
| Feature            | Async/Await         | Isolates            | Compute Method       |
|---------------------|---------------------|---------------------|----------------------|
| **Thread**          | Main thread         | Separate thread     | Separate thread      |
| **Memory**          | Shared              | Isolated            | Isolated             |
| **Complexity**      | Simple              | Complex             | Simplified           |
| **Use Case**        | I/O tasks           | Heavy computation   | Lightweight computation |



## 3 ways to create a singleton class in flutter

  1. Factory constructor

        class Singleton{
          Singleton._internal()
          static final Singleton _singleton = Singleton._internal
    
          factory Singleton(){
            return _singleton
          }
        }

 2. Static field with getter

      class Singleton{
          Singleton._internal()
          static final Singleton _singleton = Singleton._internal
          static Singleton get singleton => _singleton
        }
     

3. Static field

       class Singleton{
          Singleton._internal()
          static final Singleton singleton = Singleton._internal
        }
