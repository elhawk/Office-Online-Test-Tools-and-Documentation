
..  index:: WOPI requests; GrantUserAccess, GrantUserAccess

..  |operation| replace:: GrantUserAccess

..  _GrantUserAccess:

GrantUserAccess
===============

..  default-domain:: http

..  post:: /wopi/files/(file_id)

    The |operation| call requests that a user be granted access to the file.

    :reqheader X-WOPI-Override:
        The **string** ``GRANT_USER_ACCESS``. Required.

    :code 200: Success
    :code 400: Checked user was not found, or couldn't deserialize request
    :code 401: Invalid :term:`access token`
    :code 404: Resource does not exist / user unauthorized
    :code 500: Server error
    :code 501: Operation not supported

    ..  include:: /_fragments/common_headers.rst

Request
-------

The request for an |operation| call is JSON (as specified in :rfc:`4627`) containing the following properties:

User
    An **object** representing the person we would like to grant access to, represented by a provider and Id.

Provider / Id Object
~~~~~~~~~~~~~~~~~~~~

..  include:: /_fragments/person_provider_id.rst

Response
--------

People
    An **array** of person objects.

..  include:: /_fragments/person_object.rst