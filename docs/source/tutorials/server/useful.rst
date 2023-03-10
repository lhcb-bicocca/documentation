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
