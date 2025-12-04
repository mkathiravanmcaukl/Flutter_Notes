## What are the different approaches to Json Parsing in Flutter?

  
### 1. Manual Parsing(using dart:convert)

  -> Use jsonDecode() to parse JSON into a Map<String, dynamic> or List.

  -> Manually map the JSON keys to your model class

  Pros: Simple, no dependencies
  
  Cons: Verbose, error-prone, no compile-time safety

              import 'dart:convert';
              
              class User {
                final String name;
                final int age;
              
                User({required this.name, required this.age});
              
                factory User.fromJson(Map<String, dynamic> json) {
                  return User(
                    name: json['name'],
                    age: json['age'],
                  );
                }
              }
              
              void main() {
                String jsonString = '{"name": "Alice", "age": 30}';
                Map<String, dynamic> jsonMap = jsonDecode(jsonString);
                User user = User.fromJson(jsonMap);
              }

 ### 2. Code Generation with json_serializable

--> Use the json_serializable + build_runner package.

--> You annotate your model with @JsonSerializable and code gets generated automatically

Pros: Less biolerplate, type-safe, scalabe for large projects

Cons: Requires build_runner

          import 'package:json_annotation/json_annotation.dart';
          
          part 'user.g.dart';
          
          @JsonSerializable()
          class User {
            final String name;
            final int age;
          
            User({required this.name, required this.age});
          
            factory User.fromJson(Map<String, dynamic> json) => _$UserFromJson(json);
            Map<String, dynamic> toJson() => _$UserToJson(this);
          }


  
