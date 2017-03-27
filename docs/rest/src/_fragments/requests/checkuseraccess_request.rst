Request
-------

The request for an |operation| call is JSON (as specified in :rfc:`4627`) containing the following properties:

User
    An **object** representing the person we would like to check access for, represented by a provider and Id.

Provider / Id Object
~~~~~~~~~~~~~~~~~~~~

..  include:: /_fragments/person_provider_id.rst

Sample request
~~~~~~~~~~~~~~

A sample request to check a user's permissions on this file:

..  literalinclude:: /_fragments/activities/CheckUserAccessRequest.json
    :language: JSON
