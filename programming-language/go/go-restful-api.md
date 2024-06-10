# RESTFul API with GO

## The main package

- It's where all apis are placed.
- use gin web service
- initialize by using gin.Default()

```go
router.METHOD("/path", callback)
```

```go
func main() {
  router := gin.Default()
  router.GET("/albums", getAlbums)
  router.GET("/albums/:id", getAlbumsByID)
  router.POST("/albums", postAlbums)

  router.Run("localhost:8080")
}

func someFunction(c *gin.Context) {
  // do something here
}
```

## Frequently Used Gin

```go
c.IndentedJSON(http.StatusXX, obj) // print JSON they say use Context.JSON(), instead
```
