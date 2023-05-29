API Documentation: Direct Debit APIs
====================================

**Getting Started**
===================

The Direct Debit API facilitates the process for Service Providers
(referred to as Billers) to generate debit mandate instructions on their
clients/customers’ bank accounts for services rendered or products sold.

These debit mandate instructions are created as digital versions of
physical instructions that are duly signed by the account owners
(clients/customers). Once generated, the mandate instructions are
automatically sent to the bank where the account is held for review and
approval. The approval process requires the bank to contact the account
owner to authorize the mandate, which typically takes 24-48 hours.

The system automatically assigns a unique mandate code to each initiated
mandate. This mandate code is used to initiate a direct debit
transaction on the bank account associated with the debit mandate
instruction.

Primarily, this API caters to businesses that necessitate recurring
payments on specific dates with fixed amounts, such as insurance
premiums, loan repayments, service subscriptions, or variable recurring
payments on different dates (e.g., postpaid lines, electricity usage).

This document provides a comprehensive overview and detailed
specifications of the Direct Debit APIs, including all the necessary
information for seamless integration into your respective applications.

. The APIs consist of four main modules:

-  Mandate
-  Transactions
-  Beneficiaries
-  Banks

These modules allow users to manage mandates, initiate transactions, and
get beneficiaries for direct debit operations.

Base URL
--------

All API requests should be made to the following base URL: {{}}

Authentication
--------------

API requests require authentication using an API key. This is also a
unique alphanumeric key that is used to authenticate every request sent.
It is to be contained in the request body of any request sent.

Include the API key in the request header as follows:

Authorization: Bearer {API_KEY}

How to get your API Key
-----------------------

-  **Step 1**: Login to Direct Debit portal
-  **Step 2**: Navigate to the API Module
-  **Step 3**: Click on ’Create API Keys”
-  **Step 4**: Input the following values

   -  API Key (Name of the application intending to use the Keys)
   -  Description (
   -  Webhook URL - (URL of the application intending to use the keys)
   -  Timeout - (duration after which a request is considered
      unsuccessful)

-  **Step 5**: Complete these values and click on ‘Create Key’

**Error Handling**
------------------

Errors are returned with appropriate HTTP status codes and error
messages in the response body. Refer to the API Error Handling
documentation for more details.

HTTP status codes
~~~~~~~~~~~~~~~~~

These are 3-digit responses issued by the server. They are standard
responses and can be easily interpreted based on their first digits.

2XX - Success of some kind

4XX - Error occurred on client’s end

5XX - Error occurred in the server’s end

The codes for this API include:

200 - OK

201 - Created

202 - Accepted (Request accepted, and queued for execution)

400 - Bad request

401 - Authentication failure

403 - Forbidden

404 - Resource not found

409 - Conflict

500 - Internal Server Error

1. **Mandate Module**

The Mandate module provides endpoints for managing direct debit
mandates.

1.1 Create a Mandate
--------------------

This endpoint allows you to create a mandate on a customer’s account

**Request Body Fields**
~~~~~~~~~~~~~~~~~~~~~~~

.. raw:: html

   <table>

.. raw:: html

   <tr>

.. raw:: html

   <td>

Field

.. raw:: html

   </td>

.. raw:: html

   <td>

Type

.. raw:: html

   </td>

.. raw:: html

   <td>

Description

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

account_number

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Customer NUBAN account number to create the mandate against

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

phone_number

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The phone number associated with the transaction.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

debit_type

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The type of debit all or partial.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

frequency

.. raw:: html

   </td>

.. raw:: html

   <td>

Number

.. raw:: html

   </td>

.. raw:: html

   <td>

The frequency of debiting the mandates.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bank_id

.. raw:: html

   </td>

.. raw:: html

   <td>

Number

.. raw:: html

   </td>

.. raw:: html

   <td>

The ID of the bank of the customer bank and this is gotten from the Get
Bank endpoint

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

email

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Customer email address

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

start_date

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The start date of the mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

end_date

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The end date of the mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

narration

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The narration or description of the mandate i.e. what the mandate is for

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

address

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Customer address

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

amount

.. raw:: html

   </td>

.. raw:: html

   <td>

Number

.. raw:: html

   </td>

.. raw:: html

   <td>

The maximum amount that can be debited using the specific mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

beneficiary_id

.. raw:: html

   </td>

.. raw:: html

   <td>

Number

.. raw:: html

   </td>

.. raw:: html

   <td>

The ID of the recipient of the mandate debits.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

file_base64

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The Base64 encoded data equivalent to the customer’s mandate letter.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

file_extension

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The extension of the file which is pdf .

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

**Response Body Fields**
~~~~~~~~~~~~~~~~~~~~~~~~

1.2. Get Mandate
----------------

This endpoint retrieves all mandates associated with the API key in use

.. _response-body-fields-1:

**Response Body Fields**
~~~~~~~~~~~~~~~~~~~~~~~~

.. raw:: html

   <table>

.. raw:: html

   <tr>

.. raw:: html

   <td>

Field

.. raw:: html

   </td>

.. raw:: html

   <td>

Type

.. raw:: html

   </td>

.. raw:: html

   <td>

Description

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

status

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The status of the request

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

message

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

A message describing the result of the request

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

data

.. raw:: html

   </td>

.. raw:: html

   <td>

object

.. raw:: html

   </td>

.. raw:: html

   <td>

An object containing the mandate information

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

data

.. raw:: html

   </td>

.. raw:: html

   <td>

array

.. raw:: html

   </td>

.. raw:: html

   <td>

An array of mandate objects

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

account_number

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The account number associated with the mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

account_name

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The account name associated with the mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

frequency

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The frequency of the mandate (e.g., daily, weekly)

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bvn

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The Bank Verification Number (BVN) of the user

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

phone_number

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The phone number associated with the mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

email

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The email address associated with the mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

start_date

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The start date of the mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

end_date

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The end date of the mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

narration

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

A description or note for the mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

address

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The address associated with the mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

amount

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The amount associated with the mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

status

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The status of the mandate (e.g., pending, active)

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

workflow_status

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The workflow status of the mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

debit_type

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The type of debit for the mandate (e.g., all, limited)

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

created_on

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The date and time the mandate was created

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bank

.. raw:: html

   </td>

.. raw:: html

   <td>

object

.. raw:: html

   </td>

.. raw:: html

   <td>

The bank details associated with the mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

name

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The name of the bank

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bank_code

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The bank code

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

institution_code

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The institution code of the bank

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

url

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The URL of the bank

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

beneficiary

.. raw:: html

   </td>

.. raw:: html

   <td>

object

.. raw:: html

   </td>

.. raw:: html

   <td>

The recipient of the mandate debits.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

account_number

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The account number of the beneficiary

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

account_name

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The account name of the beneficiary

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bvn

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The Bank Verification

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

1.3 Get Mandate Details
-----------------------

Retrieves the details of a specific mandate.

**Query Params**
~~~~~~~~~~~~~~~~

.. raw:: html

   <table>

.. raw:: html

   <tr>

.. raw:: html

   <td>

Field

.. raw:: html

   </td>

.. raw:: html

   <td>

Type

.. raw:: html

   </td>

.. raw:: html

   <td>

Description

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

Mandate_id

.. raw:: html

   </td>

.. raw:: html

   <td>

Number

.. raw:: html

   </td>

.. raw:: html

   <td>

The ID of the mandate you want to get the details of.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

.. _response-body-fields-2:

**Response Body Fields**
~~~~~~~~~~~~~~~~~~~~~~~~

.. raw:: html

   <table>

.. raw:: html

   <tr>

.. raw:: html

   <td>

Field

.. raw:: html

   </td>

.. raw:: html

   <td>

Type

.. raw:: html

   </td>

.. raw:: html

   <td>

Description

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

status

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The status of the request

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

message

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

A message describing the result of the request

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

data

.. raw:: html

   </td>

.. raw:: html

   <td>

object

.. raw:: html

   </td>

.. raw:: html

   <td>

An object containing the mandate information

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

account_number

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The account number associated with the mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

account_name

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The account name associated with the mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

frequency

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The frequency of the mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bvn

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The Bank Verification Number (BVN) of the customer

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

phone_number

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The phone number associated with the mandate (null in this case)

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

email

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The email address associated with the mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

start_date

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The start date of the mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

end_date

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The end date of the mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

narration

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

A description or note for the mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

address

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The address associated with the mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

amount

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The amount associated with the mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

status

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The status of the mandate (e.g., active)

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

workflow_status

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The workflow status of the mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

debit_type

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The type of debit for the mandate (e.g., all)

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

created_on

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The date and time the mandate was created

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bank

.. raw:: html

   </td>

.. raw:: html

   <td>

object

.. raw:: html

   </td>

.. raw:: html

   <td>

The bank details associated with the mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

name

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The name of the bank

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bank_code

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The bank code

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

institution_code

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The institution code of the bank

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

url

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The URL of the bank

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

beneficiary

.. raw:: html

   </td>

.. raw:: html

   <td>

object

.. raw:: html

   </td>

.. raw:: html

   <td>

The beneficiary details associated with the mandate

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

account_number

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The account number of the beneficiary

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

account_name

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The account name of the beneficiary

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bvn

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The Bank Verification Number (BVN) of the beneficiary

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

last_transaction_date

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The last transaction date of the beneficiary

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

status

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The status of the beneficiary (e.g., active)

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

created_on

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The date and time the beneficiary was created

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bank

.. raw:: html

   </td>

.. raw:: html

   <td>

object

.. raw:: html

   </td>

.. raw:: html

   <td>

The bank details associated with the beneficiary

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

name

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The name of the bank

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bank_code

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The bank code

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

institution_code

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The institution code of the bank

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

url

.. raw:: html

   </td>

.. raw:: html

   <td>

string

.. raw:: html

   </td>

.. raw:: html

   <td>

The URL of the bank

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

1.4. Activate / deactivate Mandate
----------------------------------

Activate or deactivate a specific mandate.

.. _query-params-1:

**Query Params**
~~~~~~~~~~~~~~~~

.. raw:: html

   <table>

.. raw:: html

   <tr>

.. raw:: html

   <td>

Field

.. raw:: html

   </td>

.. raw:: html

   <td>

Type

.. raw:: html

   </td>

.. raw:: html

   <td>

Description

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

Mandate_id

.. raw:: html

   </td>

.. raw:: html

   <td>

Number

.. raw:: html

   </td>

.. raw:: html

   <td>

The ID of the mandate you want to get the details of.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

Type

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

indicate the desired status for the mandate, either ‘activate’,
‘deactivate’ or ‘approve’.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

.. _response-body-fields-3:

**Response Body Fields**
~~~~~~~~~~~~~~~~~~~~~~~~

2. **Transactions Module**

The Transactions module provides endpoints for initiating direct debit
transactions.

2.1. Get Transactions
---------------------

Retrieve the transactions related to the mandates associated with the
API key.

.. _response-body-fields-4:

**Response Body Fields**
~~~~~~~~~~~~~~~~~~~~~~~~

.. raw:: html

   <table>

.. raw:: html

   <tr>

.. raw:: html

   <td>

Field

.. raw:: html

   </td>

.. raw:: html

   <td>

Type

.. raw:: html

   </td>

.. raw:: html

   <td>

Description

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

id

.. raw:: html

   </td>

.. raw:: html

   <td>

Integer

.. raw:: html

   </td>

.. raw:: html

   <td>

The ID of the transaction.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

amount

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The amount of the transaction.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

mandate_id

.. raw:: html

   </td>

.. raw:: html

   <td>

Integer

.. raw:: html

   </td>

.. raw:: html

   <td>

The ID of the associated mandate.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

mandate_account_name

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The account name associated with the mandate.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

mandate_account_number

.. raw:: html

   </td>

.. raw:: html

   <td>

Integer

.. raw:: html

   </td>

.. raw:: html

   <td>

The account number associated with the mandate.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

mandate_bvn

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The Bank Verification Number (BVN) associated with the mandate.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

reference

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The reference number of the transaction.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

narration

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The description or purpose of the transaction.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

beneficiary_id

.. raw:: html

   </td>

.. raw:: html

   <td>

Integer

.. raw:: html

   </td>

.. raw:: html

   <td>

The ID of the recipient of the mandate debits.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

beneficiary_account_name

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The account name of the recipient of the mandate debits.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

beneficiary_account_number

.. raw:: html

   </td>

.. raw:: html

   <td>

Integer

.. raw:: html

   </td>

.. raw:: html

   <td>

The account number of the recipient of the mandate debits.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

beneficiary_bvn

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The Bank Verification Number (BVN) of the beneficiary.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

session_id

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The session ID associated with the transaction.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

status

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The status of the transaction (e.g., success, failed).

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

created_on

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The date and time when the transaction was created.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

mandate_bank

.. raw:: html

   </td>

.. raw:: html

   <td>

Object

.. raw:: html

   </td>

.. raw:: html

   <td>

The bank details associated with the mandate (see bank fields below).

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

id

.. raw:: html

   </td>

.. raw:: html

   <td>

Integer

.. raw:: html

   </td>

.. raw:: html

   <td>

The ID of the bank.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

name

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The name of the bank.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bank_code

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The bank code associated with the bank.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

institution_code

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The institution code associated with the bank.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

url

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The URL of the bank (if available).

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

2.2. Get Transaction Details
----------------------------

Retrieves the details of a specific transaction.

\*\* Params Query*\*
~~~~~~~~~~~~~~~~~~~~

.. raw:: html

   <table>

.. raw:: html

   <tr>

.. raw:: html

   <td>

Field

.. raw:: html

   </td>

.. raw:: html

   <td>

Type

.. raw:: html

   </td>

.. raw:: html

   <td>

Description

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

Transaction_id

.. raw:: html

   </td>

.. raw:: html

   <td>

Number

.. raw:: html

   </td>

.. raw:: html

   <td>

The ID of the transaction you want to get the details of.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

.. _response-body-fields-5:

**Response Body Fields**
~~~~~~~~~~~~~~~~~~~~~~~~

.. raw:: html

   <table>

.. raw:: html

   <tr>

.. raw:: html

   <td>

Field

.. raw:: html

   </td>

.. raw:: html

   <td>

Type

.. raw:: html

   </td>

.. raw:: html

   <td>

Description

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

id

.. raw:: html

   </td>

.. raw:: html

   <td>

Integer

.. raw:: html

   </td>

.. raw:: html

   <td>

The ID of the transaction.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

amount

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The amount of the transaction.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

mandate_id

.. raw:: html

   </td>

.. raw:: html

   <td>

Integer

.. raw:: html

   </td>

.. raw:: html

   <td>

The ID of the associated mandate.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

mandate_account_name

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The account name associated with the mandate.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

mandate_account_number

.. raw:: html

   </td>

.. raw:: html

   <td>

Integer

.. raw:: html

   </td>

.. raw:: html

   <td>

The account number associated with the mandate.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

mandate_bvn

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The Bank Verification Number (BVN) associated with the mandate.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

reference

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The reference number of the transaction.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

narration

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The description or purpose of the transaction.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

beneficiary_id

.. raw:: html

   </td>

.. raw:: html

   <td>

Integer

.. raw:: html

   </td>

.. raw:: html

   <td>

The ID of the recipient of the mandate debits.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

beneficiary_account_name

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The account name of the recipient of the mandate debits.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

beneficiary_account_number

.. raw:: html

   </td>

.. raw:: html

   <td>

Integer

.. raw:: html

   </td>

.. raw:: html

   <td>

The account number of the recipient of the mandate debits.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

beneficiary_bvn

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The Bank Verification Number (BVN) of the beneficiary.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

session_id

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The session ID associated with the transaction.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

status

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The status of the transaction (e.g., success, failed).

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

created_on

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The date and time when the transaction was created.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

mandate_bank

.. raw:: html

   </td>

.. raw:: html

   <td>

Object

.. raw:: html

   </td>

.. raw:: html

   <td>

The bank details associated with the mandate (see bank fields below).

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

id

.. raw:: html

   </td>

.. raw:: html

   <td>

Integer

.. raw:: html

   </td>

.. raw:: html

   <td>

The ID of the bank.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

name

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The name of the bank.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bank_code

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The bank code associated with the bank.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

institution_code

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The institution code associated with the bank.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

url

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The URL of the bank (if available).

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

2.3. Get Transaction Status
---------------------------

Retrieves the status of a specific transaction.

.. _response-body-fields-6:

**Response Body Fields**
~~~~~~~~~~~~~~~~~~~~~~~~

.. raw:: html

   <table>

.. raw:: html

   <tr>

.. raw:: html

   <td>

Field

.. raw:: html

   </td>

.. raw:: html

   <td>

Type

.. raw:: html

   </td>

.. raw:: html

   <td>

Description

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

status

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The status of the mandate transactions.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

count

.. raw:: html

   </td>

.. raw:: html

   <td>

Integer

.. raw:: html

   </td>

.. raw:: html

   <td>

The number of transactions with the given status.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

sum

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

The total sum of transactions with the given status.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

3. **Beneficiaries Module**

The Beneficiaries module provides endpoints for managing beneficiary
accounts.

3.1. Get Beneficiaries
----------------------

Retrieves the beneficiaries from the direct debit portal.

.. _response-body-fields-7:

**Response Body Fields**
~~~~~~~~~~~~~~~~~~~~~~~~

.. raw:: html

   <table>

.. raw:: html

   <tr>

.. raw:: html

   <td>

Field

.. raw:: html

   </td>

.. raw:: html

   <td>

Type

.. raw:: html

   </td>

.. raw:: html

   <td>

Description

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

id

.. raw:: html

   </td>

.. raw:: html

   <td>

Integer

.. raw:: html

   </td>

.. raw:: html

   <td>

Unique identifier for the recipient of the mandate debits.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

account_number

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Account number associated with the recipient of the mandate debits.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

account_name

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Name of the account holder associated with the recipient of the mandate
debits.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bvn

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Bank Verification Number (BVN) associated with the beneficiary

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

last_transaction_date

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Date and time of the last transaction made on the beneficiary’s account
(null if not available)

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

status

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Status of the beneficiary (e.g., active, inactive)

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

created_on

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Date and time when the beneficiary was created

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bank.name

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Name of the bank associated with the beneficiary

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bank.bank_code

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Bank code of the bank associated with the beneficiary

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bank.institution_code

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Institution code of the bank associated with the beneficiary

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bank.url

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

3.2 Get Beneficiary Details
---------------------------

Retrieves the details of a specific beneficiary account.

.. _params-query-1:

\*\* Params Query*\*
~~~~~~~~~~~~~~~~~~~~

.. raw:: html

   <table>

.. raw:: html

   <tr>

.. raw:: html

   <td>

Field

.. raw:: html

   </td>

.. raw:: html

   <td>

Type

.. raw:: html

   </td>

.. raw:: html

   <td>

Description

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

Beneficiary_id

.. raw:: html

   </td>

.. raw:: html

   <td>

Number

.. raw:: html

   </td>

.. raw:: html

   <td>

The ID of the beneficiary you want to get the details of.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

**Response Body Field**
~~~~~~~~~~~~~~~~~~~~~~~

.. raw:: html

   <table>

.. raw:: html

   <tr>

.. raw:: html

   <td>

Field

.. raw:: html

   </td>

.. raw:: html

   <td>

Type

.. raw:: html

   </td>

.. raw:: html

   <td>

Description

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

id

.. raw:: html

   </td>

.. raw:: html

   <td>

Integer

.. raw:: html

   </td>

.. raw:: html

   <td>

Unique identifier for the beneficiary

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

account_number

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Account number associated with the recipient of the mandate debits.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

account_name

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Name of the account holder associated with the beneficiary

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bvn

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Bank Verification Number (BVN) associated with the beneficiary

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

last_transaction_date

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Date and time of the last transaction made on the beneficiary’s account
(null if not available)

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

status

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Status of the beneficiary (e.g., active, inactive)

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

created_on

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Date and time when the beneficiary was created

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bank.name

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Name of the bank associated with the beneficiary

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bank.bank_code

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Bank code of the bank associated with the beneficiary

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bank.institution_code

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Institution code of the bank associated with the beneficiary

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bank.url

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

3.3 Get Beneficiary Status
--------------------------

Retrieves the status of the beneficiaries from the direct debit portal

.. _response-body-field-1:

**Response Body Field**
~~~~~~~~~~~~~~~~~~~~~~~

.. raw:: html

   <table>

.. raw:: html

   <tr>

.. raw:: html

   <td>

Field

.. raw:: html

   </td>

.. raw:: html

   <td>

Type

.. raw:: html

   </td>

.. raw:: html

   <td>

Description

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

status

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Status of the beneficiary (e.g., active, inactive)

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

count

.. raw:: html

   </td>

.. raw:: html

   <td>

Integer

.. raw:: html

   </td>

.. raw:: html

   <td>

Count of beneficiaries with the specified status

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

3.4 Get Beneficiary Status by ID
--------------------------------

Retrieves the status of a specific beneficiary

.. _query-params-2:

\*\* Query Params \*\*
~~~~~~~~~~~~~~~~~~~~~~

.. raw:: html

   <table>

.. raw:: html

   <tr>

.. raw:: html

   <td>

Field

.. raw:: html

   </td>

.. raw:: html

   <td>

Type

.. raw:: html

   </td>

.. raw:: html

   <td>

Description

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

Beneficiary_id

.. raw:: html

   </td>

.. raw:: html

   <td>

Number

.. raw:: html

   </td>

.. raw:: html

   <td>

The ID of the mandate you want to get the details of.

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

.. _response-body-field-2:

**Response Body Field**
~~~~~~~~~~~~~~~~~~~~~~~

.. raw:: html

   <table>

.. raw:: html

   <tr>

.. raw:: html

   <td>

Field

.. raw:: html

   </td>

.. raw:: html

   <td>

Type

.. raw:: html

   </td>

.. raw:: html

   <td>

Description

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

transactions.count

.. raw:: html

   </td>

.. raw:: html

   <td>

Integer

.. raw:: html

   </td>

.. raw:: html

   <td>

Count of transactions associated with the beneficiary

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

mandates.count

.. raw:: html

   </td>

.. raw:: html

   <td>

Integer

.. raw:: html

   </td>

.. raw:: html

   <td>

Count of mandates associated with the beneficiary

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

**Banks.**
==========

The Bank module provides endpoints for the banks on the direct debit
portal

4.1 Get Banks
-------------

Retrieve the banks available on the direct debit portal

.. _response-body-fields-8:

**Response Body Fields**
~~~~~~~~~~~~~~~~~~~~~~~~

.. raw:: html

   <table>

.. raw:: html

   <tr>

.. raw:: html

   <td>

Field

.. raw:: html

   </td>

.. raw:: html

   <td>

Type

.. raw:: html

   </td>

.. raw:: html

   <td>

Description

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

id

.. raw:: html

   </td>

.. raw:: html

   <td>

Integer

.. raw:: html

   </td>

.. raw:: html

   <td>

Unique identifier for the bank

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

name

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Name of the bank

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bank_code

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Bank code associated with the bank

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

institution_code

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Institution code associated with the bank

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

url

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

URL pointing to the bank’s logo or image

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

4.3 Account Lookup
------------------

Retrieve the details of a specific account

**Request Body Field**
~~~~~~~~~~~~~~~~~~~~~~

.. raw:: html

   <table>

.. raw:: html

   <tr>

.. raw:: html

   <td>

Field

.. raw:: html

   </td>

.. raw:: html

   <td>

Type

.. raw:: html

   </td>

.. raw:: html

   <td>

Description

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

account_number

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Account number to be looked up

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bank_id

.. raw:: html

   </td>

.. raw:: html

   <td>

Integer

.. raw:: html

   </td>

.. raw:: html

   <td>

Identifier of the bank to which the account belongs

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

.. _response-body-field-3:

**Response Body Field**
~~~~~~~~~~~~~~~~~~~~~~~

.. raw:: html

   <table>

.. raw:: html

   <tr>

.. raw:: html

   <td>

Field

.. raw:: html

   </td>

.. raw:: html

   <td>

Type

.. raw:: html

   </td>

.. raw:: html

   <td>

Description

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

account_name

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Name of the account holder associated with the account number

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

bvn

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Bank Verification Number (BVN) associated with the account holder

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   <tr>

.. raw:: html

   <td>

session_id

.. raw:: html

   </td>

.. raw:: html

   <td>

String

.. raw:: html

   </td>

.. raw:: html

   <td>

Session ID or identifier associated with the account lookup operation

.. raw:: html

   </td>

.. raw:: html

   </tr>

.. raw:: html

   </table>

**Conclusion**
==============

This API documentation offers a comprehensive overview and
specifications for the Direct Debit APIs, including modules for
beneficiaries, banks, and the management of mandates and transactions.
To seamlessly integrate and utilise these APIs, utilise the provided
endpoints and adhere to the defined request and response formats.

1. 
