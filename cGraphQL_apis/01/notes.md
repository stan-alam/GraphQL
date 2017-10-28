REST API authors use the following techniques and conventions to address the limited control of what is returned to the client ... REST >>> garbage in, garbage out. **the contract with the client and server is one-sided:** 
## The client gets what the server wants to give it

	Writing detailed, custom documentation about API responses, so clients at least know what to expect.

	Supporting query parameters like (include and fields) that act as flags to select information, 
    adding some limited flexibility.

	Including references (either IDs or URLs) to related data, rather than embedding it, effectively 
	splitting the query across multiple requests.

	Using different resources to model different levels of data inclusion (for example, /users/123 as a full 
		set of data and /profiles/123 as a sparse set of data), duplicating or reusing large chunks of code. )

	Splitting the API completely, perhaps by platform (for instance, exposing /desktop/users/123 
	and /mobile/users/123) to support the needs of different types of clients.

	Some combination of all of these.