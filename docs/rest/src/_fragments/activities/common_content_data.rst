ContentAction
    A **string** with value "created", "updated", or "deleted".

ContentId
    A **string** identifying the content this activity relates to in the document.  Maximum length 2048 unicode characters.

NavigationId
    A **string** that represents the location of the content the activity is based on within the document. Optional.  Maximum length 2048 unicode characters.
    When present, the WOPI server can append this to the url in the notification using the TODO document and link to placeholder value.