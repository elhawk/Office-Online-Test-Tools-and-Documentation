Activity Object
~~~~~~~~~~~~~~~

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


Creator
    A person **object** representing the activity creator.  Optional.

    ..  important:: The WOPI server should use the access token of the user sending the batch of activities to attribute the activities in notifications, and save the user as the activity author if storing the activities.  The creator should be ignored, if sent by the clients.  Creator is only used when the client queries activities.

Data
    An **object** with data that is particular to the activity type.


