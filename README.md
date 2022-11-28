# API Analytics

A lightweight API analytics solution, complete with a dashboard.

Currently available for:
 - Python: <b>Flask</b> and <b>FastAPI</b>
 - Node.js: <b>Express</b> and <b>Fastify</b>
 - Go: <b>Gin</b>

## Getting Started

### 1. Generate an API key

Head to https://my-api-analytics.vercel.app/generate to generate your unique API key with a single click. This key is used to monitor your specific API, so keep it secret! It's also required in order to view your APIs analytics dashboard.

### 2. Add middleware to your API

Add our lightweight middleware to your API. Almost all processing is handled by our servers so there should be virtually no impact on your APIs performance.

#### FastAPI

```bash
pip install api-analytics
```

```py
from fastapi import FastAPI
from api_analytics.fastapi import Analytics

app = FastAPI()
app.add_middleware(Analytics, api_key=<api_key>)

@app.get("/")
async def root():
    return {"message": "Hello World!"}
```

#### Flask

```bash
pip install api-analytics
```

```py
from flask import Flask
from api_analytics.flask import add_middleware

app = Flask(__name__)
add_middleware(app, <api_key>)

@app.get("/")
def root():
    return {"message": "Hello World!"}
```

#### Express

```bash
npm i node-api-analytics
```

```js
import express from 'express';
import { expressAnalytics } from 'node-api-analytics';

const app = express()

app.use(analytics(<api_key>))

app.get("/", (req, res) => {
    res.send({message: "Hello World"});
});

app.listen(8080, () => {
    console.log('Server listening at http://localhost:8080');
})
```

#### Fastify

```bash
npm i node-api-analytics
```

```js
import Fastify from 'fastify';
import { fastifyAnalytics } from 'node-api-analytics;

const fastify = Fastify({
  logger: true,
})

fastify.addHook('onRequest', fastifyAnalytics(<api_key>));

fastify.get('/', function (request, reply) {
  reply.send({ message: 'Hello World!' });
})

fastify.listen({ port: 8080 }, function (err, address) {
  console.log('Server listening at http://localhost:8080')
  if (err) {
    fastify.log.error(err);
    process.exit(1);
  }
})
```

#### Koa

```bash
npm i node-api-analytics
```

```js
import Koa from "koa";
import { koaAnalytics } from "node-api-analytics";

const app = new Koa();

app.use(koaAnalytics(<api_key>));

app.use((ctx) => {
  ctx.body = { message: "Hello World!" };
});

app.listen(8080, () =>
  console.log('Server listening at https://localhost:8080')
);
```

#### Gin

```bash
go get -u github.com/tom-draper/api-analytics/analytics/go
```

```go
package main

import (
	analytics "github.com/tom-draper/api-analytics/analytics/go"
	"net/http"

	"github.com/gin-gonic/gin"
)

func root(c *gin.Context) {
	jsonData := []byte(`{"message": "Hello World!"}`)
	c.Data(http.StatusOK, "application/json", jsonData)
}

func main() {
	router := gin.Default()
	
	router.Use(analytics.Analytics(<api_key>))

	router.GET("/", root)
	router.Run("localhost:8080")
}
```

### 3. View your analytics

Your API will log requests on all valid routes. Head over to https://my-api-analytics.vercel.app/dashboard and paste in your API key to view your dashboard.

## Data and Security

All data is stored securely in compliance with The EU General Data Protection Regulation (GDPR).

For any given request to your API, data recorded is limited to:
 - API hostname
 - Path requested by user
 - User's operating system
 - User's browser
 - Request method (GET, POST, PUT, etc.)
 - Time of request
 - Status code
 - Response time
 - API framework (FastAPI, Flask, etc.)

Data collected is only used by the analytics dashboard.

When using API Analytics to collect analytics for your API, you are anonymous, with the API key the only link between you and you API's analytics. Should you lose your API key, you will have no method to access your API analytics.

You can use the same API key across multiple APIs, but all your data will appear in the same dashboard.
