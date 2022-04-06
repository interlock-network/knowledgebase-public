# Trust On First Use

In general, trust on first use (or TOFU for short) is a type of authentication scheme, usually for client software to form trusted connections with an unknown endpoint. The general idea is that a client will keep a local database (and in some cases remote) containing a list of trusted endpoints. If an endpoint is unknown (not contained in the database), then either the endpoint is automatically trusted and added to the database, OR the client user is prompted to confirm that the endpoint is to be trusted. All subsequent uses of a trusted endpoint are trusted.

#threat-detection
