
..  index:: WOPI requests; CheckUserAccess (containers), CheckUserAccess (containers)

..  |operation| replace:: CheckUserAccess

..  _CheckUserAccess (containers):

CheckUserAccess (containers)
============================

..  default-domain:: http

..  post:: /wopi/containers/(container_id)

    The |operation| call asks what kind of access a user has to the file.

    ..  include:: /_fragments/common_containers_params.rst

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
    A **Boolean** of whether the user has read access to the container.  Required.

UserCanCreateChildContainer
    A **Boolean** corresponding to what :ref:`CheckContainerInfo` would return for :term:`UserCanCreateChildContainer` when called for the User in the request.  Optional.

UserCanCreateChildFile
    A **Boolean** corresponding to what :ref:`CheckContainerInfo` would return for :term:`UserCanCreateChildFile` when called for the User in the request.  Optional.

UserCanDelete
    A **Boolean** corresponding to what :ref:`CheckContainerInfo` would return for :term:`UserCanDelete` when called for the User in the request.  Optional.

UserCanRename
    A **Boolean** corresponding to what :ref:`CheckContainerInfo` would return for :term:`UserCanRename` when called for the User in the request.  Optional.