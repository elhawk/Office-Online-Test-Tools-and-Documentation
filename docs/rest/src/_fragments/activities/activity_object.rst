Activity Object
~~~~~~~~~~~~~~~

A single activity is a JSON object with the following properties:

Type
    A **string** representing the activity type, so clients and servers can tell if they understand the activity.
    Currently, the activity types are:

    * comment

    More activity types will certainly get added. Hosts should ignore activities with a type they do not understand. Hosts may also ignore any activity type that they understand but do not care about.

Id
    A UUID (universally unique identifier), represented as a **string** in the standard format described in :rfc:`4122` section 3.
    That is, it is a string of the form XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX, where X denotes a hexadecimal digit.

    WOPI clients should prefer lower case characters for hexadecimal values “a” through “f”.
    However, as described in :rfc:`4122`, WOPI hosts must parse the UUID string in a case-insensitive way.

Timestamp
    A **string** that represents the time the activity happened.  The time must be a UTC time, formatted in ISO 8601 round-trip format.
    For example, ``"2009-06-15T13:45:30.0000000Z"``.

People
    An **array** of person objects representing the people who were involved with this activity.  Optional.

    ..  important:: The WOPI server should use the access token of the user sending the batch of activities to attribute the activities in notifications, and save the user as the activity author if storing the activities.  The creator should be ignored, if sent by the clients.  Creator is only used when the client queries activities.

Data
    An **object** with data that is particular to the activity type.


