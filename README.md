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