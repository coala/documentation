Usage of cobot
==============

.. note::

Display all of the help commands that Hubot knows about
---------------------------------------------------------

    cobot help
    
::

    cobot help

Display all help comments that match <query>
----------------------------------------------

    cobot help <query>
    
::

    cobot help sss

Assigns issus <issus_link> to user
------------------------------------

    conbot assign <issus_link>
    
::

    cobot assign https://github.com/coala/coala/issues/3845

Unassign the user from the issus <issue_link>
------------------------------------------------

    cobot unassign <issus_link>
    
::

    cobot unssign https://github.com/coala/coala/issues/3845

Create a Github issus given the title and repository
-------------------------------------------------------

    cobot new issus
    
 ::
 
    cobot new issus cobot "Post a message if a user tries to assign an issue but hasn't accepted the invite"

Marks the given pull request as work in process/pending review
-----------------------------------------------------------------

    cobot mark (wip|pending) <pull URL>
    
::

    cobot mark wip https://github.com/coala/projects/pull/237

Returns the info we have on your topic
----------------------------------------

    cobot explain <topic>
    
::

    cobot explain fixed

Maintainers invite users to the coala organization
----------------------------------------------------

    cobot (invite|inv) <username> [to [team]]
    
::

    cobot invite Bob

Doesn't mind
--------------

    cobot <nevermind|nm> 
    
::

    cobot nevermind

Searches Wolfram Alpha for the answer to the question
-------------------------------------------------------

    cobot <wa|wolfram> <question>
    
::

    cobot wa sss

Searchs google for you
------------------------

    cobot lmgtfy <term>
    
::

    cobot lmgtfy coala

Make sure hubot still knows the rules
----------------------------------------

    cobot the rules
    
::

    cobot the rule

Real talk yo
--------------

    cobot ghetto
    
::

    cobot ghetto

