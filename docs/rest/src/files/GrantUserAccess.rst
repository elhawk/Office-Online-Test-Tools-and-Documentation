
..  index:: WOPI requests; GrantUserAccess, GrantUserAccess

..  |operation| replace:: GrantUserAccess

..  _GrantUserAccess:

GrantUserAccess
===============

..  default-domain:: http

..  post:: /wopi/files/(file_id)

    The |operation| call requests that one or more users be granted a particular type of access to the file. This API is purely additive and cannot be used to revoke a user's existing permissions.

    ..  include:: /_fragments/common_params.rst

    :reqheader X-WOPI-Override:
        The **string** ``GRANT_USER_ACCESS``. Required.

    :code 200: Success
    :code 400: Couldn't deserialize request
    :code 401: Invalid :term:`access token`
    :code 404: Resource does not exist / user unauthorized
    :code 500: Server error
    :code 501: Operation not supported

    ..  include:: /_fragments/common_headers.rst

Request
-------

The request for an |operation| call is JSON (as specified in :rfc:`4627`) containing the following properties:

Users
    An **array** of user **objects** representing the people we would like to grant access to, each represented by a provider and Id.  Required.

GrantReadAccess
    A **Boolean** indicating that every user should gain the ability to read the file.  Optional.

GrantWriteAccess
    A **Boolean** indicating that every user should gain the ability to write to the file, corresponding to the :term:`UserCanWrite` property of :ref:`CheckFileInfo`.  Optional.

Scenario
    A **string** that a WOPI client might include to provide more details about the reason that access is being granted. For example, a host might choose to notify a user when a file is explicitly shared with them but might not send a notification when they were granted access by being mentioned in a comment because they expect to send a notification from a corresponding :ref:`AddActivities` operation.
    Valid values: "mention", "share". Unrecognized values should be ignored without error.

The permissions specified are to be applied to each user in the batch. Different combinations of permissions cannot be specified for each user. If a WOPI client wants to specify different permissions for some users it must separate those users into another request.

Provider / Id Object
~~~~~~~~~~~~~~~~~~~~

..  include:: /_fragments/person_provider_id.rst

Sample request
~~~~~~~~~~~~~~

A sample request to grant read and write access to a user:

..  literalinclude:: /_fragments/activities/GrantUserAccessRequest.json
    :language: JSON

Response
--------

The response for an |operation| call is JSON (as specified in :rfc:`4627`) containing a single required property:

GrantUserAccessResponses
    An **array** of objects with the status of each added activity.

GrantUserAccessResponse Object
~~~~~~~~~~~~~~~~~~~~~~~

Each GrantUserAccessResponse object has the following properties:

Id
    The **string** Id of a user from the request batch.

Provider
    The **string** Provider of a user from the request batch.

Status
    An **integer** representing the status of granting this user access.  Possible values are:

    * 0 - Success
    * 1 - CannotGrantPermission
    * 2 - UserDoesNotExist

Message
    A **string** which the client can log. Optional.

Sample response
~~~~~~~~~~~~~~~
A sample response to the sample request.  The server failed the edit activity because it does not support the edit type.  The comment activities succeeded.

..  literalinclude:: /_fragments/activities/GrantUserAccessResponse.json
    :language: JSON