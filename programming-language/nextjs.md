# NextJS

NextJS is a framework built on top of React

- Node ver > 18

## Routing

- URL replicate directory

### Static Routing

```
dir src/dashboard/app/page.js
url localhost:XXXX/dashboard/app
```

- I can put ( ) in _dashboard_ to remove it from url

### Dynamic Routing

```python
dir scr/dashboard/app/[id]/page.js
url localhost:XXXX/dashboard/app/:id
```

Multiple params is also allowed

```python
dir scr/dashboard/app/[id]/[title]/page.js
url localhost:XXXX/dashboard/app/:id/:title
```

Access to params by pass it as props

```javascript
const Component = ({ params }) => {
  return (
    <div>
      {params.id} {params.title}
    </div>
  );
};
```

Catching all routes

- Convenient when rendering pages that have same layout but different information

```python
dir scr/dashboard/app/[...id]/page.js
url localhost:XXXX/dashboard/app/:id/:canbeanything/:multipletimes

params = { id: string[] }

```

Or I can

- doing [[x]] will also include the upper dir
- useful when want to render the same without :id

```python
dir scr/dashboard/app/[[...id]]/page.js
url localhost:XXXX/dashboard/app
```
