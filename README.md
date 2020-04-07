OVERVIEW
--------

Digital Rebar Platform - various Postman related Patterns for operating infrastructure managed by DRP.

To operate this Collection you will need to set an apprpriate Environment with your DRP Endpoint information.  In addition, various Postman Variables are used to drive the various patterns found in this collection.

Postman Usage in Video Form
---------------------------

The Postman usage patterns and examples are available for your review in video form, you can find the video at:

  * https://youtu.be/OsPhkJ-P-Sk

SOURCE CODE
-----------

The source code for this collection is maintained as part of the Digital Rebar Platform github content, and can be found at:

	* https://github.com/digitalrebar/postman

SETUP
-----

Create an Environment for the specific DRP Endpoint you will work with.  Set the following Variables (with examples, modify appropriately):

  * RS_ENDPOINT = https://10.10.10.10:8092
  * RS_USERNAME = drpadmin
  * RS_PASSWORD = PASSWORD


AUTHENTICATION
--------------

By default, the ``drp-patterns`` collection uses the RS\_USERNAME and RS\_PASSWORD to generate a JWT Token for the subsequent authentications.  This is completed as part of the collections ``Pre-request Scripts`` mechanism.  If you remove the ``Pre-request Scripts`` code, you can generate a Digital Rebar Platform authentication token via the API or CLI in an offline manner.  For CLI example, do:

	* ``drpcli users token <USERNAME> ttl 24h``

Replace ``<USERNAME>`` with a user that you are authorized to generate tokens for.  This token can be used without the operator or system having user/auth access.

Simply set the ``Environment`` variable in Postman ``RS_TOKEN`` with the token you generate.


OPERATION
---------

The following Postman Variables implement the various pattern change behaviors.

  * PROFILE = profile_to_change
  * WORKFLOW = workflow_to_set

Setting these values will either add/remove (profile), or set the operational Workflow on the Machine object.

You can use the Postman _Runner_ to execute groups of API calls in a single "run".  The collection is organized using Folders as individual sets of API calls that you might wish to make in on run.  Use the Runner, set the Environment, then select the sub-folder with the appropriate set of calls.


A NOTE ABOUT JSON PATCH
-----------------------

The Digital Rebar Platform service makes extensive use of the JSON PATCH (http://jsonpatch.com/) mechanism.  This provides strong guarantees that the JSON Object or Field you are modifying is in a known good starting state, and hasn't been modified by another Writer via the Web Portal, CLI, or API systems.  If the PATCH ``test`` operation fails, the PATCH will not complete successfully.

This Postman code makes extensive use of the Variable subsystem to store temporary state information to support the PATCH operations.  An example for Adding a profile requires two API calls, one initial ``GET`` operation to get the current list of ``Profiles`` on the Machine Object, storing this as ``RS_PROFILES_CURRENT``, and then creating a Variable ``RS_PROFILES_NEW`` with the amended/added profile listed in the Environment variable ``PROFILE``.

The result is the JSON PATCH which is part of the Body of the PATCH RESTful call, which would look like this:

```javascript
[
	{
		"op": "test",
		"path": "/Profiles",
		"value": {{RS_PROFILES_CURRENT}}
	},
	{
		"op": "replace",
		"path": "/Profiles",
		"value": {{RS_PROFILES_NEW}}
	}
]
```

Note the use of the Postman Variables to complete the PATCH Body of the request.


NOTES
-----

The Digital Rebar Platform API relies extensively on the JSON PATCH operations.  This means to insure atomicty and safety guarantees, you must first get the current state of a JSON Field that you would like to change, then modify the field with the new values.

This method guarantees that you will only modify a Field from a given start point to an intended destination.  If some one/thing makes an API, CLI, or Web Portal call that changes the object on you, the JSON PATCH operation will fail, protecting against unintended effects.


TODO
----

This needs to be rewritten to take better advantage of reusable components.  Currently, a lot of the "GET" operations are duplicated, and not very well laid out for reusability or future modification.



