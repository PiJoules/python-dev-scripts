# python-scripts
Scripts helpful for python development.

## Setup
Add the following to your `.bashrc` to make these commands available globally.
```sh
source /path/to/python-dev-scripts/_setup_venv_scripts
```

## _switch_virtualenv
Creates and switches to a new virtual environment. Just switches if the venv exists.
This creates a dedicated hidden directory in your home dir (`/home/$USER/.venvs`)
where all venvs created by this script will be placed.

The default python version used is whatever is represented by the command `python`.

This way, you can use `tree` without having the screen get flooded with the contents of
the venv.

Pip is automatically upgraded to the latest available version when creating a new venv.

```sh
$ _switch_virtualenv venv  # Creates venv
(venv) $ _switch_virtualenv venv2  # Creates venv2
(venv2) $ _switch_virtualenv venv  # Just switches back to venv
```

To specify the python version, add the `-p` flag. The value provided to this must either
be a path to the python executable or an existing `python` command.
```sh
$ _switch_virtualenv venv -p python3.5  # Create venv using python3.5
$ _switch_virtualenv venv -p /usr/bin/python2.7  # Python version from path
```

To automatically install modules in a requirements file when creating a new venv,
add the `-r` flag to `_switch_virtualenv`.
```sw
$ _switch_virtualenv venv -r my_requirements.txt
```

If you run into any errors creating the inital virtualenv relating to pip, just run the same command again.
I have not yet looked into what's causing it, but running the same command seems to fix it and successfully
create the venv.

### Default modules
To install modules by default in a new venve created with `_switch_virtualenv`, include it in
the `requirements.txt` located in the same directory as the `_switch_virtualenv` script.

The following modules are located in this `requirements.txt` and installed by default:
- ipython
- requests


## _delete_virtualenv
Deletes a virtual environment created with _switch_virtualenv. If you are in the venv you are
about to delete, the venv is deactivated then deleted. If you are in a different venv from
the one you are deleting, the venv will just be deleted and you will remain in the current
venv.

```sh
$ _switch_virtualenv venv  # Create and switch to venv
(venv) $ _switch_virtualenv venv2  # Create and switch to venv2
(venv2) $ _delete_virtualenv venv  # Delete venv
(venv2) $ _delete_virtualenv venv2  # Deactivate and delete venv2
```


## _init_package
Creates files in the current directory for setting up a package.
Created files:
- README.md
- setup.py
- project directory
- requirements.txt
- dev-requirements.txt
- python .gitignore

```sh
$ _init_package project_name
```


##_setup_venv_scripts
Sets up autocompletion for `_switch_virtualenv` and `_delete_virtualenv`.
Hitting tab when using these scripts will list any existing virtualenvs in
`/home/$USER/.venvs`.


```sh
$ source _setup_venv_scripts
$ _switch_virtualenv venv
(venv) $ _switch_virtualenv v[TAB]
venv
(venv) $ _switch_virtualenv venv2
(venv2) $ _delete_virtualenv v[TAB]
venv venv2
```

