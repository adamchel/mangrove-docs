+++
next = "/2-models/allowed-types"
prev = "/2-models"
title = "Introduction"
toc = true
weight = 1

+++

A **model** is the fundamental way you access data in MongoDB with Mangrove. Models lets you treat C++ classes as objects you can store in the database. When you make a class a model, you can specify

## Creating a Model

You can turn almost any C++ class into a model by having it inherit publicly from the `mangrove::model<T>` base class, where `T` is type of the class you are making a model.

```cpp
// Example of inheritance required for model
class Message : mangrove::model<Message> {
    bsoncxx::oid author_id;
    std::string content;
    std::chrono::system_clock::time_point time_sent;
}
```

This inheritance gives the inheriting class access to the interface specified here (TODO: Doxygen link). The inheritance also gives you access to the `_id` variable. Since every document stored in a MongoDB database contains an `_id`, the model stores one automatically for you. By default this of type {{% a_blank "`bsoncxx::oid`" "http://mongodb.github.io/mongo-cxx-driver/classbsoncxx_1_1oid.html" %}}, but you can customize it. We'll discuss how to do this in a [later section](/2-models/custom_id).

## Specifying Fields to Serialize

Before you can use a model, you must specify which of its fields you want to be included when an instance of a model is serialized and saved to the database. You can do this with the `MANGROVE_MAKE_KEYS_MODEL` macro.

This macro accepts the class you are registering as a model, as well as a variadic list of the fields you want to include, wrapped as name-value pairs (**NVPs**).

```cpp
// Example of registering fields in model
class Message : mangrove::model<Message> {
    bsoncxx::oid author_id;
    std::string content;
    std::chrono::system_clock::time_point time_sent;
    int dont_include_me;

    MANGROVE_MAKE_KEYS_MODEL(Message,
                             MANGROVE_NVP(author_id),
                             MANGROVE_NVP(content),
                             MANGROVE_NVP(time_sent))
}
```

The `MANGROVE_NVP` macro specifies that you want its argument serialized in such a way that its **name** or **key** is the name of the variable. For example, in the above code sample, the resulting saved BSON document would look something like the following:

```json
{
    "_id" : ObjectId("576d7238e249391db3271e31"),
    "author_id" : ObjectId("576d5145e2493917691144f1"),
    "content" : "Hey, did you see how cool Mangrove is?!",
    "time_sent" : ISODate("2016-07-01T14:42:06.018Z")
}
```

{{% notice info %}}
While there is no limitation to the complexity of the classes you can turn into a model, there are limitations regarding which types are serializable and can be included in the `MANGROVE_MAKE_KEYS_MODEL` macro. These limitations are discussed in the [next section](/2-models/allowed-types). 
{{% /notice %}}

If you don't want the name of the field to be exactly the same as the name of your variable, you can use the macro `MANGROVE_CUSTOM_NVP` (TODO: may be different) to specify a custom name for the resulting BSON element of a particular field.

TODO: code sample

TODO: tip about shortening variable names

## Active Record Manipulation
