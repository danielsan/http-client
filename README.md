# promise-data-to
This is a helper to perform POST requests using promises.

## Install
```sh
npm install @everymundo/promise-data-to
```

## Usage
### POST some data
```js
const httpClient = require('@everymundo/http-client')

const headers = { 'content-type': 'application/json' }
const endpoint = new httpClient.PostEndpoint('http://your-host.com/path', headers)
const data = { myData:'Something' }

const res = await httpClient.promiseDataTo(endpoint, data)
// OR
const res = await httpClient.promisePost(endpoint, data)
// OR
const res = await httpClient.post(endpoint, data)
```

### GET some data
```js
const httpClient = require('@everymundo/http-client')

const headers = { 'authorization': 'your token' }
const endpoint = new httpClient.GetEndpoint('http://your-host.com/path', headers)

const res = await httpClient.promiseGet(endpoint)
// OR
const res = await httpClient.get(endpoint)
```

### POST using the Fetch API
```js
const httpClient = require('@everymundo/http-client')

const headers = { 'authorization': 'your token' }
const res = await httpClient.fetch('http://your-host.com/path', { headers, body: data })
```

### HEAD request
```js
const httpClient = require('@everymundo/http-client')

const headers = { 'authorization': 'your token' }
const res = httpClient.head('http://your-host.com/path', { headers })
```

### GET using the Fetch API
```js
const { fetch } = require('@everymundo/http-client')

const headers = { 'authorization': 'your token' }
const res = await fetch('http://your-host.com/path', { headers })
```


### HEAD using the Fetch API
```js
const { fetch } = require('@everymundo/http-client')

const headers = { 'authorization': 'your token' }
const res = await fetch('http://your-host.com/path', { headers })
```

## Response Schema
```js
{
    statusCode, // the response statusCode
    code, // alias for statusCode [for backaward compatibility]
    err,
    method, // Request Method
    start, // Date Object captured right before starting the request
    end: Date.now(), // Int Timestamp from when the request has finished
    attempt, // the number of attempts of the retries
    endpoint, // the endpoint object either passed or generated from a string
    resTxt, // alias for responseText [for backaward compatibility]
    responseText, // the response buffer.toString()
    buffer, // uncompressed responseBuffer if that one is compressed, otherwise, responseBuffer 
    responseBuffer, // raw response buffer
    dataType, // the name of the constructor of the posted data [Array, Object, String, Buffer]
    dataLen, // when posting arrays it shows the number of array items posted
    compress, // the type of compression for the POST request, if any. Valid values are gzip and deflate
    requestHeaders, // the headers used on the request
    responseHeaders // the headers received from the remote server
}
```

## Some Features
* Automatically retries to send the requests when statusCode > 399
