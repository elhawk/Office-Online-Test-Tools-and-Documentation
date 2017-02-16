
..  index:: WOPI requests; AddActivities, AddActivities

..  |operation| replace:: AddActivities

..  _AddActivities:

AddActivities
=============

..  default-domain:: http

..  post:: /wopi/files/(file_id)/activities

    The |operation| API sends activities about the file to the host.  The host can use these activities to send users notifications about
    their documents -- for instance, that someone made comments.  The host can also choose to store these activities to enable an activity feed,
    or other features based on knowledge of past activities.

    ..  include:: /_fragments/common_params.rst

    :reqheader X-WOPI-Override:
        The **string** ``ADD_ACTIVITIES``. Required.

    :code 200: Success
    :code 400: Couldn't deserialize request. Should not be returned for activities of unknown type
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


Activity Object
---------------

A single activity is a JSON object with the following properties:

Type
    A **string** representing the activity type, so clients and servers can tell if they understand the activity.
    Currently, the activity types are:

    * comment
    * mention

Id
    A **string** identifying the activity uniquely within the upload batch

Created
    A **string** that represents the time the activity happens.  The time must be a UTC time, formatted in ISO 8601 round-trip format.
    For example, ``"2009-06-15T13:45:30.0000000Z"``.

AnchorId
    A **string** that represents the location of the content the activity is based on within the document.  Optional.  When present,
    the WOPI server can append this to the url in the notification using the TODO document and link to placeholder value.

Data
    An **object** with data that is particular to the activity type.

..  important::
    The WOPI server should use the access token of the user sending the batch of activities to attribute the activities in notifications,
    and save the user as the activity author if storing the activities.

Person
------

Activities may refer to people besides the activity's creator (inferred from the access token). These people are represented by a person object.
This person object may come from the host via the GetPeople APIs, or it may come from the document content such as comment author information.
In the latter case, we might not have any information but the user's name.  Clients should send as much information as they have.

A person has the following properties, all of which are optional.

Name
    A **string** of the user's friendly name.  Could be something like "Guest" or "Anonymous" for anonymous users.

Email
    A **string** of the user's email.

Id
    A **string** that the host can use, in the context of the provider, to uniquely identify the user.

Provider
    A **string** giving the context in which the Id can be used to idetnify the user.

Comment Activity
----------------

A comment activity has the following key/value pairs in its data object:

CommentText
    A **string** containing the text of the comment. Optional.

ParentAuthor
    A person **object** representing the author of the comment this comment is replying to, if applicable.  Optional.

Participants
    An **array** of person objects representing all the participants in the comment thread, if applicable.  Optional.

ContentAction
    A **string** with value "created", "updated", or "deleted".

Mention Activity
----------------

A mention activity has the following key/value pairs in its data object:

Mentionees
    An **array** of person objects representing the people mentioned.

ContentAction
    A **string** with value "created", "updated", or "deleted".

Response
--------

The response for an |operation| call is JSON (as specified in :rfc:`4627`) containing a single required property:

ActivityResponses
    An **array** of objects with the status of each added activity.

ActivityResponse Object
-----------------------

Each ActivityResponse object has the following properties

Id
    The **string** Id of the activity from the request batch.

Status
    An **integer** representing the status of adding the activity.  Possible values are:

    * 0 - Success
    * 1 - RetryableFailure
    * 2 - PermanentFailure

Message
    A **string** which the client can log. Optional.