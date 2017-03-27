
..  index:: WOPI requests; GrantUserAccess, GrantUserAccess

..  |operation| replace:: GrantUserAccess

..  _GrantUserAccess:

GrantUserAccess
===============

..  default-domain:: http

..  post:: /wopi/files/(file_id)

    The |operation| call requests that a user be granted access to the file.

    ..  include:: /_fragments/common_params.rst

    :reqheader X-WOPI-Override:
        The **string** ``GRANT_USER_ACCESS``. Required.

    :code 200: Success
    :code 400: Requested user was not found, or couldn't deserialize request
    :code 401: Invalid :term:`access token`
    :code 403: User does not have permission to grant the requested user the requested access.
    :code 404: Resource does not exist / user unauthorized
    :code 410: The user whose permissions are being modified does not exist
    :code 500: Server error
    :code 501: Operation not supported

    ..  include:: /_fragments/common_headers.rst

Request
-------

The request for an |operation| call is JSON (as specified in :rfc:`4627`) containing the following properties:

User
    An **object** representing the person we would like to grant access to, represented by a provider and Id.  Required.

UserCanRead
    A **Boolean** of whether we would like the user to have read access to the file.  Optional.

UserCanWrite
    A **Boolean** corresponding to what we would like :ref:`CheckFileInfo` to return for :term:`UserCanWrite` when called for the User in the request.  Optional.

Provider / Id Object
~~~~~~~~~~~~~~~~~~~~

..  include:: /_fragments/person_provider_id.rst

Sample request
~~~~~~~~~~~~~~

A sample request to grant read and write access to a user:

..  literalinclude:: /_fragments/activities/GrantUserAccessRequest.json
    :language: JSON

