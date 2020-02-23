NOTE
----

Various Digital Rebar Platfrom (DRP) operational patterns for use in a Postman
tool.

REQUIRES
--------

Requires the DRP Endpoint and credentials are defined as Postman Variables.  Generally
speaking, use of an Environment for a given DRP Endpoint will specify these.  See the
``environments`` collections as an example.

Example Variable settings:

  * ``RS_ENDPOINT`` = ``https://10.10.10.10:8092``
  * ``RS_USERNAME`` = ``drpadmin``
  * ``RS_PASSWORD`` = ``PASSWORD``


OPERATION
---------

The following Postman Variables implement the various pattern change behaviors.

  * ``RS_UUID`` = the DRP Machine UUID object to modify
  * ``PROFILE`` = profile_to_change
  * ``WORKFLOW`` = workflow_to_set

The ``RS_UUID`` is the Machines UUID that will be modified.

The ``PROFILE`` defines the Profile to either be added or removed from the defined ``RS_UUID``.

The ``WORKFLOW`` defines the Workflow to set on the Machine.
