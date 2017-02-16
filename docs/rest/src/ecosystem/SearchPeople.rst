
..  index:: WOPI requests; SearchPeople, SearchPeople

..  |operation| replace:: SearchPeople

..  _SearchPeople:

SearchPeople
============

..  default-domain:: http

..  post:: /wopi/ecosystem

    The |operation| operation returns a list of people related to the requesting user, possibly filtered to match a search term.

    :reqheader X-WOPI-Override:
        The **string** ``SEARCH_PEOPLE``. Required.

    :code 200: Success
    :code 400: Couldn't deserialize request
    :code 401: Invalid :term:`access token`
    :code 500: Server error
    :code 501: Operation not supported

    ..  include:: /_fragments/common_headers.rst

Response
--------

..  include:: /_fragments/json_response.rst


Required response properties
----------------------------

The following properties must be present in all |operation| responses:


ContainerPointer
~~~~~~~~~~~~~~~~

A JSON-formatted object containing the following properties:

..  include:: /_fragments/container_pointer.rst


Other response properties
-------------------------

ContainerInfo
~~~~~~~~~~~~~

..  include:: /_fragments/container_info.rst


Sample response
---------------

..  literalinclude:: /_fragments/responses/container_pointer_and_info.json
    :language: JSON
