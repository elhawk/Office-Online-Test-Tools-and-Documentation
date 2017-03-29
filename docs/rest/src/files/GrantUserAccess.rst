
..  index:: WOPI requests; GrantUserAccess, GrantUserAccess

..  |operation| replace:: GrantUserAccess

..  _GrantUserAccess:

GrantUserAccess
===============

..  default-domain:: http

..  post:: /wopi/files/(file_id)

    The |operation| call requests that a user be granted access to the file. This API is purely additive and cannot be used to revoke a user's permissions.

    ..  include:: /_fragments/common_params.rst

    :reqheader X-WOPI-Override:
        The **string** ``GRANT_USER_ACCESS``. Required.

    :code 200: Success
    :code 400: Couldn't deserialize request
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

GrantReadAccess
    A **Boolean** indicating the user should gain the ability to read the file.  Optional.

GrantWriteAccess
    A **Boolean** indicating the user should gain the ability to write to the file, corresponding to the :term:`UserCanWrite` property of :ref:`CheckFileInfo`.  Optional.

Scenario
    A **string** that a WOPI client might include to provide more details about the reason that access is being granted. For example, a host might choose to notify a user when a file is explicitly shared with them but might not send a notification when they were granted access by being mentioned in a comment because they expect to send a notification from a corresponding :ref:`AddActivities` operation.
    Valid values: "mention", "share". Unrecognized values should be ignored without error.

Provider / Id Object
~~~~~~~~~~~~~~~~~~~~

..  include:: /_fragments/person_provider_id.rst

Sample request
~~~~~~~~~~~~~~

A sample request to grant read and write access to a user:

..  literalinclude:: /_fragments/activities/GrantUserAccessRequest.json
    :language: JSON

