## 1. What is the use of AutomaticKeepAliveClientMixin for listview items in flutter

AutomaticKeepAliveClientMixin is used in Flutter to keep a widget's state alive when it is scrolled out of view in a ListView (or other scrollable widgets). 
By default, Flutter may dispose of list items that are not visible to save resources. If you want to preserve the state (e.g., form input, scroll position) of each item, use this mixin.

How it works:

Add AutomaticKeepAliveClientMixin to your list item widget's state class.

Override wantKeepAlive to return true.

Ex: 

          class MyListItem extends StatefulWidget {
          @override
          _MyListItemState createState() => _MyListItemState();
        }
        
        class _MyListItemState extends State<MyListItem> with AutomaticKeepAliveClientMixin {
          @override
          bool get wantKeepAlive => true;
        
          @override
          Widget build(BuildContext context) {
            super.build(context); // Important!
            return // your item widget;
          }
        }


## 2. ValueNotifier using to update the widgets

          import 'package:flutter/material.dart';
          
          final counter = ValueNotifier<int>(0);
          
          class CounterWidget extends StatelessWidget {
            @override
            Widget build(BuildContext context) {
              return ValueListenableBuilder<int>(
                valueListenable: counter,
                builder: (context, value, child) {
                  return Text('Count: $value', style: TextStyle(fontSize: 24));
                },
              );
            }
          }
          
          void main() {
            runApp(MaterialApp(
              home: Scaffold(
                appBar: AppBar(title: Text('ValueNotifier Counter')),
                body: Center(child: CounterWidget()),
                floatingActionButton: FloatingActionButton(
                  onPressed: () => counter.value++,
                  child: Icon(Icons.add),
                ),
              ),
            ));
          }

  ## 3. ChangeNotifier using to update the widgets

          import 'package:flutter/material.dart';
          import 'package:provider/provider.dart';
          
          class CounterModel extends ChangeNotifier {
            int _count = 0;
            int get count => _count;
            void increment() {
              _count++;
              notifyListeners();
            }
          }
          
          void main() {
            runApp(
              ChangeNotifierProvider(
                create: (_) => CounterModel(),
                child: MyApp(),
              ),
            );
          }
          
          class MyApp extends StatelessWidget {
            @override
            Widget build(BuildContext context) {
              return MaterialApp(
                home: Scaffold(
                  appBar: AppBar(title: Text('Provider Counter')),
                  body: Center(
                    child: Consumer<CounterModel>(
                      builder: (context, model, child) {
                        return Text('Count: ${model.count}', style: TextStyle(fontSize: 24));
                      },
                    ),
                  ),
                  floatingActionButton: FloatingActionButton(
                    onPressed: () => context.read<CounterModel>().increment(),
                    child: Icon(Icons.add),
                  ),
                ),
              );
            }
          }
