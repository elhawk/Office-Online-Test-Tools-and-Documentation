
..  index:: WOPI requests; GrantUserAccess (containers), GrantUserAccess (containers)

..  |operation| replace:: GrantUserAccess

..  _GrantUserAccess (containers):

GrantUserAccess (containers)
============================

..  default-domain:: http

..  post:: /wopi/containers/(container_id)

    The |operation| call requests that a user be granted access to the container.

    ..  note::
        The host can decide whether to make the access grant recursive.

    ..  include:: /_fragments/common_containers_params.rst

    :reqheader X-WOPI-Override:
        The **string** ``GRANT_USER_ACCESS``. Required.

    :resheader X-WOPI-UserNotFound:
        ..  include:: /_fragments/headers/X-WOPI-UserNotFound.rst

    :code 200: Success
    :code 400: Requested user was not found, or couldn't deserialize request
    :code 401: Invalid :term:`access token`
    :code 404: Resource does not exist / user unauthorized
    :code 422: User does not have permission to grant the requested user the requested access.
    :code 500: Server error
    :code 501: Operation not supported

    ..  include:: /_fragments/common_headers.rst

Request
-------

The request for an |operation| call is JSON (as specified in :rfc:`4627`) containing the following properties:

User
    An **object** representing the person we would like to grant access to, represented by a provider and Id.  Required.

UserCanRead
    A **Boolean** of whether we would like to grant the user read access to the container.  Optional.

UserCanCreateChildContainer
    A **Boolean** corresponding to what we would like :ref:`CheckContainerInfo` to return for :term:`UserCanCreateChildContainer` when called for the User in the request.  Optional.

UserCanCreateChildFile
    A **Boolean** corresponding to what we would like :ref:`CheckContainerInfo` to return for :term:`UserCanCreateChildFile` when called for the User in the request.  Optional.

UserCanDelete
    A **Boolean** corresponding to what we would like :ref:`CheckContainerInfo` to return for :term:`UserCanDelete` when called for the User in the request.  Optional.

UserCanRename
    A **Boolean** corresponding to what we would like :ref:`CheckContainerInfo` to return for :term:`UserCanRename` when called for the User in the request.  Optional.

Provider / Id Object
~~~~~~~~~~~~~~~~~~~~

..  include:: /_fragments/person_provider_id.rst