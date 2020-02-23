OVERVIEW
--------

Digital Rebar Platform - various Postman related Collections for use with the postman.com service or applications.

To operate these Collection you will need to set apprpriate Environment Variables with your DRP Endpoint and authentication information.  In addition, various Postman Variables are used to drive the various patterns found in this collection.


COLLECTIONS
-----------

The following collections can be found here:

  * ``drp-apiv3`` = APIv3 reference collection, also found on the swagger-ui of a DRP Endpoint
  * ``drp-patterns`` = Various API patterns for driving operational changes on a DRP Endpoint
  * ``environments`` = example Environment definitions

SETUP
-----

Create an Environment for the specific DRP Endpoint you will work with.  Set the following Variables (with examples, modify appropriately):

  * ``RS_ENDPOINT`` = ``https://10.10.10.10:8092``
  * ``RS_USERNAME`` = ``drpadmin``
  * ``RS_PASSWORD`` = ``PASSWORD``


OPERATION
---------

The following Postman Variables implement the various pattern change behaviors.

  * ``RS_UUID`` = the DRP Machine UUID object to modify
  * ``PROFILE`` = profile_to_change
  * ``WORKFLOW`` = workflow_to_set

Setting these values will either add/remove (profile), or set the operational Workflow on the Machine object specified by ``RS_UUID``.


NOTES
-----

The Digital Rebar Platform API relies extensively on the JSON PATCH operations.  This means to insure atomicty and safety guarantees, you must first get the current state of a JSON Field that you would like to change, then modify the field with the new values.

This method guarantees that you will only modify a Field from a given start point to an intended destination.  If some one/thing makes an API, CLI, or Web Portal call that changes the object on you, the JSON PATCH operation will fail, protecting against unintended effects.


TODO
----

This needs to be rewritten to take better advantage of reusable components.  Currently, a lot of the "GET" operations are duplicated, and not very well laid out for reusability or future modification.



