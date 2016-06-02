## Realms

>Realms are deeply connected with hapi's plugin system, so it's suggested that you read about [plugins](/tutorials/plugins) before moving on to realms.

Put simply, a **realm** is a context for a specific instance of a plugin being registered.  It is a limited version of a sandbox for plugins to maintain state used by the framework when adding routes, extensions, and other properties.  In practice you interact with a realm as a plain object with,
  1. some read-only properties that describe settings and options particular to the plugin's registration.
  2. some writable areas to store information that should remain sandboxed within the plugin.

It's worth reiterating the distinction that a realm isn't specific just to a plugin, but rather to a particular registration of a plugin.  For example, if one plugin were registered multiple times then each registration would have its own realm.

### What uses realms?
`server.bind()`, `server.path()`, `server.view()`, etc. (todo)

### How do I access the realm?

The realm is available in three places,
  - The [server](/api#server) via [`server.realm`](/api#serverrealm).  When your plugin's `register` function is called (`function(server, options, next)`) a realm is created and made available here.  Request extensions, routes, etc. registered to the server will have access to this realm.  When you're not in a plugin, you instead have access to the single "root" realm.
  - The [reply interface](/api#reply-interface) via `reply.realm`.
    - In a route handler, this is the realm in which the route was added.
    - In a request extension, this is the realm in which the extension was registered.
    - In an authentication strategy, this is the realm in which the strategy was defined.
  - The [route public interface](/api#route-public-interface) via `route.realm`.  Notably, once a route is resolved you can access the realm from the request on `request.route.realm`.

### How can I leverage realms?
Usually server decorations. (todo)
