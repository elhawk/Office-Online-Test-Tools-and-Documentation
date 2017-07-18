ContentAction
    A **string** with value "created", "updated", or "deleted".

ContentId
    A **string** identifying the content this activity relates to in the document.  Maximum length 1024 unicode characters.

NavigationId
    Optional. A **string** that represents the location of the content that a client may use to present the activity to the user. Maximum 1024 unicode characters.
    This value is probably specific to a particular WOPI client and is probably not useful to the WOPI server.
    When present, the WOPI server can append this to the url in the notification using the TODO document and link to placeholder value.