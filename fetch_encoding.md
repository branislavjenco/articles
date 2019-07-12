# Fetch API doesn't support other encodings than UTF-8

When fetching data from a server using the Fetch API's `response.text()` method, only UTF-8 is used, and cannot be changed.
Solution is to use an `ArrayBuffer` and `TextEncoder`, like this:
```
data = await response.arrayBuffer().then(buffer => {
  const decoder = new TextDecoder(encoding);
  return decoder.decode(buffer);
});
```

Now it's easy when you always know the encoding, but ideally we want to use the encoding
that the server gives us in the response headers. Like this:

```
const contentType = response.headers.get('content-type');
const encoding = contentType.match(/charset=([\s\S]+)$/)[1];
```

Beware, `TextEncoder` is not supported in IE11 or Edge (`ArrayBuffer` is). There is an npm package called `text-encoding` that allegedly serves as a polyfill but I haven't tested it.
