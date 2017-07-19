Person
~~~~~~

A person has the following properties.

Name
    A **string** of the user's friendly name. Required. May be blank.

PictureUrl
    A **string** with a url to a profile picture of the user. Optional.

..  include:: /_fragments/person_provider_id.rst

Relationships
-------------
Each person has several optional properties that may be set to describe the person's relationship to the activity.  As usual, all properties default to false and should not be included when they are false.

Mentioned
    A **boolean** property indicating this person was explicitly mentioned in the activity, for example via an @mention.

InThread
    A **boolean** property that indicates that this user was part of a threaded discussion but was not explicitly involved in this activity.  For example, a threaded comment discussion.

RepliedTo
    A **boolean** property that indicates that this user is the parent of a piece of content that this activity is replying to.  For example, a reply in a threaded comment discussion.

Creator
    A **boolean** property that indicates that this user is the person who created the activity.  This is omitted on AddActivities calls; the host should determine the creator via the access token used on the AddActivities request.
