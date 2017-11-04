WireMock - Best mate to deliver TDD: Case of study
==================================================

Introduction
------------
This project consist only to provide an example of usage of Wire-Mock
This project is HEAVELY inspired by the following project in [git](https://github.com/tomakehurst/wiremock/tree/master/sample-war/src/main/webapp/WEB-INF)

This project is a use case. For more details and deep technical know how please refer to the previous link provided.

Credit
------
Thanks to [Tom Akehurst](http://www.tomakehurst.com/) for his shared project that helped me to prepare this mcok.

What is about?
------------
Imagine that you are a qa, working in company and whish to deliver tests int TDD style. This became quickly aproblematic as it is very difficult to check if your tests are checking the correct information(s) or not.
A quick win is to deploy a simulator that will provide for you interactions as they are supposed to be delivered by dev team.
The current project assume that the dev team(s) is/are working hard to deliver api for [petsore](http://petstore.swagger.io/)

Imagine that your job is to provide tests for the following endpoints:
-	POST /pet to create a new pet with the following body
	```json
    {
      "id": 0,
      "category": {
        "id": 0,
        "name": "string"
      },
      "name": "doggie",
      "photoUrls": [
        "string"
      ],
      "tags": [
        {
          "id": 0,
          "name": "string"
        }
      ],
      "status": "available"
	}
```
-	GET /pet/findByStatus?status={available,pending,sold} will return results like the following
```json
   [{  
      "id":1507556953502,
      "category":{  
         "id":12,
         "name":"boxer"
      },
      "name":"Dixie",
      "photoUrls":[  
         "photoUrls",
         "url1",
         "url2",
         "url3"
      ],
      "tags":[  
         {  
            "id":11,
            "name":"calm"
         }
      ],
      "status":"available"
   }]
   ````
-	GET /pet/{petId} Find pet by ID and the response is looking like the following payload:
```json
    {  
       "id":1507556867977,
       "category":{  
          "id":12,
          "name":"boxer"
       },
       "name":"Dixie",
       "photoUrls":[  
          "photoUrls",
          "url1",
          "url2",
          "url3"
       ],
       "tags":[  
          {  
             "id":11,
             "name":"calm"
          }
       ],
       "status":"available"
}
```
To answer the question what is about? this is simply a try to provide an example of mocked server that provide such answers.

PS: Full documentation can be found at [wiremock.org](http://wiremock.org/ "wiremock.org")



Questions and Issues
--------------------
If you have a question about WireMock, or are experiencing a problem you're not sure is a bug please post a message to the
[WireMock mailing list](https://groups.google.com/forum/#!forum/wiremock-user).

On the other hand if you're pretty certain you've found a bug please open an issue.

Contributing
------------
We welcome bug fixes and new features in the form of pull requests. If you'd like to contribute, please be mindful of the
following guidelines:
* All changes should include suitable tests, whether to demonstrate the bug or exercise and document the new feature.
* Please make one change per pull request.
* If the new feature is significantly large/complex/breaks existing behaviour, please first post a summary of your idea
on the mailing list to generate a discussion. This will avoid significant amounts of coding time spent on changes that ultimately get rejected.
* Try to avoid reformats of files that change the indentation, tabs to spaces etc., as this makes reviewing diffs much
more difficult.

Building WireMock locally
-------------------------
To run all of WireMock's tests:
```bash
./gradlew clean test
```

To build both JARs (thin and standalone):
```bash
./gradlew jar shadowJar
```

The built JARs will be placed under ``build/libs``.
