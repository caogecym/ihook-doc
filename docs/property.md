---
id: property
title: Property
---

When configuring notification conditions, you may specify [JsonPath](https://github.com/json-path/JsonPath) expression in the property field to extract response data for evaluation. Here an example of how JsonPath expression works.

JsonPath Examples
-------------

Given the JSON response

```javascript
{
    "store": {
        "book": [
            {
                "category": "reference",
                "author": "Nigel Rees",
                "title": "Sayings of the Century",
                "price": 8.95
            },
            {
                "category": "fiction",
                "author": "Evelyn Waugh",
                "title": "Sword of Honour",
                "price": 12.99
            },
            {
                "category": "fiction",
                "author": "Herman Melville",
                "title": "Moby Dick",
                "isbn": "0-553-21311-3",
                "price": 8.99
            },
            {
                "category": "fiction",
                "author": "J. R. R. Tolkien",
                "title": "The Lord of the Rings",
                "isbn": "0-395-19395-8",
                "price": 22.99
            }
        ],
        "bicycle": {
            "color": "red",
            "price": 19.95
        }
    },
    "expensive": 10
}
```

| JsonPath (click link to try)| Result |
| :------- | :----- |
| <a href="http://jsonpath.herokuapp.com/?path=store.bicycle.color" target="_blank">store.bicycle.color</a>| red |
| <a href="http://jsonpath.herokuapp.com/?path=store.book.length()" target="_blank">store.book.length()</a>                 | 4                     |
| <a href="http://jsonpath.herokuapp.com/?path=store.book[2]" target="_blank">store.book[2]</a>                 | The third book                      |
| <a href="http://jsonpath.herokuapp.com/?path=store.book[-2]" target="_blank">store.book[-2]</a>                 | The second to last book            |
| <a href="http://jsonpath.herokuapp.com/?path=store.book[0,1]" target="_blank">store.book[0,1]</a>               | The first two books               |
| <a href="http://jsonpath.herokuapp.com/?path=store.book[:2]" target="_blank">store.book[:2]</a>                | All books from index 0 (inclusive) until index 2 (exclusive) |
| <a href="http://jsonpath.herokuapp.com/?path=store.book[1:2]" target="_blank">store.book[1:2]</a>                | All books from index 1 (inclusive) until index 2 (exclusive) |
| <a href="http://jsonpath.herokuapp.com/?path=store.book[-2:]" target="_blank">store.book[-2:]</a>                | Last two books                   |
| <a href="http://jsonpath.herokuapp.com/?path=store.book[2:]" target="_blank">store.book[2:]</a>                | Book number two from tail          |
| <a href="http://jsonpath.herokuapp.com/?path=store.book[*].author" target="_blank">store.book[*].author</a>| The authors of all books     |
| <a href="http://jsonpath.herokuapp.com/?path=.author" target="_blank">.author</a>                   | All authors                         |
| <a href="http://jsonpath.herokuapp.com/?path=store.*" target="_blank">store.*</a>                  | All things, both books and bicycles  |
| <a href="http://jsonpath.herokuapp.com/?path=store..price" target="_blank">store..price</a>             | The price of everything         |
| <a href="http://jsonpath.herokuapp.com/?path=store.book[?(@.isbn)]" target="_blank">store.book[?(@.isbn)]</a>          | All books with an ISBN number         |
| <a href="http://jsonpath.herokuapp.com/?path=store.book[?(@.price < 10)]" target="_blank">store.book[?(@.price < 10)]</a> | All books in store cheaper than 10  |
| <a href="http://jsonpath.herokuapp.com/?path=store.book[?(@.price <= $['expensive'])]" target="_blank">store.book[?(@.price <= $['expensive'])]</a> | All books in store that are not "expensive"  |
| <a href="http://jsonpath.herokuapp.com/?path=store.book[?(@.author =~ /.*REES/i)]" target="_blank">store.book[?(@.author =~ /.*REES/i)]</a> | All books matching regex (ignore case)  |
| <a href="http://jsonpath.herokuapp.com/?path=.*" target="_blank">.*</a>                        | Give me every thing   

Operators
---------

| Operator                  | Description                                                        |
| :------------------------ | :----------------------------------------------------------------- |
| `@`                       | The current node being processed by a filter predicate.            |
| `*`                       | Wildcard. Available anywhere a name or numeric are required.       |
| `..`                      | Deep scan. Available anywhere a name is required.                  |
| `.<name>`                 | Dot-notated child                                                  |
| `['<name>' (, '<name>')]` | Bracket-notated child or children                                  |
| `[<number> (, <number>)]` | Array index or indexes                                             |
| `[start:end]`             | Array slice operator                                               |
| `[?(<expression>)]`       | Filter expression. Expression must evaluate to a boolean value.    |


Functions
---------

Functions can be invoked at the tail end of a path - the input to a function is the output of the path expression.
The function output is dictated by the function itself.

| Function                  | Description                                                         | Output    |
| :------------------------ | :------------------------------------------------------------------ |-----------|
| min()                     | Provides the min value of an array of numbers                       | Double    |
| max()                     | Provides the max value of an array of numbers                       | Double    |
| avg()                     | Provides the average value of an array of numbers                   | Double    |
| stddev()                  | Provides the standard deviation value of an array of numbers        | Double    |
| length()                  | Provides the length of an array                                     | Integer   |
| sum()                     | Provides the sum value of an array of numbers                       | Double    |


Filter Operators
-----------------

Filters are logical expressions used to filter arrays. A typical filter would be `[?(@.age > 18)]` where `@` represents the current item being processed. More complex filters can be created with logical operators `&&` and `||`. String literals must be enclosed by single or double quotes (`[?(@.color == 'blue')]` or `[?(@.color == "blue")]`).   

| Operator                 | Description                                                           |
| :----------------------- | :-------------------------------------------------------------------- |
| ==                       | left is equal to right (note that 1 is not equal to '1')              |
| !=                       | left is not equal to right                                            |
| <                        | left is less than right                                               |
| <=                       | left is less or equal to right                                        |
| >                        | left is greater than right                                            |
| >=                       | left is greater than or equal to right                                |
| =~                       | left matches regular expression  [?(@.name =~ /foo.*?/i)]             |
| in                       | left exists in right [?(@.size in ['S', 'M'])]                        |
| nin                      | left does not exists in right                                         |
| subsetof                 | left is a subset of right [?(@.sizes subsetof ['S', 'M', 'L'])]       |
| anyof                    | left has an intersection with right [?(@.sizes anyof ['M', 'L'])]     |
| noneof                   | left has no intersection with right [?(@.sizes noneof ['M', 'L'])]    |
| size                     | size of left (array or string) should match right                     |
| empty                    | left (array or string) should be empty                                |