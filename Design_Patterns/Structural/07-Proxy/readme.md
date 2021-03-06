# Proxy
Lets you provide a substitute or placeholder for another object.

### Problem
You have a massive object that consumes a vast amount of system resources. You need it from time to time, but not always. You could implement lazy initialization and all of object's clients would need to execute some deferred initialization code. This would probably cause a lot of ```code duplication```.

### Solution
This pattern suggests you create a new proxy class with the same interface as an original service object. Upon receiving a request from a client, the proxy creates a real service object and delegates all the work to it.

```
  Client 1    --
  Client 2    --    Proxy   --- DataBase
  Client 3    --
The proxy disguises itself as a database object. It can handle lazy initialization and rsult caching wuthout the client or the real database object even knowing.
```

### Benefit
If you need to execute something either before or after the primary logic of the class, the proxy lets you do this without changing that class. Since the proxy implements the same interface as the original class, it can be passed to any client that expects a real service object.

### Structure
1- ```Service interface``` -> Declares the interface of the Service and Proxy must follow this.

2- The ```Service``` -> is a class that provides some useful business logic.

3- The ```Proxy``` -> has a reference field that points to a service object. After finishes its processing it passes the requests to the service object.

4- ``` The Client``` -> should work with bother services and proxies using the same interface.
 
### Applicability
1- Lazy initialization (virtual proxy)

2- Access Control (protection proxy). Specific clients are able to use the service object.

3- Local execution of a remote service (remove proxy). This is when the service object is located on a remote server.

4- Logging requests (logging proxy). Whe you want to keep a history of requests to the service object.

5- Caching request result (caching proxy). Cache results of client request and manage the life cycle of this cache.

### Pros
1- You can control the service object without clients knowing about it.

2- You can manage the lifecycle of the service object when clients don't care about it.

3- The Proxy works even if the service object is not ready or is not available.

4- Open/Closed Principle. You can introduce new proxies without changing the service or clients.

### Cons
1- The code may become more complicated since you need to introduce a lot of new classes.

2- The response from the service might get delayed.
