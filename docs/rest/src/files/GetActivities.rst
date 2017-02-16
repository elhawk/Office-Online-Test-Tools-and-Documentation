
..  index:: WOPI requests; GetActivities, GetActivities

..  |operation| replace:: GetActivities

..  _GetActivities:

GetActivities
=============

..  default-domain:: http

..  post:: /wopi/files/(file_id)/activities

    The |operation| API queries activities from the WOPI host.

    ..  include:: /_fragments/common_params.rst

    :reqheader X-WOPI-Override:
        The **string** ``GET_ACTIVITIES``. Required.

    :code 200: Success
    :code 400: Couldn't deserialize request. Should not be returned for activities of unknown type, or unsupported filters.
    :code 401: Invalid :term:`access token`
    :code 404: Resource not found/user unauthorized
    :code 500: Server error
    :code 501: GetActivities is not supported

    ..  include:: /_fragments/common_headers.rst

Request
-------

The request for an |operation| call is JSON (as specified in :rfc:`4627`) containing the following properties:

Top
    An **integer** with the maximum number of activities we would like returned to us.  Required.

    ..  note:: Hosts should order activities most-recent first when returning the top N activities to the requesting client.

    ..  note:: Hosts may define their own maximum number of activities to return in a given response.  If top exceeds this value, hosts should return their own maximum, rather than failing the request.

SkipToken
    A **string** which is opaque to the clients.  This string is returned in the GetActivities response, and can be sent
    on subsequent GetActivities requests for paging. Optional.

TypeFilter
    An **array** of strings listing the activity types the client wants.  Optional.

    ..  note:: If hosts do not support filtering, return all activity types.  If the client does not provide a filter, return all activity types.  If some of the requested types are not understood by the host, return the ones that are understood.

Response
--------

The response for an |operation| call is JSON (as specified in :rfc:`4627`) containing the following properties:

Activities
    An **array** of objects representing the returned activities, defined below.

ItemsExceedTop
    A **Boolean** indicating whether there are more activities matching the filter than were returned.

SkipToken
    A **string** value which clients can send on subsequent GetActivities requests for paging.  Opaque to clients.  Optional.

HostActivityViewUrl
    A **string** url to the host's activity view page, if it has one.  Optional.

..  include:: /_fragments/activities/activity_object.rst

For more on the activity types and type-specific data, see :ref:`AddActivities`