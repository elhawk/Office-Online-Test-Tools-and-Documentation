
..  index:: WOPI requests; GetPeople, GetPeople

..  |operation| replace:: GetPeople

..  _GetPeople:

GetPeople
=========

..  default-domain:: http

..  post:: /wopi/ecosystem

    ..  include:: /_fragments/future_operation.rst

    The |operation| operation takes a list of people provider / id pairs, and returns full person information for them.

    ..  note::
        When the host cannot find one or more of the people in the request, it should simply not return a person
        for that provider / id in the response.  The request should still return Success.

    ..  include:: /_fragments/access_token_param.rst

    :reqheader X-WOPI-Override:
        The **string** ``GET_PEOPLE``. Required.

    :code 200: Success
    :code 400: Couldn't deserialize request
    :code 401: Invalid :term:`access token`
    :code 429: Too many requests, as per RFC 6585.  Hosts are encourage to set the Retry-After header too.
    :code 500: Server error
    :code 501: Operation not supported

    ..  include:: /_fragments/common_headers.rst

Request
-------

The request for an |operation| call is JSON (as specified in :rfc:`4627`) containing the following properties:

People
    An **array** of objects.  Each object contains a person provider and a person Id.

Provider / Id Object
~~~~~~~~~~~~~~~~~~~~

..  include:: /_fragments/person_provider_id.rst

Response
--------

People
    An **array** of person objects.

..  include:: /_fragments/person_object.rst