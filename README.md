### Intro

Debugging a network request _(AKA: ajax, hxr, fetch...)_ is a very important skill when tracking down bugs

### What we will do

1. Create server on our local machine that we can send ajax request to
2. Open a static webpage that will make an ajax request to our server
3. Realize our ajax request is not getting the expected information
4. Inspect the _Network_ tab in the _Developer Console_ to see what we are sending and getting back
5. Update our ajax call to handle the correct data

### Steps

1. Clone Repo

  ```
  git clone git@github.com:stevenkaspar/learning-debug-network-request.git
  cd learning-debug-network-request
  ```

2. Start Server

  ```
  python server.py
  ```

3. Open static `index.html` file in browser

4. Click _**Make Ajax Request**_ button

  You will see an error `Ajax Error: response.map is not a function`

5. Right-Click webpage and click _**Inspect**_

  You will in the _Console_ tab that there is a warning at line `index.html:17`

6. Inspect `index.html:17`

  After looking at the code, you will notice we are expecting the _**response**_ object to be an array of items, but we are getting an error when trying that

  You could put a `console.log(response)` in the code to debug, but for this example we are going to look at the _Network_ tab and look at the response directly

7. Go to the _Network_ tab

8. Click _**Make Ajax Request**_ button again

  There will now be an entry on the _Network_ tab

9. Click the _localhost_ line entry and click the _Response_ tab

  This is the body of the network request's response (what the server sent back). You can see it is sending back an object instead of an array

  ```
  {"data": [ { "id": 1, "label": "Test One Label" }, { "id": 2, "label": "Test Two Label" } ]}
  ```

10. Update `index.html:11` to handle the response correctly. Save the file and refresh the page

11. Click _**Make Ajax Request**_ button again

  Our code should now iterate through the `response.data` array and show our items
