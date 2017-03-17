
..  index:: WOPI requests; AddActivities, AddActivities

..  |operation| replace:: AddActivities

..  _AddActivities:

AddActivities
=============

..  default-domain:: http

..  post:: /wopi/files/(file_id)/activities

    The |operation| operation sends activities about the file to the host.  The host can use these activities to send users notifications about
    their documents -- for instance, that someone made comments.  The host can also choose to store these activities to enable an activity feed,
    or other features based on knowledge of past activities.

    ..  include:: /_fragments/common_params.rst

    :reqheader X-WOPI-Override:
        The **string** ``ADD_ACTIVITIES``. Required.

    :code 200: Success
    :code 400: Couldn't deserialize request. Should not be returned for activities of unknown type, even if the batch contained zero activities of known types.
    :code 401: Invalid :term:`access token`
    :code 404: Resource not found/user unauthorized
    :code 500: Server error
    :code 501: AddActivities is not supported

    ..  include:: /_fragments/common_headers.rst

Request
-------

The request for an |operation| call is JSON (as specified in :rfc:`4627`) containing a single required property:

Activities
    An **array** of activity objects, defined below.

..  include:: /_fragments/activities/activity_object.rst
..  include:: /_fragments/activities/comment_activity.rst

People
~~~~~~

Activities may refer to people besides the activity's creator (inferred from the access token). These people are represented by a person object.
This person object may come from the host via SearchPeople, or it may come from the document content such as comment author information.
In the latter case, we might not have any information but the user's name.  Clients should send as much information as they have.

..  include:: /_fragments/person_object.rst

Sample request
~~~~~~~~~~~~~~

A sample request consisting of two comments (one of which is a reply) and a mention is below.

..  literalinclude:: /_fragments/activities/AddActivitiesRequest.json
    :language: JSON

Response
--------

The response for an |operation| call is JSON (as specified in :rfc:`4627`) containing a single required property:

ActivityResponses
    An **array** of objects with the status of each added activity.

ActivityResponse Object
~~~~~~~~~~~~~~~~~~~~~~~

Each ActivityResponse object has the following properties

Id
    The **string** Id of the activity from the request batch.

Status
    An **integer** representing the status of adding the activity.  Possible values are:

    * 0 - Success
    * 1 - RetryableFailure
    * 2 - PermanentFailure
    * 3 - UnknownType

Message
    A **string** which the client can log. Optional.

Sample response
~~~~~~~~~~~~~~~
A sample response to the sample request.  The server failed the edit activity because it does not support the edit type.  The comment activities succeeded.

..  literalinclude:: /_fragments/activities/AddActivitiesResponse.json
    :language: JSON