+++
next = "/2-models/custom_id"
prev = "/2-models/introduction"
title = "Allowed Types"
toc = true
weight = 2

+++

As we discussed in the previous section, there are a limited number of types that you can save and load, or **serialize** in the database. Here we'll enumerate every type that you can include in the `MANGROVE_MAKE_KEYS_MODEL` macro.

## Primitive Types

Mangrove officially supports the following four primitive types:

* `int32_t`
* `int64_t`
* `double`
* `bool`

{{% notice warning %}}
Mangrove will also accept other primitive types such as `int`, `long`, or `unsigned int`, but we highly recommend that you go with one of the four supported types. Other types will be implicitly cast to one of the four supported types, which might cause unpredictable behavior that differs from platform to platform.
{{% /notice %}}

## Strings

Mangrove officially supports the serialization of `std::string`. If you prefer to use string "views" that minimize the number of copies your program makes, check the `b_utf8` type discussed in [BSON "View" Types](/2-models/allowed-types/#bson-view-types).

## Containers

## Optionals

## BSON Types

### BSON "View" Types

