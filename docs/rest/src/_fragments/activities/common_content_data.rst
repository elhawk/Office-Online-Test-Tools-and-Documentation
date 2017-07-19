ContentAction
    A **string** with value "created", "updated", or "deleted".

ContentId
    A **string** identifying the content this activity relates to in the document.  Maximum length 1024 unicode characters.

NavigationId
    Optional. A **string** that represents the location in the document where the activity happened (a deep link). Maximum 1024 unicode characters.
    The format of this value is specific to a particular WOPI client or file type and is probably not useful to the WOPI server.
    When present, the WOPI server can append this to the url in the notification using the (TODO: document and link to placeholder) parameter in discovery.