# Welcome

Welcome to the [consoledock](https://www.consoledock.com) documentation. 

The console is an all-in-one platform for selling cloud GPUs. From customer billing to automated deployments, the documentation is in here :) 

## Run your own console

* `git clone https://github.com/fluidstackio/infinity` - Download the codebase.
* `cd infinity` - CD into the folder.
* `pip3 install -r requirements.txt` - Install pip3 resources.
* `flask run` - Run the console in Flask development mode.
* `git checkout -b new-branch` - Change directory into the new branch. Develop here and push when done back to the origin to see your changes reflected!

## File layout

    scheduler.py    # Runs every 10 minutes for cron tasks.
    runtime.txt     # Define the Python runtime for Heroku
    requirements.txt    # Pip repositories that should be installed
    kubernetes-config   # Coreweave kubernetes configuration
    .env            # Global variables
    LICENSE.txt
    .flaskenv
    .gitignore
    Procfile
    README.md
    app/
        index.md    # The documentation homepage.
        static      # Static resources
            ...     # Various files
        templates/  # HTML Jinja files
            ...     # Various files
        views/      # Python HTML files
            api/    # API files
                ... # Various files
            ...     # Various files
        utils/      # Utilities functions
            ...     # Various files
        config.py   # Get Python variables from the .env file
        __init__.py # Initialize directory
        ...         # Other markdown pages, images and other files.
