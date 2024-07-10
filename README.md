# OpenAPI-article-

# OpenAPI Specification
it allows the description of a remote API accessible through HTTP or HTTP-like protocols. This description, which may be stored as one or more documents (such as local files or HTTP-accessible network resources), is called an **OpenAPI Description** (**OAD**).


# What is an API ?
an **Application Programming Interface** (API) defines the allowed interactions between **two pieces of software**, just like a User Interface defines the ways in which a user can interact with a program.

An API is composed of the list of possible methods to call (requests to make), their parameters, return values and any data format they require (among other things). This is equivalent to how a user's interactions with a mobile phone app are limited to the buttons, sliders and text boxes in the app's User Interface.

APIs can be **local**, where both interacting parties run on the same machine. For example, the Windows API offered by the Operating System to its applications, the Standard C Library offered by any C compiler to the programs being compiled, or the TensorFlow API offered by this machine library to programs using it.

This documentation, though, focuses on **remote** APIs, where the interacting parties run on separate machines and communicate over a network. For example, a public weather service offering up machine-readable forecasts to be consumed by web pages or mobile applications, or Twitter allowing third-party applications to send messages through its network.

To wrap up the definitions, the party offering up its services through an API is called the **provider** and the one requesting these services is the **consumer**.

Using API is an everyday practice in computer science since their benefits are unquestionable.
To name only the most prominent:

- APIs provide **information hiding**: neither side of the API (the provider and the consumer) know the implementation details of the other one. As long as both adhere to the API, they can be changed as much needed without the other party even noticing.
- APIs are also called **Contracts**, because they are assumed to be unbreakable: The provider **promises** not to change its API and to keep honoring it in the years to come. With this promise in hand consumers can start developing their parts and rely on the functionality offered up by the API with confidence.

# API Description through Documentation
APIs are typically accompanied by a **reference guide**; a piece of literature explaining to a developer how to use the API.


Unfortunately, everybody working on software development is familiar with one or more of the following problems:
- unclear documentation
- incomplete or non-existing documentation
- information in a language the reader does not understand
in these cases, to find the information they require developers might have to read source code, debug programs or analyze network traffic, which are gigantic **time sinks**.

# API Description using the OAS

An **API description file** is a **machine-readable** specification of an API. It should strive to be as **complete**, and **fully-detailed** as possible, although absolute completeness is not usually a requirement. Also, just like legal contracts, the more **unambiguous** it is, the more useful it becomes.

its main advantage over documentation which only humans can read is that it enables **automated processing**.

furthermore, a tool can use the API description to **generate boilerplate code** to build provider and consumer applications. Only the business logic needs to be added and the generated code takes care of all the API handling, removing another source of mistakes and making sure that the code and the documentation match. Additionally, if the data passed to the API must satisfy any constraint it can be automatically verified by the boilerplate code, removing even more manual code.

the API description file might include examples, and these examples can be used as responses from **auto-generated mock servers**. This enables early API testing, even before the API provider code is written.

# Structure of an OpenAPI Description

An OpenAPI Description (OAD) describes an HTTP-like API in one or more machine-readable documents (files or network resources). This page describes the syntax of these documents and the minimal structure they must contain.

## OpenAPI Description Syntax

OpenAPI Descriptions are written as one or more text documents. Each document represents a JSON object, in either JSON or YAML format. **References** are used to link parts of the JSON object(s) to each other, and this linked structure is the complete OpenAPI Description. Parsing begins with an OpenAPI Object, and the document containing that object is known as the **entry document**, commonly called `openapi.json` or `openapi.yaml`.

JSON can represent **Numbers**, **Strings**, **Booleans**, `null`, **values**, **Arrays** and **Objects**. An array is an ordered list of values which can have different types. An object (also called Map) is a collection of name-value pairs where the names (also called Keys or Fields) are unique within the object and the values can have any of the supported types (including other objects or arrays).

here's a comparison showing the difference between yaml and json:

JSON :

```
{
    "anObject": {
        "aNumber": 42,
        "aString": "this is a string",
        "aBoolean": true,
        "nothing": null,
        "arrayOfNumbers": [
            1,
            2,
            3
        ]
    }
}
```

YAML:

```
anObject:
    aNumber: 42
    aString: "this is a string"
    aBoolean: true
    nothing: null
    arrayOfNumbers:
    - 1
    - 2
    - 3
```

YAML is typically preferred because of its slightly reduced file size, but the two formats are completely interchangeable.

## Minimal OpenAPI Description Structure

a minimal OpenAPI Description is a single JSON object containing fields adhering to the strucutre defined in the OpenAPI Specification.

the root object in any OpenAPI Description is the OpenAPI Object, and only two of its fields are mandatory: `openapi` and `info`. Additionally, at least one of `paths`, `components` and `webhooks` is required.

- `openapi` (**string**): this indicates the version of the OAS this OAD is using, e.g. "3.1.1". Using this field tools can check that the description correctly adheres to the specification.
- `info` (**Info Object)**: this provides general information about the API (like its description, author and contact information) but only mandatory fields are `title` and `version`.
    - `title` (**string**): a human-readable name for the API, like "Github REST API", useful to keep API collections organized.
    - `version` (**string**): indicates the version **of the API description** (not to be confused with the OAS version above). Tools can use this field to generate code that ensures that clients and servers are interacting through the same version of the API.
- `paths` (**Path Objects**): this describes all the **endpoints** of the API, including their parameters and all possible server responses. Server and client code can be generated from this description, along with its documentation.

here's an example of a minimal OpenAPI Description:

```
openapi: 3.1.0
info:
    title: A minimal OpenAPI Description
    version: 0.0.1
paths: {} # no endpoints defined
```

# API endpoints

## The endpoint list

API endpoints (also called Operations or Routes) are called **Paths** in the OAS. The Paths Object, accessible through the `paths` field in the root OpenAPI Object, is the container for all operations supported by the API:

![illustration](https://spec.openapis.org/oas/v3.1.0#pathItemObject)

every field in the Paths Object is a Path Item Object describing one API endpoint. Fields are used instead of an Array because they enforce endpoint name uniqueness at the syntax level.

paths **must start with a forward slash** `/` since they are directly appended to the serever URL to construct the full endpoint URL.

```
openapi: 3.1.0
info:
    tile: Tic Tac Toe
    description: |
        This API allows writing down marks on a Tic Tac Toe board and requesting the state of
        the board or of individual squares.
    version: 1.0.0
paths:
    /board:
```
