# Server

## Web Server

- A web server is just a computer that serves data over a network, typically the Internet.
- Servers run software that listens for incoming requests from clients. When a request is received, the server responds with the requested data.
- Any server worth its salt (suspiciously looking at you Python...) can handle many requests at the same time. In Go, we do this by spawning a new goroutine for each request.

## Go Routine in Server

- Go servers are great for performance whether the workload is I/O or CPU-bound
- Node.js and Express work well for I/O-bound tasks, but struggle with CPU-bound tasks
- Python and Django/Flask do just fine with I/O bound tasks, but frankly, no one picks Python for its performance

## Debugging Server

Debugging a CLI app is simple:

- Write some code
- Build and run the code
- See if it did what you expected.
- If it didn't, add some logging or fix the code, and go back to step 2.

Debugging a server is a little different. The simplest way (minimal tooling) is to:

- Write some code
- Build and run the code
- Send a request to the server using a browser or some other HTTP client
- See if it did what you expected.
- If it didn't, add some logging or fix the code, and go back to step 2.

## HTTP Handler

```go
// it's just a interface

type Handler interface {
	ServeHTTP(ResponseWriter, *Request)
}
```

## Middleware Signature

```go
func (cfg *apiConfig) middlewareMetricsInc(next http.Handler) http.Handler {
	return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
		cfg.fileServerHits++
		next.ServeHTTP(w, r)
	})
}

func (cfg *apiConfig) metricsHandler(w http.ResponseWriter, r *http.Request) {
	hits := cfg.fileServerHits
	w.Header().Set("Content-Type", "text/plain; charset=utf-8")
	w.WriteHeader(http.StatusOK)
	w.Write([]byte(fmt.Sprintf("Hits: %d", hits)))
}
```

## Routing

> Fixed URL Paths

- A pattern that exactly matches the URL path. For example, if you have a pattern /about, it will match the URL path /about and no other paths.
  Subtree Paths
- If a pattern ends with a slash /, it matches all URL paths that have the same prefix. For example, a pattern /images/ matches /images/, /images/logo.png, and /images/css/style.css. As we saw with our /app/\* path, this is useful for serving a directory of static files or for structuring your application into sub-sections.

> Longest Match Wins

- If more than one pattern matches a request path, the longest match is chosen. This allows more specific handlers to override more general ones. For example, if you have patterns / (root) and /images/, and the request path is /images/logo.png, the /images/ handler will be used because it's the longest match.

> Host-specific Patterns

- We won't be using this but be aware that patterns can also start with a hostname (e.g., www.example.com/). This allows you to serve different content based on the Host header of the request. If both host-specific and non-host-specific patterns match, the host-specific pattern takes precedence.

## Decode JSON Request Body

```go
{
    "name": "John",
    "age": 30,
}

func handler(w http.ResponseWriter, r *http.Request){
    type parameters struct {
        // these tags indicate how the keys in the JSON should be mapped to the struct fields
        // the struct fields must be exported (start with a capital letter) if you want them parsed
        Name string `json:"name"`
        Age int `json:"age"`
    }

    decoder := json.NewDecoder(r.Body)
    params := parameters{}
    err := decoder.Decode(&params)
    if err != nil {
        // an error will be thrown if the JSON is invalid or has the wrong types
        // any missing fields will simply have their values in the struct set to their zero value
		log.Printf("Error decoding parameters: %s", err)
		w.WriteHeader(500)
		return
    }
    // params is a struct with data populated successfully
    // ...
}
```

## Encode JSON Request Body

```go
func handler(w http.ResponseWriter, r *http.Request){
    // ...

    type returnVals struct {
        // the key will be the name of struct field unless you give it an explicit JSON tag
        CreatedAt time.Time `json:"created_at"`
        ID int `json:"id"`
    }
    respBody := returnVals{
        CreatedAt: time.Now(),
        ID: 123,
    }
    dat, err := json.Marshal(respBody)
	if err != nil {
		log.Printf("Error marshalling JSON: %s", err)
		w.WriteHeader(500)
		return
	}
    w.Header().Set("Content-Type", "application/json")
    w.WriteHeader(200)
	w.Write(dat)
}
```

## end
