# Create a Simple API Using Django REST Framework in Python

# Step 1: Navigate to any folder you want in order to create the django project, open the command prompt there and enter the following command:

        django-admin startproject SampleProject

# Step2: Navigate to the project folder and create a web app using the below command:

        python manage.py startapp MyApp

# Step 3: Open the settings.py file and add the below lines of code in the INSTALLED_APPS section

            'rest_framework',
             'myFirstAPI',
 
 
# Step4: Open views.py file inside myFirstAPI folder 
        
            from django.shortcuts import render
            from django.http import Http404
            from rest_framework.views import APIView
            from rest_framework.decorators import api_view
            from rest_framework.response import Response
            from rest_framework import status
            from django.http import JsonResponse
            from django.core import serializers
            from django.conf import settings
            import json

            @api_view(["POST"])
            def IdealWeight(heightdata):
                try:
                    height=json.loads(heightdata.body)
                    weight=str(height*10)
                    return JsonResponse("Ideal weight should be:"+weight+" kg",safe=False)
                except ValueError as e:
                    return Response(e.args[0],status.HTTP_400_BAD_REQUEST)

    The IdealWeight(heightdate) is the method that gets executed when API call is made. It has a simple logic to calculate weight(=height*10). The line return JsonRespone(…) will send the response back.

# Step5: Open urls.py file and add the below lines of code:

     from django.conf.urls import url
  	 from django.contrib import admin
	 from MyApp import views
	 urlpatterns = [
     url(r'^admin/', admin.site.urls),
     url(r'^idealweight/',views.IdealWeight)
	 ]

The line url(r^idealweight/,views.IdealWeight) basically tells us that the IdealWeight method will be called using the url http://<server ip>/idealweight/

# Step6: We can start the api with below commands in command prompt:

        python manage.py runserver

Finally, we can test the API using POSTMAN.


