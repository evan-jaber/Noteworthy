QUICK SETUP:

1) Install and activate virtual environment
In the root folder, on the terminal create a virtual environment.
 Terminal command: python -m venv [name of the environment (usually env)]
 Activate command: env/Scripts/activate

2) Creating and setting up Django Project
 a) Install django and all the main libraries : 
  a. pip install django 
  b. pip install djangorestframework django-cors-headers
  c. pip install djangorestframework-simplejwt
  d. pip install PyJWT
  e. python -m pip install Pillow
  f. pip install django-jazzmin
  
 b) Create project in terminal: django-admin startproject server
 c) Cd to the server folder
 d) Create an app in django in the terminal
  a. python manage.py startapp [name of the app 'api']
  
3) Create a react app using vite
Go back to the root folder and:
 a) npm create vite@latest client -- --template react
 b) cd client
 c) npm install

4) Open VS code and the run the servers
 a) In the root folder open VS code:
  a. code .
 b) Open two terminals and make sure your virtual environment is active
 c) Run django server
  a. cd to server
  b. python manage.py runserver
 d) Run react server
  a. cd to client
  b. npm run dev
 
  
 5) Set up the settings.py to include rest_framework and corsheaders
  Import these things on top of settings file: 
    from pathlib import Path
    from datetime import timedelta
    from dotenv import load_dotenv
    import os
    
  CORS_ALLOWED_ORIGINS = [
      "http://127.0.0.1:5173",
      "http://localhost:5173",
  ]
  
  #Application definition (add jazzmin on top)
  
  INSTALLED_APPS = [
      'jazzmin',
      'django.contrib.admin',
      'django.contrib.auth',
      'django.contrib.contenttypes',
      'django.contrib.sessions',
      'django.contrib.messages',
      'django.contrib.staticfiles',
      #External Apps
      'rest_framework_simplejwt.token_blacklist',
      'rest_framework',
      'corsheaders',
      #Internal Apps
      'api',
  ]
  
  MIDDLEWARE = [
      'django.middleware.security.SecurityMiddleware',
      'django.contrib.sessions.middleware.SessionMiddleware',
      "corsheaders.middleware.CorsMiddleware",
      'django.middleware.common.CommonMiddleware',
      'django.middleware.csrf.CsrfViewMiddleware',
      'django.contrib.auth.middleware.AuthenticationMiddleware',
      'django.contrib.messages.middleware.MessageMiddleware',
      'django.middleware.clickjacking.XFrameOptionsMiddleware',
  ]

6) import time delta format in settings.py
    a) from datetime import timedelta

7) add these lines in the end of the settings.py to configure jwt based auth
REST_FRAMEWORK = {
 'DEFAULT_AUTHENTICATION_CLASSES': (
 'rest_framework_simplejwt.authentication.JWTAuthentication',
 )
 }

SIMPLE_JWT = {
 'ACCESS_TOKEN_LIFETIME': timedelta(minutes=5),
 'REFRESH_TOKEN_LIFETIME': timedelta(days=50),
 'ROTATE_REFRESH_TOKENS': True,
 'BLACKLIST_AFTER_ROTATION': True,
 'UPDATE_LAST_LOGIN': False,
 'ALGORITHM': 'HS256',
 'VERIFYING_KEY': None,
 'AUDIENCE': None,
 'ISSUER': None,
 'JWK_URL': None,
 'LEEWAY': 0,
 'AUTH_HEADER_TYPES': ('Bearer',),
 'AUTH_HEADER_NAME': 'HTTP_AUTHORIZATION',
 'USER_ID_FIELD': 'id',
 'USER_ID_CLAIM': 'user_id',
 'USER_AUTHENTICATION_RULE':
 'rest_framework_simplejwt.authentication.default_user_authentication_rule',
 'AUTH_TOKEN_CLASSES': ('rest_framework_simplejwt.tokens.AccessToken',),
 'TOKEN_TYPE_CLAIM': 'token_type',
 'TOKEN_USER_CLASS': 'rest_framework_simplejwt.models.TokenUser',
 'JTI_CLAIM': 'jti',
 'SLIDING_TOKEN_REFRESH_EXP_CLAIM': 'refresh_exp',
 'SLIDING_TOKEN_LIFETIME': timedelta(minutes=5),
 'SLIDING_TOKEN_REFRESH_LIFETIME': timedelta(days=1),
 }


8) Install requierments
    a. activate env
    b. cd to server
    c. pip freeze > requirments.txt

9) Install django environ
    a. activate env
    b. cd to server
    c. pip install django-environ


#frontend setup starts headers

#install these packages while staying in root folder
a) npm i axios dayjs jwt-decode react-router-dom