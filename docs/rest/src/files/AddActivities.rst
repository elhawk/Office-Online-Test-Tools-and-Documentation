
..  index:: WOPI requests; AddActivities, AddActivities

..  |operation| replace:: AddActivities

..  _AddActivities:

AddActivities
=============

..  default-domain:: http

..  get:: /wopi/files/(file_id)/activities

    The |operation| sends activities about the file to the host.  The host can use these activities to send users notifications about
	their documents -- for instance, that someone made comments on a file that a user shared.  The host can also choose to store these 
	activities to enable an activity feed, or other features based on knowledge of past activities.

    ..  include:: /_fragments/common_params.rst

    :reqheader X-WOPI-Override:
        The **string** ``ADD_ACTIVITIES``. Required.

    :code 200: Success
    :code 401: Invalid :term:`access token`
    :code 404: Resource not found/user unauthorized
    :code 412: File is larger than **X-WOPI-MaxExpectedSize**
    :code 500: Server error

    ..  include:: /_fragments/common_headers.rst
