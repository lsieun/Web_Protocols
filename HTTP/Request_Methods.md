# HTTP methods

## Intro

There are four main HTTP methods, four verbs if you will, that identify the operations that can be performed:

- GET
- POST
- PUT
- DELETE

These four methods are not arbitrary. They have specific semantics that applications should adhere to.

The `GET` method retrieves a representation of a resource. `GET` is side-effect free, and can be repeated without concern if it fails. Furthermore, its output is often cached, though that can be controlled with the right headers, as you’ll see shortly. In a properly architected system, `GET` requests can be bookmarked and prefetched without concern. For example, one should not allow a file to be deleted merely by following a link because a browser may GET all links on a page before the user asks it to. By contrast, a well-behaved browser or web spider will not POST to a link without explicit user action.

The `PUT` method uploads a representation of a resource to the server at a known URL. It is not side-effect free, but it is idempotent. That is, it can be repeated without concern if it fails. Putting the same document in the same place on the same server twice in a row leaves the server in the same state as only putting it once.

The `DELETE` method removes a resource from a specified URL. It, too, is not side-effect free, but is idempotent. If you aren’t sure whether a delete request succeeded—for instance, because the socket disconnected after you sent the request but before you received a response—just send the request again. Deleting the same resource twice is not a mistake.

The `POST` method is the most general method. It too uploads a representation of a resource to a server at a known URL, but it does not specify what the server is to do with the newly supplied resource. For instance, the server does not necessarily have to make that resource available at the target URL, but may instead move it to a different URL. Or the server might use the data to update the state of one or more completely different resources. `POST` should be used for **unsafe operations that should not be repeated**, such as making a purchase.

## Select Method

Because `GET` requests include all necessary information in the URL, they can be bookmarked, linked to, spidered, and so forth. `POST`, `PUT`, and `DELETE` requests cannot be. This is deliberate. `GET` is intended for noncommital actions, like browsing a static web page. The other methods, especially `POST`, are intended for actions that commit to something. For example, adding an item to a shopping cart should send a `GET`, because this action doesn’t commit; the user can still abandon the cart. However, placing the order should send a `POST` because that action makes a commitment. This is why browsers ask you if you’re sure when you go back to a page that uses POST. Reposting data may buy two copies of a book and charge your credit card twice.

In practice, `POST` is vastly overused on the Web today. Any safe operation that does not commit the user to anything should use `GET` rather than `POST`. Only operations that commit the user should use `POST`.

One sometimes mistaken reason for preferring `POST` over `GET` is when forms require large amounts of input. There’s an outdated misconception that browsers can only work with query strings of a few hundred bytes. Although this was true in the mid-1990s, today all major browsers are good up to URL lengths of at least `2,000` characters. If you have more form data to submit than that, you may indeed need to support `POST`; but safe operations should still prefer `GET` for nonbrowser clients. This is less common than you might think, though. You usually only exceed those limits if you’re uploading data to the server to create a new resource, rather than merely locating an existing resource on the server; and in these cases `POST` or `PUT` is usually the right answer anyway.

In addition to these four main HTTP methods, a few others are used in special circumstances. The most common such method is `HEAD`, which acts like a `GET` except it only returns the header for the resource, not the actual data. This is commonly used to check the modification date of a file, to see whether a copy stored in the local cache is still valid.

The other two that Java supports are `OPTIONS`, which lets the client ask the server what it can do with a specified resource; and `TRACE`, which echoes back the client request for debugging purposes, especially when proxy servers are misbehaving. Different servers recognize other nonstandard methods including `COPY` and `MOVE`, but Java does not send these.
