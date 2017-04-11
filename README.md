# rocket_cors

Plucked from a [rejected PR][Rejected] to rocket_contrib, this crate contains a basic 
Response Wrapper adding handling for CORS negotiation to a Rocket Responder. 

The `CORS` type, which implements `Responder`. This type allows
you to request resources from another domain.

# Usage

You can use the `CORS` type for you routes as a preflight like that:

    #[route(OPTIONS, "/user")]
    fn cors_preflight() -> PreflightCORS {
        CORS::preflight("http://somehost.com")
            .methods(vec![Method::Options, Methods::Get])
            .headers(vec!["Content-Type"])
    }

And then you can just simply do something like this:

    
    #[get("/user")]
    fn user() -> CORS<String> {
        CORS::any("Hello I'm User!".to_string())
    }
    

[Rejected]: https://github.com/SergioBenitez/Rocket/pull/141
