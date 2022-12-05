# Using the Fetch API
Fetch is a browser built-in API for making HTTP calls. Returns a promise. Note - The promise will get resolved even when the request has a status other than 2XX. It will only fail if something is wrong with fetch like internet is disconnected but not if something is wrong with the API endpoint. So you must check if the request has succeeded in the "then" callback.

## Get Request
```javascript
fetch("https://reqres.in/api/users")
.then((res) => {
  if(res.ok){
    console.log("Success");
    res.json() // Note that we need to call with method on the res object to get data, it is not readable directly. this also returns a promise
    .then((data) => {
      console.log(data);
      /*
      Output:
      {
        data: Array(6),
        page: 1,
        per_page: 6,
        total: 12,
        total_pages: 2
      }
      */
    }); 
  } else {
    console.log("Failure");
  }
})
.catch((error) => {
  console.log(error);
});
```

## Other Types of Requests Such As Post
```javascript
fetch("https://reqres.in/api/users", {
  method: "POST", // or GET, DELETE, PUT
  headers: {
    "Content-Type": "application/json" // This is very important, otherwise the POST request will not work
  },
  body: JSON.stringify({ // Stringify is very important, otherwise the POST request will not work
    name: "Abhinav Aggarwal"
  })
})
.then((res) => {
  console.log(res.json());
  /*
  Output:
  {
    createdAt: "date-string",
    id: 32,
    name: "Abhinav Aggarwal"
  }
  */
})
.catch((error) => {
  console.log(error);
});
```
