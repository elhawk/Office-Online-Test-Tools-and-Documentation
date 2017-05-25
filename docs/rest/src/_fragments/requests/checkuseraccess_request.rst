Request
-------

The request for an |operation| call is JSON (as specified in :rfc:`4627`) containing the following properties:

Users
    An **array** of User **objects** representing the people whose access  we would like to check, each represented by a provider and Id.

Provider / Id Object
~~~~~~~~~~~~~~~~~~~~

..  include:: /_fragments/person_provider_id.rst

Sample request
~~~~~~~~~~~~~~

A sample request to check the permissions of several users on this file:

..  literalinclude:: /_fragments/activities/CheckUserAccessRequest.json
    :language: JSON
