
..  index:: WOPI requests; CheckUserAccess, CheckUserAccess

..  |operation| replace:: CheckUserAccess

..  _CheckUserAccess:

CheckUserAccess
===============

..  default-domain:: http

..  post:: /wopi/files/(file_id)

    The |operation| call asks what kind of access one or more users have to the file.

    ..  include:: /_fragments/common_params.rst

    :reqheader X-WOPI-Override:
        The **string** ``CHECK_USER_ACCESS``. Required.

    :code 200: Success
    :code 400: Couldn't deserialize request
    :code 401: Invalid :term:`access token`
    :code 404: Resource does not exist / user unauthorized
    :code 500: Server error
    :code 501: Operation not supported

    ..  include:: /_fragments/common_headers.rst

..  include:: /_fragments/requests/checkuseraccess_request.rst

Response
--------

The response for an |operation| call is JSON (as specified in :rfc:`4627`) containing a single required property:

CheckUserAccessResponses
    An **array** of objects that describes the current permissions of each user in the request batch.

CheckUserAccessResponse Object
~~~~~~~~~~~~~~~~~~~~~~~

Each CheckUserAccessResponse object has the following properties:

Id
    The **string** Id of a user from the request batch.

Provider
    The **string** Provider of a user from the request batch.

Status
    An **integer** representing the status of checking this user's access.  Possible values are:

    * 0 - Success
    * 1 - UserDoesNotExist

Message
    A **string** which the client can log. Optional.

UserCanRead
    A **Boolean** of whether the user has read access to the file.  Required.

UserCanWrite
    A **Boolean** corresponding to what :ref:`CheckFileInfo` would return for :term:`UserCanWrite` when called for the User in the request.  Required.

As usual, all properties whose value is the default (0 or false) may be omitted.  For example, the status property may be omitted when it is 0 (indicating success) and users without a particular permission do not need to explicitly return false for that property.

Sample response
~~~~~~~~~~~~~~

A sample response describing the current permissions on this file for a set of users:

..  literalinclude:: /_fragments/activities/CheckUserAccessResponse.json
    :language: JSON
