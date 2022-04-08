mongostore
==========

[Gorilla's Session](http://www.gorillatoolkit.org/pkg/sessions) store implementation with MongoDB

## Requirements

Depends on the [mgo](https://github.com/kidstuff/mongostore) library.

## Installation

    go get https://github.com/bos-hieu/mongostore

## Documentation

Available on [godoc.org](http://www.godoc.org/github.com/bos-hieu/mongostore).

### Example
```go
    func foo(rw http.ResponseWriter, req *http.Request) {
        // Fetch new store. 
    	client, err := mongo.NewClient(options.Client().ApplyURI("mongodb://localhost:27017"))
    	if err != nil {
    		panic(err)
    	}
    	
    	if err := client.Connect(context.Background()); err != nil {
    		panic(err)
    	}
    	defer client.Disconnect(context.Background())

        // Get a session.
        store := NewMongoStore(
            client.Database("test").Collection("test_session"),
            3600,
            false,
            []byte("secret-key"),
        )

        // Add a value.
        session.Values["foo"] = "bar"

        // Save.
        if err = sessions.Save(req, rw); err != nil {
            log.Printf("Error saving session: %v", err)
        }

        fmt.Fprintln(rw, "ok")
    }
```
