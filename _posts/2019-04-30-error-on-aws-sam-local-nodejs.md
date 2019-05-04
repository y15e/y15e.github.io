---
layout: post
title: "Error on AWS SAM local Node.js runtime"
---

AWS SAM sample Node.js application doesn't work on my Arch Linux environment.

* OS: Arch Linux 4.19.37-1-lts
* SAM version: 0.15.0
* Docker version: 18.09.5-ce, build e8ff056dbc

The error can be reproduced with following steps.

1. Initialize a sample Node.js application.

   ```
   $ sam init --runtime nodejs
   [+] Initializing project structure...
   
   Project generated: ./sam-app
   
   Steps you can take next within the project folder
   ===================================================
   [*] Invoke Function: sam local invoke HelloWorldFunction --event event.json
   [*] Start API Gateway locally: sam local start-api
   
   Read sam-app/README.md for further instructions
   
   [*] Project initialization is now complete
   ```
   
2. Start local api.

   ```
   $ cd sam-app
   $ sam local start-api
   2019-04-30 17:58:36 Found credentials in shared credentials file: ~/.aws/credentials
   2019-04-30 17:58:36 Mounting HelloWorldFunction at http://127.0.0.1:3000/hello [GET]
   2019-04-30 17:58:36 You can now browse to the above endpoints to invoke your functions. You do not need to restart/reload SAM CLI while working on your functions, changes will be reflected instantly/automatically. You only need to restart SAM CLI if you update your AWS SAM template
   2019-04-30 17:58:36  * Running on http://127.0.0.1:3000/ (Press CTRL+C to quit)
   ```
   
3. Make a http request to **http://127.0.0.1:3000/hello** with curl in another terminal. The response is "*Internal server error*".

   ```
   $ curl http://127.0.0.1:3000/hello
   {"message":"Internal server error"}
   ```
   
4. A 502 error is recorded in the server log.

   ```
   2019-04-30 17:59:20 Invoking app.lambdaHandler (nodejs8.10)
   
   Fetching lambci/lambda:nodejs8.10 Docker container image......
   2019-04-30 17:59:22 Mounting /var/work/sam-app/hello-world as /var/task:ro,delegated inside runtime container
   2019-04-30 17:59:30 Function returned an invalid response (must include one of: body, headers or statusCode in the response object). Response received: 
   2019-04-30 17:59:30 127.0.0.1 - - [30/Apr/2019 17:59:30] "GET /hello HTTP/1.1" 502 -
   ```
   
# Workaround:

I was able to solve the issue by installing Node.js 8.10 via yum during docker image build phase and using `/usr/bin/node` instead of original `/var/lang/bin/node`.

[Changes in the Dockerfile](https://github.com/y15e/docker-lambda/commit/3ec7f0fe8086b6fdcd15c92b9976b91072108f3f)
![AWS Lambda Node.js 8.10](/assets/img/aws-lambda-nodejs.png)

1. You can build above modified docker image by following steps.

   ```
   $ git clone git@github.com:y15e/docker-lambda.git
   $ cd docker-lambda/nodejs8.10/run
   $ docker build -t lambci/lambda:nodejs8.10 .
   ```

2. Run `sam local start-api` with `--skip-pull-image` option. Don't forget `--skip-pull-image` option otherwise the original docker image will be downloaded and the above changes will be reverted.

   ```
   $ cd sam-app
   $ sam local start-api --skip-pull-image
   ```

3. Make a http request with curl, then you can see the correct response.

   ```
   $ curl http://127.0.0.1:3000/hello
   {"message":"hello world"}
   ```

Before I found above workaround, I tried following things but the issue wasn't solved.

* Tried non LTS version of Arch Linux.
* Tried Ubuntu server.
* Tried MX Linux.
* Downgraded docker version.

  ```
  $ yum downgrade glibc-2.17-196.172.amzn1.x86_64 glibc-common-2.17-196.172.amzn1.x86_64
  ```
