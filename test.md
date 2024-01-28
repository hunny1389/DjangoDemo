Step 1: Start a project with the following command

          django-admin startproject todo_site

Step 2:  Change the directory to todo_site.

          cd todo_site

Step 3: Create an app with the following command.

          python manage.py startapp todo

Step 4: To include the app in our project, we need to add a reference to its configuration class in the INSTALLED_APPS setting. 
        The TodoConfig class is in the todo/apps.py file, so its dotted path is 'todo.apps.TodoConfig'. Edit the mysite/settings.py 
        file and add that dotted path to the INSTALLED_APPS setting. It’ll look like this: 

                    INSTALLED_APPS = [
    "todo.apps.TodoConfig",
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
          ]

Step 5: Creating Models . Edit the todo/models.py file so it looks like this

          from django.db import models

          class Question(models.Model):
              question_text = models.CharField(max_length=200)
              pub_date = models.DateTimeField("date published")
          
          
          class Choice(models.Model):
              question = models.ForeignKey(Question, on_delete=models.CASCADE)
              choice_text = models.CharField(max_length=200)
              votes = models.IntegerField(default=0)

Step 6: Migrations Files to the Database. This creates the DB based on the models

          python manage.py makemigrations
          python manage.py migrate
Step 7: Creating an admin user. First we’ll need to create a user who can login to the admin site. Run the following command and follow along

          $ python manage.py createsuperuser

Step 8: Start the development server
          
          $ python manage.py runserver

Step 9: Make the todo app modifiable in the admin. we need to tell the admin that Question objects have an admin interface. 
        To do this, open the todo/admin.py file, and edit it to look like this:

          from django.contrib import admin
          from .models import Question          
          admin.site.register(Question)

Step 10: This is optional. Change TIME_ZONE to India timezone. Change the line in todo_site/settings.py to the below mentioned:

          TIME_ZONE = 'Asia/Kolkata'

Step 11: use Django’s generic views instead. To do so, open the polls/views.py file and change it like so:

          from django.http import HttpResponseRedirect
          from django.shortcuts import get_object_or_404, render
          from django.urls import reverse
          from django.views import generic
          
          from .models import Choice, Question
          
          
          class IndexView(generic.ListView):
              template_name = "polls/index.html"
              context_object_name = "latest_question_list"
          
              def get_queryset(self):
                  """Return the last five published questions."""
                  return Question.objects.order_by("-pub_date")[:5]
          
          
          class DetailView(generic.DetailView):
              model = Question
              template_name = "polls/detail.html"
          
          
          class ResultsView(generic.DetailView):
              model = Question
              template_name = "polls/results.html"
          
          
          def vote(request, question_id):
              # same as above, no changes needed.
              ...
                    

          
