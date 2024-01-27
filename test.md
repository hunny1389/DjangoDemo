Step 1: Start a project with the following command

          django-admin startproject todo_site

Step 2:  Change the directory to todo_site.

          cd todo_site

Step 3: Create an app with the following command.

          python manage.py startapp todo

Step 4: To include the app in our project, we need to add a reference to its configuration class in the INSTALLED_APPS setting. 
        The PollsConfig class is in the polls/apps.py file, so its dotted path is 'polls.apps.PollsConfig'. Edit the mysite/settings.py 
        file and add that dotted path to the INSTALLED_APPS setting. It’ll look like this: 
