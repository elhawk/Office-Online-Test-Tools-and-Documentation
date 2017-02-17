
..  index:: WOPI requests; SearchPeople, SearchPeople

..  |operation| replace:: SearchPeople

..  _SearchPeople:

SearchPeople
============

..  default-domain:: http

..  post:: /wopi/ecosystem

    The |operation| operation returns a list of people related to the requesting user, possibly filtered to match a search term.

    ..  tip::
        To improve the user experience, hosts can optionally order the people returned to return relevant contacts earlier in the list.
        This can enable a user's most frequent contacts to be displayed first in an @mention people picker dropdown, for instance.

    ..  include:: /_fragments/access_token_param.rst

    :reqheader X-WOPI-Override:
        The **string** ``SEARCH_PEOPLE``. Required.

    :code 200: Success
    :code 400: Couldn't deserialize request
    :code 401: Invalid :term:`access token`
    :code 500: Server error
    :code 501: Operation not supported

    ..  include:: /_fragments/common_headers.rst

Request
-------

The request for an |operation| call is JSON (as specified in :rfc:`4627`) containing the following properties:

Top
    An **integer**, the maximum number of people to return.  Required.

    ..  note:: Hosts may define their own maximum number of people to return in a given response.  If top exceeds this value, hosts should return their own maximum, rather than failing the request.

Filter
    A **string** search term that the returned people should match.  Optional.

WopiSrc
    A **string** of a :term:`WOPISrc` with no access token.  Optional.

    ..  tip::
        The WopiSrc can be used by hosts to prioritize people relevant to the file -- for instance, people the file has been shared with --
        when returning people results.  Hosts can also ignore this property.

Response
--------

PeopleExceedTop
    A **boolean** indicating whether there were more people matching the filter than were returned in the response.

People
    An **array** of person objects.

..  include:: /_fragments/person_object.rst