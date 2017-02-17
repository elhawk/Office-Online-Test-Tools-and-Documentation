
..  index:: WOPI requests; CheckUserAccess, CheckUserAccess

..  |operation| replace:: CheckUserAccess

..  _CheckUserAccess:

CheckUserAccess
===============

..  default-domain:: http

..  post:: /wopi/files/(file_id)

    The |operation| call asks what kind of access a user has to the file.

    ..  include:: /_fragments/common_params.rst

    :reqheader X-WOPI-Override:
        The **string** ``CHECK_USER_ACCESS``. Required.

    :resheader X-WOPI-UserNotFound:
        ..  include:: /_fragments/headers/X-WOPI-UserNotFound.rst

    :code 200: Success
    :code 400: Checked user was not found, or couldn't deserialize request
    :code 401: Invalid :term:`access token`
    :code 404: Resource does not exist / user unauthorized
    :code 500: Server error
    :code 501: Operation not supported

    ..  include:: /_fragments/common_headers.rst

..  include:: /_fragments/requests/checkuseraccess_request.rst

Response
--------

The response for an |operation| call is JSON (as specified in :rfc:`4627`) containing the following properties:

UserCanRead
    A **Boolean** of whether the user has read access to the file.  Required.

UserCanWrite
    A **Boolean** corresponding to what :ref:`CheckFileInfo` would return for :term:`UserCanWrite` when called for the User in the request.  Required.

RestrictedWebViewOnly
    A **Boolean** corresponding to what :ref:`CheckFileInfo` would return for :term:`RestrictedWebViewOnly` when called for the User in the request.  Optional.

UserCanAttend
    A **Boolean** corresponding to what :ref:`CheckFileInfo` would return for :term:`UserCanAttend` when called for the User in the request.  Optional.

UserCanNotWriteRelative
    A **Boolean** corresponding to what :ref:`CheckFileInfo` would return for :term:`UserCanNotWriteRelative` when called for the User in the request.  Optional.

UserCanPresent
    A **Boolean** corresponding to what :ref:`CheckFileInfo` would return for :term:`UserCanPresent` when called for the User in the request.  Optional.

UserCanRename
    A **Boolean** corresponding to what :ref:`CheckFileInfo` would return for :term:`UserCanRename` when called for the User in the request.  Optional.

WebEditingDisabled
    A **Boolean** corresponding to what :ref:`CheckFileInfo` would return for :term:`WebEditingDisabled` when called for the User in the request.  Optional.