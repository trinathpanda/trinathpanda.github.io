---
layout: post
title: "JSON: Basic Concepts & Data Types"
date: 2025-10-15 12:00:00 +0000
categories: [Data Formats, JSON]
tags: [json, data types, tutorial]
---


In this post you’ll learn what JSON is, why it’s so widely used, what its core syntax rules are, and what data types JSON supports. You’ll also see examples to cement your understanding.


## What is JSON

- JSON stands for *JavaScript Object Notation* [1].

- It’s a lightweight, text-based format for representing structured data, independent of programming language [2].

- It’s very popular for data interchange—APIs [3], configuration files [4], or anywhere you need a simple, readable format to move data between systems.

In JSON:
- Data is represented as **key:value** pairs (in objects) or as ordered lists (in arrays).

- Keys (names) must always be strings, enclosed in double quotes.

- Whitespace (spaces, newlines, tabs) is allowed and ignored outside string literals, for readability.

- JSON does **not** support comments.

## JSON Syntax / Structure

1. **Object**
    - Enclosed in curly braces `{ … }`.
    - Inside: zero or more name/value pairs, separated by commas.
    - Name (aka key) must be a string in double-quotes.
    - The name and value are separated by a colon `:`. 
    - Example: 

        ```json
        {
        "name": "Alice",
        "age": 30
        }
        ```

2. **Array**
    - Enclosed in square brackets `[ … ]`.
    - Elements are ordered, separated by commas.
    - Elements can be any valid JSON value (string, number, object, array, boolean, null)
    - Example:

        ```json
        {
        "colors": ["red", "green", "blue"]
        }
        ```

3. **Nesting**
    - Objects and arrays can be nested arbitrarily.
    - You can have an object inside an array, array inside object, etc.
    - Example:

        ```json
        {
            "user": {
                "id": 1,
                "roles": ["admin", "user"]
            },
            "active": true
        }
        ```

4. **Whitespace and formatting**
    - Whitespaces (spaces, tabs, line breaks) are allowed between tokens, to improve readability.
    - No trailing commas (i.e. you cannot have an extra comma before closing `}` or `]`).

    - JSON does not support comments (`//` or `/*` … `*/` are invalid) [5].



## Data Types Supported in JSON

JSON supports six basic types (4 primitive, 2 compound) [6] :

| Type | Description / Constraints | Example(s) |
|------|---------------------------|------------|
| String | Sequence of Unicode characters, must be in double quotes. Supports escape sequences (e.g. \", \\, \n) [7]. | `"hello"`, `"Line\nBreak"` |
| Number | A numeric literal (integer or floating-point). No special values like NaN or Infinity allowed. | `123`, `3.14`, `-42`, `1.5e3` |
| Boolean | true or false | `true`, `false` |
| Null | The literal null, meaning “no value” |	`null` |
| Object | A collection of name/value pairs (keys are strings). | `{ "a": 1, "b": "text" }` |
| Array | An ordered list of values (any of the types) | `[1, "two", false, null, { "x": 5 }]` |



## Important caveats / notes:

- JSON does not support functions, special types like undefined, or date/time types natively. Dates are usually encoded as strings [8]. 

- In JSON, there is no distinction between integer vs floating-point types — both are `“number”` type [9]. 



## Full Combined Example
Here is a more realistic JSON example combining types, nesting, arrays, etc.:

```json
{
  "first_name": "John",
  "last_name": "Smith",
  "is_alive": true,
  "age": 27,
  "address": {
    "street_address": "21 2nd Street",
    "city": "New York",
    "state": "NY",
    "postal_code": "10021-3100"
  },
  "phone_numbers": [
    {
      "type": "home",
      "number": "212 555-1234"
    },
    {
      "type": "office",
      "number": "646 555-4567"
    }
  ],
  "children": [
    "Catherine",
    "Thomas",
    "Trevor"
  ],
  "spouse": null
}
```
This is exactly the example shown on Wikipedia’s JSON page [10].



[1]: https://www.w3schools.com/js/js_json.asp "Javascript JSON - W3 Schools"
[2]: https://www.digitalocean.com/community/tutorials/an-introduction-to-json#:~:text=it%E2%80%99s%20available%20for%20use%20by%20many%20languages%20including%20Python%2C%20Ruby%2C%20PHP%2C%20and%20Java. "An Introduction to JSON - Digital Ocean"
[3]: https://www.digitalocean.com/community/tutorials/an-introduction-to-json#:~:text=JSON%20has%20been%20experiencing%20increased%20support%20in%20APIs "n Introduction to JSON - Digital Ocean"
[4]: (https://stackoverflow.blog/2022/06/02/a-beginners-guide-to-json-the-data-format-for-the-internet "A Beginners Guide to JSON - Stackoverflow Blog"
[5]: https://www.freecodecamp.org/news/what-is-json-a-json-file-example#:~:text=No%20comments%20(//%20or%20/%20/)%20are%20allowed%20in%20JSON%20data.%20(But%20you%20can%20get%20around%20that%2C%20if%20you%27re%20curious. "What is JSON - FreeCodeCamp"
[6]: https://www.geeksforgeeks.org/javascript/json-data-types/#:~:text=JSON%20supports%20mainly,Array "Json Data Type - GeekforGeeks"
[7]: (https://restfulapi.net/json-data-types/ "JSON Data Type - RestFul API"
[8]: https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Scripting/JSON?#:~:text=For%20non%2Dprimitives%2C%20JSON%20can%20contain%20object%20literals%20and%20arrays%2C%20but%20not%20functions%20or%20any%20other%20object%20types%2C%20such%20as%20Date%2C%20Set%2C%20and%20Map.%20The%20objects%20and%20arrays%20inside%20JSON%20need%20to%20further%20contain%20valid%20JSON%20data%20types. "Working with JSON"
[9]: https://www.w3schools.com/js/js_json_syntax.asp#:~:text=In%20JSON%2C%20keys%20must%20be%20strings%2C%20written%20with%20double%20quotes%3A "JSON Syntax - W3Schools"
[10]: https://en.wikipedia.org/wiki/JSON#:~:text=The%20following%20example%20shows%20a%20possible%20JSON%20representation%20describing%20a%20person. "JSON - Wiki"

