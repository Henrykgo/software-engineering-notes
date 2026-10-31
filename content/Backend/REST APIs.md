A REST API is a way for different software systems to communicate over the web using standard HTTP methods and conventions.

Basic Concepts
- Resources: things the API works with, represented by URLs e.g. /parcels/123
- HTTP methods: describes what you want
	- GET -> read
	- POST -> create
	- PUT -> update
	- DELETE -> remove
- request & response: the client sends a request, and the server sends back a response, usually JSON
- status codes: tell you what happened:
	- 200 -> success
	- 500 -> server error
- Stateless: each requests contains the information the server needs. The server doesnt need to remember previous requests, so any backend instance can handle the next request
- Idempotent: repeating the same request has the same intended result as doing it once. (POST is usually not)