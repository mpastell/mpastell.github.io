Changing defaults
_________________

Default chunk options are stored in `pweave.rcParams["chunk"]["defaultoptions"]`
dictionary. You can manipulate the dictionary to change the options.

**Have a look at current defaults:**


.. code-block:: python

    import pweave
    import pprint
    pprint.pprint(pweave.rcParams["chunk"])


::

    {'defaultoptions': {'caption': False,
                        'complete': True,
                        'display_data': True,
                        'display_stream': True,
                        'dpi': 200,
                        'echo': True,
                        'evaluate': True,
                        'f_env': None,
                        'f_pos': 'htpb',
                        'f_size': (6, 4),
                        'f_spines': True,
                        'fig': True,
                        'include': True,
                        'name': None,
                        'option_string': '',
                        'results': 'verbatim',
                        'term': False,
                        'wrap': 'output'}}
    



**Change wrapping off and default figure position to "h!"**


.. code-block:: python

    pweave.rcParams["chunk"]["defaultoptions"].update({'wrap' : False, 'f_pos' : "h!"})
    #Updated options
    pprint.pprint(pweave.rcParams["chunk"])


::

    {'defaultoptions': {'caption': False,
                        'complete': True,
                        'display_data': True,
                        'display_stream': True,
                        'dpi': 200,
                        'echo': True,
                        'evaluate': True,
                        'f_env': None,
                        'f_pos': 'h!',
                        'f_size': (6, 4),
                        'f_spines': True,
                        'fig': True,
                        'include': True,
                        'name': None,
                        'option_string': '',
                        'results': 'verbatim',
                        'term': False,
                        'wrap': False}}
    


