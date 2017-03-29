
..  index:: WOPI requests; GrantUserAccess (containers), GrantUserAccess (containers)

..  |operation| replace:: GrantUserAccess

..  _GrantUserAccess (containers):

GrantUserAccess (containers)
============================

..  default-domain:: http

..  post:: /wopi/containers/(container_id)

    ..  include:: /_fragments/future_operation.rst

    The |operation| call requests that a user be granted access to the container. This API is purely additive and cannot be used to revoke a user's permissions.

    ..  note::
        The host can decide whether to make the access grant recursive.

    ..  include:: /_fragments/common_containers_params.rst

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
    A **Boolean** indicating the user should gain the ability to read the container.  Optional.

GrantCreateChildContainer
    A **Boolean** indicating the user should gain the ability to create child containers in this container, corresponding to the :term:`UserCanCreateChildContainer` property of :ref:`CheckContainerInfo`.  Optional.

GrantCreateChildFile
    A **Boolean** indicating the user should gain the ability to create child containers in this container, corresponding to the :term:`UserCanCreateChildFile` property of :ref:`CheckContainerInfo`.  Optional.

GrantDeleteAccess
    A **Boolean** indicating the user should gain the ability to create child containers in this container, corresponding to the :term:`UserCanDelete` property of :ref:`CheckContainerInfo`.  Optional.

Provider / Id Object
~~~~~~~~~~~~~~~~~~~~

..  include:: /_fragments/person_provider_id.rst