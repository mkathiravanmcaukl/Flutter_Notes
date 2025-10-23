## What is the use of AutomaticKeepAliveClientMixin for listview items in flutter

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
