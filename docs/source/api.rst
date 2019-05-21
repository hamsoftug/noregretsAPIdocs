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
If the bearer token is invalid or expired you will receive a response with the status code set to **HTTP 401 Unauthorized**.

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

Invoices
""""""""""""

``POST`` - /api/v1/invoices
-------------------------------
Create new invoice

.. code-block:: shell

  POST /api/v1/invoices
  Accept: application/json
  Authorization: Bearer $AccessToken

Parameters
^^^^^^^^^^

+---------------+------------+-----------------------------------------------------+
| Name          | Required   | Description                                         |
+===============+============+=====================================================+
| reference_no  | optional   | Invoice reference code                              |
+---------------+------------+-----------------------------------------------------+
| title         | optional   | Invoice title                                       |
+---------------+------------+-----------------------------------------------------+
| client_id     | required   | Invoice client ID                                   |
+---------------+------------+-----------------------------------------------------+
| due_date      | required   | Invoice due date                                    |
+---------------+------------+-----------------------------------------------------+
| currency      | required   | Invoice currency                                    |
+---------------+------------+-----------------------------------------------------+
| notes         | optional   | Invoice notes                                       |
+---------------+------------+-----------------------------------------------------+
| tax           | optional   | Invoice tax 1 percentage                            |
+---------------+------------+-----------------------------------------------------+
| tax2          | optional   | Invoice tax 2 percentage                            |
+---------------+------------+-----------------------------------------------------+
| extra_fee     | optional   | Invoice extra fee percentage                        |
+---------------+------------+-----------------------------------------------------+
| discount      | optional   | Invoice discount percentage                         |
+---------------+------------+-----------------------------------------------------+
| project_id    | optional   | Project ID related to invoic                        |
+---------------+------------+-----------------------------------------------------+
| is_visible    | optional   | Set to 0 to hide invoice from client                |
+---------------+------------+-----------------------------------------------------+
| line_items[]  | optional   | Array of invoice items                              |
+---------------+------------+-----------------------------------------------------+
| tags[]        | optional   | Array list of tags e.g ``tags[design]``             |
+---------------+------------+-----------------------------------------------------+

``GET`` - /api/v1/users/{id}
-------------------------------
Get invoice information

.. code-block:: shell

  GET /api/v1/users/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

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
Show invoice payments

.. code-block:: shell

  GET /api/v1/invoices/{id}/payments
  Accept: application/json
  Authorization: Key $AccessToken

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

``POST`` - /api/v1/expenses
-------------------------------
Create a new expense

.. code-block:: shell

  POST /api/v1/expenses
  Accept: application/json
  Authorization: Bearer $AccessToken

Parameters
^^^^^^^^^^

+---------------+------------+-----------------------------------------------------+
| Name          | Required   | Description                                         |
+===============+============+=====================================================+
| amount        | required   | Expense amount e.g 1500.00                          |
+---------------+------------+-----------------------------------------------------+
| category      | required   | Expense category                                    |
+---------------+------------+-----------------------------------------------------+
| expense_date  | required   | Expense date                                        |
+---------------+------------+-----------------------------------------------------+
| tax           | required   | Tax 1 percentage                                    |
+---------------+------------+-----------------------------------------------------+
| tax2          | required   | Tax 2 percentage                                    |
+---------------+------------+-----------------------------------------------------+
| currency      | optional   | Expense Currency                                    |
+---------------+------------+-----------------------------------------------------+
| billable      | optional   | Whether the expense is billable. Default 1          |
+---------------+------------+-----------------------------------------------------+
| notes         | optional   | Expense notes                                       |
+---------------+------------+-----------------------------------------------------+
| project_id    | optional   | Associated project ID if any                        |
+---------------+------------+-----------------------------------------------------+
| client_id     | optional   | Associated client ID if any                         |
+---------------+------------+-----------------------------------------------------+
| vendor        | optional   | Associated vendor name                              |
+---------------+------------+-----------------------------------------------------+
| is_visible    | optional   | Show/Hide expense from client. Default 0            |
+---------------+------------+-----------------------------------------------------+
| tags[]        | optional   | Array list of tags e.g ``tags[design]``             |
+---------------+------------+-----------------------------------------------------+

``GET`` - /api/v1/expenses/{id}
--------------------------------
Get expense information

.. code-block:: shell

  GET /api/v1/expenses/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

Sample Response
^^^^^^^^^^^^^^^^
.. code-block:: json

  {
    "type": "expenses",
    "id": "10",
    "attributes": {
        "id": 10,
        "code": "EXP-AC0010",
        "amount": "222.04",
        "before_tax": "0.00",
        "currency": "USD",
        "billable": 1,
        "category": 47,
        "vendor": "Feil and Sons",
        "tax": "0.95",
        "tax2": null,
        "taxed": null,
        "expense_date": "2018-12-24T00:00:00+03:00",
        "billed": false,
        "project_id": 1,
        "client_id": 2,
        "invoiced_id": null,
        "is_recurring": 0,
        "frequency": null,
        "next_recur_date": null,
        "recur_starts": null,
        "recur_ends": null,
        "exchange_rate": "1.00000",
        "is_visible": 0,
        "notes": null,
        "user_id": 1,
        "created_at": "2018-12-24T05:30:44+03:00",
        "updated_at": "2018-12-24T05:30:44+03:00"
    }
  }


``PUT`` - /api/v1/expenses/{id}
--------------------------------
Update an expense

.. code-block:: shell

  PUT /api/v1/expenses/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

Parameters
^^^^^^^^^^

+---------------+------------+-----------------------------------------------------+
| Name          | Required   | Description                                         |
+===============+============+=====================================================+
| amount        | required   | Expense amount e.g 1500.00                          |
+---------------+------------+-----------------------------------------------------+
| category      | required   | Expense category                                    |
+---------------+------------+-----------------------------------------------------+
| expense_date  | required   | Expense date                                        |
+---------------+------------+-----------------------------------------------------+
| tax           | required   | Tax 1 percentage                                    |
+---------------+------------+-----------------------------------------------------+
| tax2          | required   | Tax 2 percentage                                    |
+---------------+------------+-----------------------------------------------------+
| currency      | optional   | Expense Currency                                    |
+---------------+------------+-----------------------------------------------------+
| billable      | optional   | Whether the expense is billable. Default 1          |
+---------------+------------+-----------------------------------------------------+
| notes         | optional   | Expense notes                                       |
+---------------+------------+-----------------------------------------------------+
| project_id    | optional   | Associated project ID if any                        |
+---------------+------------+-----------------------------------------------------+
| client_id     | optional   | Associated client ID if any                         |
+---------------+------------+-----------------------------------------------------+
| vendor        | optional   | Associated vendor name                              |
+---------------+------------+-----------------------------------------------------+
| is_visible    | optional   | Show/Hide expense from client. Default 0            |
+---------------+------------+-----------------------------------------------------+
| tags[]        | optional   | Array list of tags e.g ``tags[design]``             |
+---------------+------------+-----------------------------------------------------+

``DELETE`` - /api/v1/expenses/{id}
-----------------------------------
Delete an expense

.. code-block:: shell

  DELETE /api/v1/expenses/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

``GET`` - /api/v1/expenses
----------------------------------------
Get a list of all expenses

.. code-block:: shell

  GET /api/v1/expenses
  Accept: application/json
  Authorization: Bearer $AccessToken

``GET`` - /api/v1/expenses/{id}/comments
------------------------------------------
Show expense comments

.. code-block:: shell

  GET /api/v1/expenses/{id}/comments
  Accept: application/json
  Authorization: Bearer $AccessToken

``POST`` - /api/v1/expenses/{id}/copy
----------------------------------------
Duplicate expense

.. code-block:: shell

  POST /api/v1/expenses/{id}/copy
  Accept: application/json
  Authorization: Bearer $AccessToken

Parameters
^^^^^^^^^^

+---------------+------------+-----------------------------------------------------+
| Name          | Required   | Description                                         |
+===============+============+=====================================================+
| id            | required   | Expense ID                                          |
+---------------+------------+-----------------------------------------------------+


Payments
"""""""""""""""""

``POST`` - /api/v1/payments
-------------------------------
Create a new payment

.. code-block:: shell

  POST /api/v1/payments
  Accept: application/json
  Authorization: Bearer $AccessToken

Parameters
^^^^^^^^^^

+----------------+------------+-----------------------------------------------------+
| Name           | Required   | Description                                         |
+================+============+=====================================================+
| invoice_id     | required   | Invoice ID                                          |
+----------------+------------+-----------------------------------------------------+
| payment_date   | required   | Date when the payment was made                      |
+----------------+------------+-----------------------------------------------------+
| amount         | required   | Amount of payment made                              |
+----------------+------------+-----------------------------------------------------+
| payment_method | required   | Payment method ID                                   |
+----------------+------------+-----------------------------------------------------+
| gateway        | required   | ``Must be set to offline``                          |
+----------------+------------+-----------------------------------------------------+
| notes          | optional   | Payment additional notes                            |
+----------------+------------+-----------------------------------------------------+
| currency       | optional   | Payment Currency                                    |
+----------------+------------+-----------------------------------------------------+
| send_email     | optional   | If an email should be sent to client. Default 1     |
+----------------+------------+-----------------------------------------------------+

``GET`` - /api/v1/payments/{id}
--------------------------------
Get payment information

.. code-block:: shell

  GET /api/v1/payments/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

Sample Response
^^^^^^^^^^^^^^^^
.. code-block:: json

  {
    "type": "payments",
    "id": "10",
    "attributes": {
        "id": 10,
        "code": "PAY-20181224-0010",
        "invoice_id": 7,
        "payment_method": "Cash",
        "curreny": null,
        "amount": "73.68",
        "notes": null,
        "payment_date": "2018-12-19T05:30:31+03:00",
        "exchange_rate": "1.00000",
        "project_id": null,
        "refunded": 0,
        "archived_at": null,
        "business": {
            "id": 5,
            "name": "Rogahn-Gerhold",
            "contact_person": "wiza.samanta@example.org"
        },
        "created_at": "2018-12-24T05:30:31+03:00",
        "updated_at": "2018-12-24T05:30:31+03:00"
    }
  }


``PUT`` - /api/v1/payments/{id}
--------------------------------
Update a payment

.. code-block:: shell

  PUT /api/v1/payments/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

Parameters
^^^^^^^^^^

+----------------+------------+-----------------------------------------------------+
| Name           | Required   | Description                                         |
+================+============+=====================================================+
| invoice_id     | required   | Invoice ID                                          |
+----------------+------------+-----------------------------------------------------+
| payment_date   | required   | Date when the payment was made                      |
+----------------+------------+-----------------------------------------------------+
| amount         | required   | Amount of payment made                              |
+----------------+------------+-----------------------------------------------------+
| payment_method | required   | Payment method ID                                   |
+----------------+------------+-----------------------------------------------------+
| notes          | optional   | Payment additional notes                            |
+----------------+------------+-----------------------------------------------------+
| currency       | optional   | Payment Currency                                    |
+----------------+------------+-----------------------------------------------------+

``DELETE`` - /api/v1/payments/{id}
-----------------------------------
Delete a payment

.. code-block:: shell

  DELETE /api/v1/payments/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

``GET`` - /api/v1/payments
----------------------------------------
Get a list of all payments

.. code-block:: shell

  GET /api/v1/payments
  Accept: application/json
  Authorization: Bearer $AccessToken

``GET`` - /api/v1/payments/{id}/comments
------------------------------------------
Show estimate comments

.. code-block:: shell

  GET /api/v1/payments/{id}/comments
  Accept: application/json
  Authorization: Bearer $AccessToken

``POST`` - /api/v1/payments/{id}/refund
------------------------------------------
Mark a payment as refunded

.. code-block:: shell

  POST /api/v1/payments/{id}/refund
  Accept: application/json
  Authorization: Bearer $AccessToken


Contracts
"""""""""""""""""

``POST`` - /api/v1/contracts
-------------------------------
Create a new contracts

.. code-block:: shell

  POST /api/v1/contracts
  Accept: application/json
  Authorization: Bearer $AccessToken

Parameters
^^^^^^^^^^

+---------------------+------------+-----------------------------------------------------+
| Name                | Required   | Description                                         |
+=====================+============+=====================================================+
| contract_title      | required   | Contract title                                      |
+---------------------+------------+-----------------------------------------------------+
| client_id           | required   | Client associated with the contract                 |
+---------------------+------------+-----------------------------------------------------+
| start_date          | required   | Contract start date                                 |
+---------------------+------------+-----------------------------------------------------+
| end_date            | required   | Contract end date                                   |
+---------------------+------------+-----------------------------------------------------+
| expiry_date         | required   | Number of days before a contract expires. E.g 14    |
+---------------------+------------+-----------------------------------------------------+
| payment_terms       | optional   | Number of days. E.g 14                              |
+---------------------+------------+-----------------------------------------------------+
| currency            | optional   | Contract Currency                                   |
+---------------------+------------+-----------------------------------------------------+
| termination_notice  | optional   | Number of days to be notified before termination    |
+---------------------+------------+-----------------------------------------------------+
| rate_is_fixed       | optional   | If fixed rate. Default 0                            |
+---------------------+------------+-----------------------------------------------------+
| fixed_rate          | optional   | Contract fixed amount e.g 1500.00                   |
+---------------------+------------+-----------------------------------------------------+
| hourly_rate         | optional   | Contract hourly rate                                |
+---------------------+------------+-----------------------------------------------------+
| description         | optional   | Contract description                                |
+---------------------+------------+-----------------------------------------------------+
| license_owner       | optional   | Contract license owner. ``freelancer or client``    |
+---------------------+------------+-----------------------------------------------------+
| late_payment_fee    | optional   | Late payment fee                                    |
+---------------------+------------+-----------------------------------------------------+
| late_fee_percent    | optional   | If late payment is percentage. Default 1            |
+---------------------+------------+-----------------------------------------------------+
| cancelation_fee     | optional   | Contract cancellation fee                           |
+---------------------+------------+-----------------------------------------------------+
| is_visible          | optional   | Show/hide contract from client                      |
+---------------------+------------+-----------------------------------------------------+
| deposit_required    | optional   | Amount of deposit required. E.g 1500.00             |
+---------------------+------------+-----------------------------------------------------+
| services            | optional   | List of contract services. E.g Web Design, SEO      |
+---------------------+------------+-----------------------------------------------------+
| client_rights       | optional   | Rights granted to client                            |
+---------------------+------------+-----------------------------------------------------+
| portfolio_rights    | optional   | Right to include work in portfolio. Default 1       |
+---------------------+------------+-----------------------------------------------------+
| non_compete         | optional   | Add non-compete section. Default 1                  |
+---------------------+------------+-----------------------------------------------------+
| appropriate_conduct | optional   | Enable sexual harassment clause. Default 1          |
+---------------------+------------+-----------------------------------------------------+

``GET`` - /api/v1/contracts/{id}
--------------------------------
Get contract information

.. code-block:: shell

  GET /api/v1/contracts/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

Sample Response
^^^^^^^^^^^^^^^^
.. code-block:: json

  {
    "type": "contracts",
    "id": "10",
    "attributes": {
        "id": 10,
        "title": "Dare LLC Contract",
        "start_date": "2018-12-24T05:30:20+03:00",
        "end_date": "2019-01-08T05:30:20+03:00",
        "expiry_date": "2018-12-29T05:30:20+03:00",
        "rate_is_fixed": 0,
        "fixed_rate": null,
        "hourly_rate": "12.97",
        "currency": "USD",
        "license_owner": "client",
        "payment_terms": "6",
        "late_payment_fee": "0.00",
        "late_fee_percent": 1,
        "termination_notice": 12,
        "cancelation_fee": "11.19",
        "deposit_required": "0.00",
        "signed": 0,
        "services": "Beatae blanditiis ea commodi et tempore est.",
        "client_rights": "Qui culpa qui consequatur architecto nam officia. Minus nulla odio sapiente delectus ut. Dolore nemo reprehenderit dolore odit eum consequuntur. Voluptate nesciunt et vero beatae sint ut.",
        "portfolio_rights": 1,
        "non_compete": 1,
        "feedbacks": 0,
        "appropriate_conduct": 1,
        "annotations": null,
        "description": "Necessitatibus totam qui nostrum ad non qui distinctio. Ipsam non sed deserunt recusandae non eum amet. Et quo quaerat enim voluptates pariatur. Dolor sint cum voluptatem enim. Et ratione deleniti aut deserunt eligendi itaque aut. Qui et eius non voluptatibus quos a sunt. Et rerum quia suscipit nisi. Voluptatem exercitationem culpa at quo deleniti. Reprehenderit repellat ullam nemo tempore amet optio. Et porro distinctio nostrum minus placeat. Voluptatum dolore ex in qui esse occaecati eum. Minus iste nostrum id laudantium. Vel ipsam qui expedita sed et laborum commodi unde. Temporibus fugit sint voluptas fuga.",
        "viewed_at": null,
        "sent_at": null,
        "is_draft": true,
        "rejected_at": null,
        "rejected_reason": null,
        "user_id": 1,
        "business": {
            "id": 1,
            "name": "Sipes-Schuster",
            "contact_person": "ehauck@example.com"
        },
        "created_at": "2018-12-24T05:30:20+03:00",
        "updated_at": "2018-12-24T05:30:20+03:00"
    }
  }


``PUT`` - /api/v1/contracts/{id}
--------------------------------
Update a contract

.. code-block:: shell

  PUT /api/v1/contracts/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

Parameters
^^^^^^^^^^
.. TIP:: Same as the create new contract parameters

``DELETE`` - /api/v1/contracts/{id}
-----------------------------------
Delete a contract

.. code-block:: shell

  DELETE /api/v1/contracts/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken


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
  Authorization: Bearer $AccessToken

Parameters
^^^^^^^^^^
+---------------+------------+-----------------------------------------------------+
| Name          | Required   | Description                                         |
+===============+============+=====================================================+
| name          | required   | Contact Name                                        |
+---------------+------------+-----------------------------------------------------+
| email         | required   | Contact email address                               |
+---------------+------------+-----------------------------------------------------+
| username      | required   | Contact username                                    |
+---------------+------------+-----------------------------------------------------+
| company       | optional   | Contact Company ID                                  |
+---------------+------------+-----------------------------------------------------+
| password      | optional   | Contact login password                              |
+---------------+------------+-----------------------------------------------------+
| phone         | optional   | Contact Phone Number                                |
+---------------+------------+-----------------------------------------------------+
| invite        | optional   | Send email invitation. Set to 1 to send email       |
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


Projects
"""""""""""""""""

``POST`` - /api/v1/projects
-------------------------------
Create a new projects

.. code-block:: shell

  POST /api/v1/projects
  Accept: application/json
  Authorization: Bearer $AccessToken

Parameters
^^^^^^^^^^
+----------------+------------+--------------------------------------------------------------------------------+
| Name           | Required   | Description                                                                    |
+================+============+================================================================================+
| name           | required   | Project Name                                                                   |
+----------------+------------+--------------------------------------------------------------------------------+
| client_id      | required   | Project client ID                                                              |
+----------------+------------+--------------------------------------------------------------------------------+
| start_date     | required   | Project start date                                                             |
+----------------+------------+--------------------------------------------------------------------------------+
| due_date       | required   | Project due date                                                               |
+----------------+------------+--------------------------------------------------------------------------------+
| currency       | optional   | Project Currency                                                               |
+----------------+------------+--------------------------------------------------------------------------------+
| description    | optional   | Description                                                                    |
+----------------+------------+--------------------------------------------------------------------------------+
| hourly_rate    | optional   | Hourly rate                                                                    |
+----------------+------------+--------------------------------------------------------------------------------+
| fixed_price    | optional   | Fixed Price. E.g 3400.00                                                       |
+----------------+------------+--------------------------------------------------------------------------------+
| notes          | optional   | Project Notes                                                                  |
+----------------+------------+--------------------------------------------------------------------------------+
| manager        | optional   | User ID                                                                        |
+----------------+------------+--------------------------------------------------------------------------------+
| estimate_hours | optional   | Project Estimated hours                                                        |
+----------------+------------+--------------------------------------------------------------------------------+
| billing_method | optional   | ``hourly_staff_rate, hourly_task_rate, hourly_project_rate, fixed_rate``       |
+----------------+------------+--------------------------------------------------------------------------------+
| tags[]         | optional   | Array list of tags e.g ``tags[design]``                                        |
+----------------+------------+--------------------------------------------------------------------------------+

``GET`` - /api/v1/projects/{id}
--------------------------------
Get project information

.. code-block:: shell

  GET /api/v1/projects/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

Sample Response
^^^^^^^^^^^^^^^^
.. code-block:: json

  {
    "type": "projects",
    "id": "6",
    "attributes": {
        "id": 6,
        "name": "Rice, Doyle and Bauch Project",
        "code": "PRO0006",
        "description": "Earum quia quis qui id minima et. Esse facere qui eligendi et eaque quia. Rerum corporis consequatur velit odit quam. Aliquam quia architecto et et repellendus. Molestiae et facilis neque dolor. Et laudantium totam aut et. Recusandae corrupti non maxime sed ratione eos ut. Cupiditate repellat harum quia dolor. Et voluptatum laboriosam ex nostrum sed necessitatibus repellat. Eveniet sunt enim est aut ea minima eos. Culpa nihil rem qui non sunt quia. Sed et adipisci porro dolore perferendis fugiat. Quisquam laboriosam quisquam et aspernatur. Rem vel ad facere enim cumque.",
        "client_id": 3,
        "business": {
            "id": 3,
            "name": "Ferry-Schuster",
            "contact_person": "wiza.samanta@example.org"
        },
        "currency": "USD",
        "start_date": "2018-12-24T00:00:00+03:00",
        "due_date": "2019-03-01T00:00:00+03:00",
        "hourly_rate": "59.38",
        "fixed_price": "0.00",
        "progress": 0,
        "notes": null,
        "manager": 1,
        "status": "Active",
        "estimate_hours": "82.08",
        "used_budget": "0.00",
        "billable_time": "0.00",
        "unbillable_time": "0.00",
        "unbilled": "0.00",
        "sub_total": "0.00",
        "total_expenses": "0.00",
        "contract_id": null,
        "billing_method": "hourly_project_rate",
        "created_at": "2018-12-24T05:30:32+03:00",
        "updated_at": "2018-12-24T05:30:32+03:00"
    }
  }


``PUT`` - /api/v1/projects/{id}
--------------------------------
Update project information

.. code-block:: shell

  PUT /api/v1/projects/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

Parameters
^^^^^^^^^^
.. TIP:: Same as the create new project API parameters

``DELETE`` - /api/v1/projects/{id}
-----------------------------------
Delete project

.. code-block:: shell

  DELETE /api/v1/projects/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

``GET`` - /api/v1/projects
----------------------------------------
Get a list of all projects

.. code-block:: shell

  GET /api/v1/projects
  Accept: application/json
  Authorization: Bearer $AccessToken

``GET`` - /api/v1/projects/{id}/invoices
------------------------------------------
Show project invoices

.. code-block:: shell

  GET /api/v1/projects/{id}/invoices
  Accept: application/json
  Authorization: Bearer $AccessToken


``GET`` - /api/v1/projects/{id}/tasks
----------------------------------------
Show project tasks

.. code-block:: shell

  GET /api/v1/projects/{id}/tasks
  Accept: application/json
  Authorization: Bearer $AccessToken

``GET`` - /api/v1/projects/{id}/expenses
------------------------------------------
Show project expenses

.. code-block:: shell

  GET /api/v1/projects/{id}/expenses
  Accept: application/json
  Authorization: Bearer $AccessToken

``POST`` - /api/v1/projects/{id}/done
--------------------------------------
Mark project as done

.. code-block:: shell

  POST /api/v1/projects/{id}/done
  Accept: application/json
  Authorization: Bearer $AccessToken

Parameters
^^^^^^^^^^
+----------------+------------+--------------------------------------------------------------------------------+
| Name           | Required   | Description                                                                    |
+================+============+================================================================================+
| id           | required   | Project ID                                                                       |
+----------------+------------+--------------------------------------------------------------------------------+

``POST`` - /api/v1/projects/{id}/invoice
------------------------------------------
Invoice project

.. code-block:: shell

  POST /api/v1/projects/{id}/invoice
  Accept: application/json
  Authorization: Bearer $AccessToken

Parameters
^^^^^^^^^^
+----------------+------------+--------------------------------------------------------------------------------+
| Name           | Required   | Description                                                                    |
+================+============+================================================================================+
| invoice_style  | required   | ``single or task_line``                                                        |
+----------------+------------+--------------------------------------------------------------------------------+
| expense[]      | optional   | Array list of expense IDs to include                                           |
+----------------+------------+--------------------------------------------------------------------------------+

``POST`` - /api/v1/projects/{id}/copy
---------------------------------------------
Duplicate a project

.. code-block:: shell

  POST /api/v1/projects/{id}/copy
  Accept: application/json
  Authorization: Bearer $AccessToken

Parameters
^^^^^^^^^^
+----------------+------------+--------------------------------------------------------------------------------+
| Name           | Required   | Description                                                                    |
+================+============+================================================================================+
| id             | required   | Project ID                                                                     |
+----------------+------------+--------------------------------------------------------------------------------+
| parts[]        | optional   | Array list of what to clone e.g ``parts[expenses], parts[tasks]``              |
+----------------+------------+--------------------------------------------------------------------------------+


Tickets
"""""""""""""""""

``POST`` - /api/v1/tickets
-------------------------------
Create a new ticket

.. code-block:: shell

  POST /api/v1/tickets
  Accept: application/json
  Authorization: Bearer $AccessToken

Parameters
^^^^^^^^^^
+----------------+------------+--------------------------------------------------------------------------------+
| Name           | Required   | Description                                                                    |
+================+============+================================================================================+
| department     | required   | Ticket department ID                                                           |
+----------------+------------+--------------------------------------------------------------------------------+
| subject        | required   | Ticket subject                                                                 |
+----------------+------------+--------------------------------------------------------------------------------+
| body           | required   | Ticket Message                                                                 |
+----------------+------------+--------------------------------------------------------------------------------+
| project_id     | optional   | Project ID associated with the ticket                                          |
+----------------+------------+--------------------------------------------------------------------------------+

``GET`` - /api/v1/tickets/{id}
--------------------------------
Get ticket information

.. code-block:: shell

  GET /api/v1/tickets/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

Sample Response
^^^^^^^^^^^^^^^^
.. code-block:: json

  {
    "type": "tickets",
    "id": "10",
    "attributes": {
        "id": 10,
        "subject": "Arvid Ticket",
        "code": "TKT-20181224-0010",
        "body": "Iure et laborum debitis quod veniam eum vel temporibus. Et id culpa asperiores molestiae qui animi ad necessitatibus. Ea unde corporis omnis. Minus est dignissimos cupiditate facere autem. Quia natus aliquam qui et. Incidunt et deleniti tempore ut repellat accusamus sed. Hic quasi dolores minima molestiae. Sint non cumque repellat alias vero et perspiciatis. Ad enim qui rerum libero. Labore aut voluptas dolores possimus tenetur. Vero maxime facilis aut debitis est quis dignissimos. Quae ipsa id nihil illo. In omnis ratione sunt quo est et officia. In repudiandae recusandae ipsa similique beatae adipisci.",
        "status": {
            "id": 1,
            "name": "open"
        },
        "department": {
            "id": 1,
            "name": "Billing"
        },
        "user_id": 1,
        "project_id": null,
        "priority": {
            "id": 1,
            "name": "Low"
        },
        "due_date": "2018-12-27T00:00:00+03:00",
        "closed_at": null,
        "assignee": {
            "id": 1,
            "name": "William Mandai"
        },
        "resolution_time": 0,
        "archived_at": null,
        "created_at": "2018-12-24T05:30:44+03:00",
        "updated_at": "2018-12-24T05:30:44+03:00"
    }
  }


``PUT`` - /api/v1/tickets/{id}
--------------------------------
Update ticket information

.. code-block:: shell

  PUT /api/v1/tickets/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

Parameters
^^^^^^^^^^
.. TIP:: Same as the create new ticket API parameters above

``DELETE`` - /api/v1/tickets/{id}
-----------------------------------
Delete ticket

.. code-block:: shell

  DELETE /api/v1/tickets/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

``GET`` - /api/v1/tickets
----------------------------------------
Get a list of all tickets

.. code-block:: shell

  GET /api/v1/tickets
  Accept: application/json
  Authorization: Bearer $AccessToken

``GET`` - /api/v1/tickets/{id}/comments
------------------------------------------
Show ticket comments

.. code-block:: shell

  GET /api/v1/tickets/{id}/comments
  Accept: application/json
  Authorization: Bearer $AccessToken


``POST`` - /api/v1/tickets/{id}/status
----------------------------------------
Update ticket status

.. code-block:: shell

  POST /api/v1/tickets/{id}/status
  Accept: application/json
  Authorization: Bearer $AccessToken

Parameters
^^^^^^^^^^
+----------------+------------+--------------------------------------------------------------------------------+
| Name           | Required   | Description                                                                    |
+================+============+================================================================================+
| status         | required   | Ticket status ID                                                               |
+----------------+------------+--------------------------------------------------------------------------------+

Tasks
"""""""""""""""""

``POST`` - /api/v1/tasks
-------------------------------
Create a new task

.. code-block:: shell

  POST /api/v1/tasks
  Accept: application/json
  Authorization: Bearer $AccessToken

Parameters
^^^^^^^^^^
+----------------+------------+----------------------------------------------------------------------------------+
| Name             | Required   | Description                                                                    |
+==================+============+================================================================================+
| project_id       | required   | Project ID                                                                     |
+------------------+------------+--------------------------------------------------------------------------------+
| user_id          | required   | Task creator user id                                                           |
+------------------+------------+--------------------------------------------------------------------------------+
| name             | required   | Task Name                                                                      |
+------------------+------------+--------------------------------------------------------------------------------+
| start_date       | optional   | Task start date                                                                |
+------------------+------------+--------------------------------------------------------------------------------+
| due_date         | optional   | Task due date                                                                  |
+------------------+------------+--------------------------------------------------------------------------------+
| hourly_rate      | optional   | Hourly rate e.g 30.00                                                          |
+------------------+------------+--------------------------------------------------------------------------------+
| milestone_id     | optional   | Milestone ID                                                                   |
+------------------+------------+--------------------------------------------------------------------------------+
| stage_id         | optional   | Task stage ID                                                                  |
+------------------+------------+--------------------------------------------------------------------------------+
| team[]           | optional   | Array list of team member ID's                                                 |
+------------------+------------+--------------------------------------------------------------------------------+
| estimated_hours  | optional   | Task estimated hours e.g 72                                                    |
+------------------+------------+--------------------------------------------------------------------------------+
| description      | optional   | Description                                                                    |
+------------------+------------+--------------------------------------------------------------------------------+
| visible          | optional   | Hide or show to client                                                         |
+------------------+------------+--------------------------------------------------------------------------------+
| tags[]           | optional   | Array list of tags e.g ``tags[design]``                                        |
+------------------+------------+--------------------------------------------------------------------------------+

``GET`` - /api/v1/tasks/{id}
--------------------------------
Get task information

.. code-block:: shell

  GET /api/v1/tasks/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

Sample Response
^^^^^^^^^^^^^^^^
.. code-block:: json

  {
    "type": "tasks",
    "id": "10",
    "attributes": {
        "id": 10,
        "name": "McGlynn-Jaskolski Task",
        "project": {
            "id": 1,
            "name": "Stracke PLC Project"
        },
        "milestone": {
            "id": null,
            "name": null
        },
        "progress": 94,
        "hourly_rate": "4.08",
        "estimated_hours": "0.00",
        "estimated_price": "$0.00",
        "hours": 0,
        "start_date": "2019-01-07T00:00:00+03:00",
        "due_date": "2019-01-16T00:00:00+03:00",
        "description": "Vel autem ea aperiam nihil. Consequatur neque omnis omnis ut fugiat amet dolores. Voluptates quisquam odit tenetur doloremque ipsa voluptates.",
        "updated_at": "2018-12-24T05:30:32+03:00",
        "created_at": "2018-12-24T05:30:32+03:00"
    }
  }


``PUT`` - /api/v1/tasks/{id}
--------------------------------
Update task information

.. code-block:: shell

  PUT /api/v1/tasks/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

Parameters
^^^^^^^^^^
.. TIP:: Same as the create task API parameters above

``DELETE`` - /api/v1/tasks/{id}
-----------------------------------
Delete a task

.. code-block:: shell

  DELETE /api/v1/tasks/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

``GET`` - /api/v1/tasks
----------------------------------------
Get a list of all tasks

.. code-block:: shell

  GET /api/v1/tasks
  Accept: application/json
  Authorization: Bearer $AccessToken

``POST`` - /api/v1/tasks/{id}/copy
----------------------------------------
Duplicate a task

.. code-block:: shell

  POST /api/v1/tasks/{id}/copy
  Accept: application/json
  Authorization: Bearer $AccessToken

Parameters
^^^^^^^^^^
+----------------+------------+--------------------------------------------------------------------------------+
| Name           | Required   | Description                                                                    |
+================+============+================================================================================+
| project_id     | required   | Project ID to copy task to                                                     |
+----------------+------------+--------------------------------------------------------------------------------+

Todos
"""""""""""""""""

``POST`` - /api/v1/todos
-------------------------------
Create a new todo

.. code-block:: shell

  POST /api/v1/todos
  Accept: application/json
  Authorization: Bearer $AccessToken

Parameters
^^^^^^^^^^
+----------------+------------+----------------------------------------------------------------------------------+
| Name             | Required   | Description                                                                    |
+==================+============+================================================================================+
| module           | required   | Module related to todo e.g ``deals, clients, leads``                           |
+------------------+------------+--------------------------------------------------------------------------------+
| module_id        | required   | Entity ID e.g ``18``                                                           |
+------------------+------------+--------------------------------------------------------------------------------+
| subject          | required   | Todo subject                                                                   |
+------------------+------------+--------------------------------------------------------------------------------+
| due_date         | optional   | Todo start date                                                                |
+------------------+------------+--------------------------------------------------------------------------------+
| assignee         | optional   | User ID of the person responsible                                              |
+------------------+------------+--------------------------------------------------------------------------------+
| notes            | optional   | Additional notes                                                               |
+------------------+------------+--------------------------------------------------------------------------------+

``GET`` - /api/v1/todos/{id}
--------------------------------
Get todo information

.. code-block:: shell

  GET /api/v1/todos/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

Sample Response
^^^^^^^^^^^^^^^^
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


``PUT`` - /api/v1/todos/{id}
--------------------------------
Update todo information

.. code-block:: shell

  PUT /api/v1/todos/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

Parameters
^^^^^^^^^^
+------------------+------------+--------------------------------------------------------------------------------+
| Name             | Required   | Description                                                                    |
+==================+============+================================================================================+
| subject          | required   | Todo subject                                                                   |
+------------------+------------+--------------------------------------------------------------------------------+
| due_date         | optional   | Todo start date                                                                |
+------------------+------------+--------------------------------------------------------------------------------+
| assignee         | optional   | User ID of the person responsible                                              |
+------------------+------------+--------------------------------------------------------------------------------+
| notes            | optional   | Additional notes                                                               |
+------------------+------------+--------------------------------------------------------------------------------+

``DELETE`` - /api/v1/todos/{id}
-----------------------------------
Delete a todo

.. code-block:: shell

  DELETE /api/v1/todos/{id}
  Accept: application/json
  Authorization: Bearer $AccessToken

``GET`` - /api/v1/todos
----------------------------------------
Get a list of all todos

.. code-block:: shell

  GET /api/v1/todos
  Accept: application/json
  Authorization: Bearer $AccessToken
