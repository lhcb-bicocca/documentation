Useful Suggestions
==================

Screen
------
Screen is a command that creates a new terminal session and keeps it open even when the user logs out.
You can use it for running long-lasting jobs.

To start a screen session

.. code-block:: bash
  
  $ screen -S <name>
  
The only drawback of ``screen`` is that it uses ``CTRL+a`` to somehow give back control to the original shell (i.e.: use ``CTRL+a`` ``CTRL+d`` to detach the screen session), 
meaning that it won't be possible to use ``CTRL+a`` in the screen terminal.

For more details, see the `screen <https://www.gnu.org/software/screen/manual/screen.html>`_ user manual.

Screen and AFS
--------------
Sometimes it may be useful to open a screen session with automatically renewed AFS token.
For this purpose, one can add this function to the ``.bashrc`` file

.. code-block:: bash

  function afs_screen {
    # Start a screen session with automatically renewed AFS token.
    #
    #   afs_screen -S session_name
    #
    # Requirements:
    #  - You need a renewable kerberos ticket. Get one with:
    #      kinit -r 7d user@CERN.CH
    #    The default kinit on LXPLUS gives you a renewable ticket for 5 days.
    #  - Options are passed to the screen command. Many will not be compatible
    #    with the way screen is started. Use -S for naming the session.
  
    AKLOG=$(which aklog) krenew -t -K 10 -i -b -- sh -c "cd $(pwd) &&"' screen -D -m "$@"' -- "$@"
    #AKLOG=$(which aklog) krenew -t -K 10 -i -b -- screen -D -m "$@"
    
    # Command description
    # - AKLOG=... tell krenew where aklog is (required by -t flag)
    # - krenew -b changes directory to "/". If you don't care you can use the
    #   simpler commented out command. Otherwise, we need to remember where we
    #   were and change it back inside krenew. For this we need the extra
    #   sh layer. 
    # - krenew options:
    #   -K <N> check if ticket needs renewal every <N> minutes
    #   -t     run aklog after renewing a ticket
    #   -b     detach and run in the background
    #   -i     keep runnning krenew if ticket runs out of renewable lifetime
    # - screen options:
    #   -D -m  start in detached mode and do not fork. The command exits when
    #          screen terminates, which makes krenew exit, too.
  }


