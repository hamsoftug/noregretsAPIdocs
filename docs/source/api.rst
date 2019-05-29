API
===
.. meta::
   :description: Send and Access your SMS , Create USERS Lists , Groups and configure WEBHOOKS using a RESTful API .
   :keywords: SMS,Receivers,senders,events,Lists,Groups,contacts,Bulk SMS, Delivery Reports , Feedback

Send and Access your SMS , Create USERS Lists , Groups and configure WEBHOOKS using a RESTful API . 
Noregrets provides a RESTful API. Below are the API Endpoints you can use;

Authorization
"""""""""""""
To access the API, you first need to copy your Api Key. Go to https://noregrets.ug/#get_started create an account and login, on the left navigation menu next to the profile avatar image and  then click **Get API **. Upon Activation then Click on **Go to API Console ** In the Console click on your profile and and copy your API Key.

.. NOTE:: Insert your API Key directly into the authorization header on any API requests. Example below;

.. code-block:: shell

  curl -X GET 
  -H "Authorization: Key <api_key>" 
  -H "Content-Type: application/json"
  "https://{endpoint}/api/v1/messages"

Authentication Errors
"""""""""""""""""""""
If the apiKey is invalid or expired you will receive a response with the status code set to **HTTP 401 Unauthorized**.

If the access_token is valid but you don't have enough scope to perform this request you will receive a response with the status code set to **HTTP 403 Forbidden**.

HTTP-Codes
"""""""""""
Actions and errors yield different HTTP response codes.  
Please have a look at the expected response codes in the following list.

 - ``200`` Request OK
 - ``201`` New resource created
 - ``304`` The resource has not been changed
 - ``400`` The request parameters are invalid
 - ``401`` The  provided api key is invalid
 - ``403`` You do not possess the required rights to access this resource.
 - ``404`` The resource could not be found / is unknown.
 - ``415`` The data could not be processed or the accept header is invalid.
 - ``422`` Could not save the entity
 - ``500`` An unexpected condition was encountered
 - ``503`` The server is not available (maintenance work).

HTTP-Headers
""""""""""""
.. ATTENTION:: You must provide the following headers in each request:

+---------------+---------------------+-----------------------------------------------------+
| Header        | Valid Values        | Description                                         |
+===============+=====================+=====================================================+
| Accept        | application/json    | API Format                                          |
+---------------+---------------------+-----------------------------------------------------+
| Authorization | Key $ApiKey | Replace with your API Key                      |
+---------------+---------------------+-----------------------------------------------------+

Messages
""""""""""""

``POST`` - /api/v1/add-message
-------------------------------
Send a new message

.. code-block:: shell

  POST /api/v1/add-message
  Accept: application/json
  Authorization: Key $ApiKey

Parameters
^^^^^^^^^^

+---------------+------------+-----------------------------------------------------+
| Name          | Required   | Description                                         |
+===============+============+=====================================================+
| sender_no     | required   | the phone number routing the SMS through            |
+---------------+------------+-----------------------------------------------------+
| receiver      | required   | the phone number of the person receving             |
+---------------+------------+-----------------------------------------------------+
| message       | required   | the content of the message being sent               |
+---------------+------------+-----------------------------------------------------+

Sample Code
^^^^^^^^^^
.. code-block:: php
 

Sample Response
^^^^^^^^^^^^^^^
.. code-block:: json

{"status":false,"message":""} 



``GET`` - /api/v1/users/{id}
-------------------------------
Get invoice information

.. code-block:: shell

  GET /api/v1/users/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken
  
  
Sample Code
^^^^^^^^^^
.. code-block:: php

<?php $curl = curl_init();
curl_setopt_array($curl, array(
  CURLOPT_URL => "http://api.noregrets.ug/V1/users?key=8g80kg4swkk00wwsggg4w48c408sk08048w0s84o",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => "",
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 30,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_SSL_VERIFYHOST => 0,
  CURLOPT_SSL_VERIFYPEER => 0,
));

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
} 
 ?> 

Sample Response
^^^^^^^^^^^^^^^
.. code-block:: json

  [
  {
    "m_number": "UN47102220",
    "lastname": "Stephen Barungi",
    "firstname": "",
    "other_names": "",
    "gender": "N/A",
    "contacts": [
      {
        "contact": "barungisteven@gmail.com"
      },
      {
        "contact": "+256755168219"
      }
    ]
  },
  {
    "m_number": "DV1088633736",
    "lastname": "steve",
    "firstname": "baros",
    "other_names": "",
    "gender": "",
    "contacts": [
      {
        "contact": "sbarungi@cis.mak.ac.ug"
      }
    ]
  }
]



``PUT`` - /api/v1/users/{id}
-------------------------------
Update an invoice

.. code-block:: shell

  PUT /api/v1/users/{id}
  Accept: application/json
  Authorization: ApiKey $AccessToken

Parameters
^^^^^^^^^^

+---------------+------------+-----------------------------------------------------+
| Name          | Required   | Description                                         |
+===============+============+=====================================================+
| id            | required   | Invoice ID                                          |
+---------------+------------+-----------------------------------------------------+
| reference_no  | optional   | Invoice reference code                              |
+---------------+------------+-----------------------------------------------------+
| title         | optional   | Invoice title                                       |
+---------------+------------+-----------------------------------------------------+
| client_id     | required   | Invoice client ID                                   |
+---------------+------------+-----------------------------------------------------+


``DELETE`` - /api/v1/invoices/{id}
----------------------------------
Delete invoice

.. code-block:: shell

  DELETE /api/v1/invoices/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

``GET`` - /api/v1/invoices
----------------------------------------
Get a list of all invoices

.. code-block:: shell

  GET /api/v1/invoices
  Accept: application/json
  Authorization: Key $AccessToken

``GET`` - /api/v1/invoices/{id}/payments
----------------------------------------


Get al Groups

.. code-block:: shell

  GET /api/v1/groups/{id}/
  Accept: application/json
  Authorization: Key $ApiKey

``GET`` - /api/v1/invoices/{id}/comments
----------------------------------------
Show invoice comments

.. code-block:: shell

  GET /api/v1/invoices/{id}/comments
  Accept: application/json
  Authorization: Key $AccessToken

``GET`` - /api/v1/invoices/{id}/items
--------------------------------------
Show invoice product lines

.. code-block:: shell

  GET /api/v1/invoices/{id}/items
  Accept: application/json
  Authorization: Key $AccessToken


Expenses
"""""""""""""""""

``POST`` - /api/v1/groups
-------------------------------
Create a new group

.. code-block:: shell

  POST /api/v1/expenses
  Accept: application/json
  Authorization: Key $ApiKey

Parameters
^^^^^^^^^^

+---------------+------------+-----------------------------------------------------+
| Name          | Required   | Description or name of the group                    |
+===============+============+=====================================================+
| amount        | required   | Expense amount e.g 1500.00                          |
+---------------+------------+-----------------------------------------------------+

``GET`` - /api/v1/groups/{id}
--------------------------------
Get Group information

.. code-block:: shell

  GET /api/v1/groups/{id}
  Accept: application/json
  Authorization: Key $ApiKey

Sample Response
^^^^^^^^^^^^^^^^
.. code-block:: json

  {
    
    "status": "true",
	"message": "succees",
    "data": {
        "group_id": 10,
        "code": "EXP-AC0010",
        "group_name": "Schools",
        "created_at": "2018-12-24T05:30:44+03:00",
        "updated_at": "2018-12-24T05:30:44+03:00"
    }
  }



Clients
"""""""""""""""""

``POST`` - /api/v1/clients
-------------------------------
Create a new client

.. code-block:: shell

  POST /api/v1/clients
  Accept: application/json
  Authorization: Bearer $AccessToken

Parameters
^^^^^^^^^^
+---------------+------------+-----------------------------------------------------+
| Name          | Required   | Description                                         |
+===============+============+=====================================================+
| name          | required   | Client Name                                         |
+---------------+------------+-----------------------------------------------------+
| email         | required   | Client email address                                |
+---------------+------------+-----------------------------------------------------+
| contact_email | required   | Contact email address                               |
+---------------+------------+-----------------------------------------------------+
| phone         | optional   | Client phone number                                 |
+---------------+------------+-----------------------------------------------------+
| address1      | optional   | Address                                             |
+---------------+------------+-----------------------------------------------------+
| zip_code      | optional   | Zip Code                                            |
+---------------+------------+-----------------------------------------------------+
| city          | optional   | City                                                |
+---------------+------------+-----------------------------------------------------+
| state         | optional   | State                                               |
+---------------+------------+-----------------------------------------------------+
| locale        | optional   | Preferred locale                                    |
+---------------+------------+-----------------------------------------------------+
| country       | optional   | Country                                             |
+---------------+------------+-----------------------------------------------------+
| tax_number    | optional   | Client tax number if any                            |
+---------------+------------+-----------------------------------------------------+
| currency      | optional   | Preferred currency                                  |
+---------------+------------+-----------------------------------------------------+
| website       | required   | Client website URL                                  |
+---------------+------------+-----------------------------------------------------+
| facebook      | required   | Client facebook link                                |
+---------------+------------+-----------------------------------------------------+
| twitter       | optional   | Twitter account URL                                 |
+---------------+------------+-----------------------------------------------------+
| skype         | optional   | Skype address                                       |
+---------------+------------+-----------------------------------------------------+
| linkedin      | optional   | LinkedIn profile                                    |
+---------------+------------+-----------------------------------------------------+
| notes         | optional   | Additional notes                                    |
+---------------+------------+-----------------------------------------------------+
| tags[]        | optional   | Array list of tags e.g ``tags[design]``             |
+------------------+------------+--------------------------------------------------+

``GET`` - /api/v1/clients/{id}
--------------------------------
Get client information

.. code-block:: shell

  GET /api/v1/clients/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

Sample Response
^^^^^^^^^^^^^^^^
.. code-block:: json

  {
    "type": "clients",
    "id": "100",
    "attributes": {
        "id": 100,
        "name": "Greenholt-Harris",
        "code": "COM00100",
        "email": "mclaughlin.jason@example.net",
        "contact": {
            "id": 1,
            "email": "admin@example.com",
            "name": "William Mandai"
        },
        "address": {
            "address1": "402 Reynolds Trace\nNorth Lutherchester, SD 94456-5868",
            "address2": null,
            "city": "East Geo",
            "state": null,
            "zipcode": null,
            "country": "Peru"
        },
        "website": "https://hartmann.com",
        "phone": null,
        "mobile": null,
        "tax_number": null,
        "currency": "USD",
        "expense": "0.00",
        "balance": "0.00",
        "paid": "0.00",
        "social": {
            "skype": null,
            "facebook": null,
            "twitter": null,
            "linkedin": null
        },
        "notes": "Neque veritatis pariatur ut voluptatum. Qui officia molestias distinctio dicta quibusdam. Amet et adipisci ad eveniet.",
        "logo": "/storage/logos/tux_droid_1.jpg",
        "unsubscribed_at": null,
        "created_at": "2018-12-24T05:30:17+03:00",
        "updated_at": "2018-12-24T05:30:17+03:00"
    }
  }


``PUT`` - /api/v1/clients/{id}
--------------------------------
Update client information

.. code-block:: shell

  PUT /api/v1/clients/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

Parameters
^^^^^^^^^^
.. TIP:: Same as the create new client API parameters

``DELETE`` - /api/v1/clients/{id}
-----------------------------------
Delete a client

.. code-block:: shell

  DELETE /api/v1/clients/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

``GET`` - /api/v1/clients
----------------------------------------
Get a list of all clients

.. code-block:: shell

  GET /api/v1/clients
  Accept: application/json
  Authorization: Bearer $AccessToken

``GET`` - /api/v1/clients/{id}/contacts
------------------------------------------
Show client contacts

.. code-block:: shell

  GET /api/v1/clients/{id}/contacts
  Accept: application/json
  Authorization: Bearer $AccessToken


``GET`` - /api/v1/clients/{id}/projects
----------------------------------------
Show client projects

.. code-block:: shell

  GET /api/v1/clients/{id}/projects
  Accept: application/json
  Authorization: Bearer $AccessToken

``GET`` - /api/v1/clients/{id}/invoices
------------------------------------------
Show client invoices

.. code-block:: shell

  GET /api/v1/clients/{id}/invoices
  Accept: application/json
  Authorization: Bearer $AccessToken

``GET`` - /api/v1/clients/{id}/estimates
------------------------------------------
Show client estimates

.. code-block:: shell

  GET /api/v1/clients/{id}/estimates
  Accept: application/json
  Authorization: Bearer $AccessToken

``GET`` - /api/v1/clients/{id}/payments
------------------------------------------
Show client payments

.. code-block:: shell

  GET /api/v1/clients/{id}/payments
  Accept: application/json
  Authorization: Bearer $AccessToken

``GET`` - /api/v1/clients/{id}/subscriptions
---------------------------------------------
Show client subscriptions

.. code-block:: shell

  GET /api/v1/clients/{id}/subscriptions
  Accept: application/json
  Authorization: Bearer $AccessToken

``GET`` - /api/v1/clients/{id}/expenses
------------------------------------------
Show client expenses

.. code-block:: shell

  GET /api/v1/clients/{id}/expenses
  Accept: application/json
  Authorization: Bearer $AccessToken

``GET`` - /api/v1/clients/{id}/deals
------------------------------------------
Show organization deals

.. code-block:: shell

  GET /api/v1/clients/{id}/deals
  Accept: application/json
  Authorization: Bearer $AccessToken


Contacts
"""""""""""""""""

``POST`` - /api/v1/contacts
-------------------------------
Create a new contact

.. code-block:: shell

  POST /api/v1/contacts
  Accept: application/json
  Authorization: Key $ApiKey

Parameters
^^^^^^^^^^
+---------------+------------+-----------------------------------------------------+
| Name          | Required   | Description                                         |
+===============+============+=====================================================+
| name          | required   | Contact Name                                        |
+---------------+------------+-----------------------------------------------------+
| email         | required   | Contact email address                               |
+---------------+------------+-----------------------------------------------------+
| phone         | optional   | Contact Phone Number                                |
+---------------+------------+-----------------------------------------------------+

``GET`` - /api/v1/contacts/{id}
--------------------------------
Get contact information

.. code-block:: shell

  GET /api/v1/contacts/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

Sample Response
^^^^^^^^^^^^^^^^
.. code-block:: json

  {
    "type": "contacts",
    "id": "10",
    "attributes": {
        "id": 10,
        "name": "Johnathan Yundt I",
        "job_title": "Floral Designer",
        "email": "mackenzie46@example.org",
        "avatar": "/storage/avatars/avatar9.png",
        "city": null,
        "country": null,
        "website": null,
        "hourly_rate": "17.00",
        "business": {
            "id": 6,
            "name": "Turcotte, Buckridge and Herman",
            "contact_person": "luna66@example.net",
            "currency": "USD",
            "balance": "0.00",
            "expense": "0.00",
            "paid": "0.00"
        },
        "created_at": "2018-12-24T05:30:09+03:00",
        "updated_at": "2018-12-24T05:30:16+03:00"
    }
  }


``PUT`` - /api/v1/contacts/{id}
--------------------------------
Update contact information

.. code-block:: shell

  PUT /api/v1/contacts/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

Parameters
^^^^^^^^^^
.. TIP:: Same as the create contact API parameters

``DELETE`` - /api/v1/contacts/{id}
-----------------------------------
Delete a contact

.. code-block:: shell

  DELETE /api/v1/contacts/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

``GET`` - /api/v1/contacts
----------------------------------------
Get a list of all contacts

.. code-block:: shell

  GET /api/v1/contacts
  Accept: application/json
  Authorization: Bearer $AccessToken

