# express-session-socket.io

Simple middleware to expose express session objects inside socket.io

## Example usage:
```
io.use(require('express-session-socket.io')(sessionStore, 'very Secure Secret', function (err, session, socket, next) {
    if (err) next(err);
    socket.session = session;
    next();
}));
```

## Namespaces: 
If you use a namespace, sockets are only preserved if you use it on that namespace. i.e.
```
var foo = io.of('/foo');

foo.use(require('express-session-socket.io')(sessionStore, 'very Secure Secret', function (err, session, socket, next) {
    if (err) next(err);
    socket.session = session;
    next();
}));
```

It's worth noting that I've observed if you have middleware on io and foo, they'll both be executed, but the socket changes will only be consumable in the appropriate namespace.
