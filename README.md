WireMock - Best mate to deliver TDD: Case of study
==================================================

Introduction
------------
This project consist only to provide an example of usage of Wire-Mock
This project is HEAVELY inspired by the following project in [git](https://github.com/tomakehurst/wiremock/tree/master/sample-war/src/main/webapp/WEB-INF)

This project is a use case. For more details and deep technical know-how please refer to the previous link provided.

Credit
------
Thanks to [Tom Akehurst](http://www.tomakehurst.com/) for the shared project that helped me to prepare this mcok.

What is about?
------------
Imagine that you are a qa, working in company and whish to deliver tests int TDD style. This became quickly aproblematic as it is very difficult to check if your tests are checking the correct information(s) or not.
A quick win is to deploy a simulator that will provide for you interactions as they are supposed to be delivered by dev team.
The current project assume that the dev team(s) is/are working hard to deliver api for [petsore](http://petstore.swagger.io/)

Imagine that your job is to provide tests for the following endpoints:
-	POST /pet to create a new pet with the following body
	```
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
	
	```
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
```

-	GET /pet/{petId} Find pet by ID and the response is looking like the following payload
	
	```
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

How it is structured?
---------------------

```
mock
├── README.md
└── wiremock
    ├── pom.xml
    └──  src
        └── main
            ├── java
            └── webapp
                └── WEB-INF
                    ├── petstore
                    │   ├── __files
                    │   │   ├── available_status.json
                    │   │   ├── bad_id.json
                    │   │   ├── create_pet1.json
                    │   │   ├── create_pet2.json
                    │   │   ├── create_pet_badBody.json
                    │   │   ├── create_pet.json
                    │   │   ├── get_pet.json
                    │   │   ├── pending_status.json
                    │   │   ├── pet_does_not_exist.json
                    │   │   └── sold_status.json
                    │   └── mappings
                    │       ├── available_status.json
                    │       ├── bad_id.json
                    │       ├── create_pet1.json
                    │       ├── create_pet2.json
                    │       ├── create_pet_badBody.json
                    │       ├── create_pet.json
                    │       ├── get_pet.json
                    │       ├── pending_status.json
                    │       ├── pet_does_not_exist.json
                    │       └── sold_status.json
                    └── web.xml
```

`__files` contains the request responses.
`mappings` contain the request structure.

to start the mock server:
```
mvn clean install
mvn jetty:run
```

if all good without error, start browser

```
http://localhost:8008/__admin/
```

Describe all available endpoints.
For example, to list all available annimals you can perform GET request were status is set to availavle all you need to do is (using postman, jmeter or whatever tool you want) you perform

```
GET http://localhost:8008/v2/pet/findByStatus?status=available
```

will return all available pets set in `__files/available_status.json` file.
To stop server run

```
mvn jetty:stop
```

the list of endpoint are:

```
GET http://localhost:8008/v2/pet/findByStatus?status=available
GET http://localhost:8008/v2/pet/findByStatus?status=pending
GET http://localhost:8008/v2/pet/findByStatus?status=sold
GET http://localhost:8008/v2/pet/1-123 -->bad id
GET http://localhost:8008/v2/pet/1507556867977 -->good id
GET http://localhost:8008/v2/pet/7357550131108011980 --> pet does not exist
POST http://localhost:8008/v2/pet --> With body request as it is defined in the [mappings/{create_pet_badBody.json, create_pet.json, create_pet1.json, create_pet2.json}]
```

the request response as it has been mentioned previousley are referenced in the `__files/*` and specified in the `mappinngs/*` files.

Conclusion
----------
As it has been said, I am not re-invinting the wheel, it is just an example to quickly pick up the wiremock server technology and help my qa mates to quickly implement their test and deliver them in TDD style.

Questions and Issues
--------------------
question, bug, clarification please refer to:
[WireMock mailing list](https://groups.google.com/forum/#!forum/wiremock-user).


