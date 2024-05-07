---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:26
Last edited by: Shudipto Trafder
Last edited time: 2023-10-18T20:28
tags:
  - firebase
  - http
---
```Python
import superset.app
from flask import redirect, g, flash, request
from flask_appbuilder.security.views import UserDBModelView, AuthDBView
from superset.security import SupersetSecurityManager
from flask_appbuilder.security.views import expose
from flask_appbuilder.security.manager import BaseSecurityManager
from flask_login import login_user, logout_user
from flask_appbuilder.security.sqla.models import User
import requests
import random
import string
import os
import json


class FirebaseHelper:
    def __init__(self):
        self.firebase_api_key = os.environ.get('FIREBASE_API_KEY')

    def verify_token(self, token):
        # url = f"https://identitytoolkit.googleapis.com/v1/accounts:signInWithCustomToken?key={self.firebase_api_key}"
        # res = requests.post(
        #     url, json={"token": token, "returnSecureToken": True}
        # )
        # if res.status_code != 200:
        #     return {
        #         'status': False,
        #         'message': res.json().get('error', {}).get('message', 'Token verification failed')
        #     }

        # id_token = res.json().get('idToken', "")
        # if not id_token:
        #     return {
        #         'status': False,
        #         'message': 'Token verification failed'
        #     }

        # now get all the data
        url = f"https://www.googleapis.com/identitytoolkit/v3/relyingparty/getAccountInfo?key={self.firebase_api_key}"
        data = {
            "idToken": token
        }
        res2 = requests.post(url, json=data)
        if res2.status_code != 200:
            return {
                'status': False,
                'message': res2.json().get('error', {}).get('message', 'Token verification failed')
            }

        users = res2.json().get('users', [])
        if not users:
            return {
                'status': False,
                'message': 'Token verification failed'
            }
        user = users[0]

        # verify user is admin or manager
        user = users[0]
        print("user", user)
        # verify user is admin or manager
        rolejs = user.get('customAttributes', "{}")
        rd = json.loads(rolejs)
        role = rd['role'] if rd else ""
        if role.upper() not in ['ADMIN', 'MANAGER']:
            return {
                'status': False,
                'message': 'User is not admin or manager, please contact with admin'
            }

        return {
            'status': True,
            'message': 'Token verification success',
            'data': user
        }

    def using_email_password(self, username, password):
        url = f"https://identitytoolkit.googleapis.com/v1/accounts:signInWithPassword?key={self.firebase_api_key}"
        res = requests.post(
            url, json={
                "email": username,
                "password": password,
                "returnSecureToken": True
            }
        )
        print(res.json())
        if res.status_code != 200:
            return {
                'status': False,
                'message': res.json().get('error', {}).get('message', 'Not able to login')
            }

        id_token = res.json().get('idToken', "")
        if not id_token:
            return {
                'status': False,
                'message': 'Token verification failed'
            }

        # now get all the data
        url = f"https://www.googleapis.com/identitytoolkit/v3/relyingparty/getAccountInfo?key={self.firebase_api_key}"
        data = {
            "idToken": id_token
        }
        res2 = requests.post(url, json=data)
        print(res2.json())
        if res2.status_code != 200:
            return {
                'status': False,
                'message': 'Token verification failed'
            }

        users = res2.json().get('users', [])
        if not users:
            return {
                'status': False,
                'message': 'Token verification failed'
            }
        user = users[0]
        print("user", user)
        # verify user is admin or manager
        rolejs = user.get('customAttributes', "{}")
        rd = json.loads(rolejs)
        role = rd['role'] if rd else ""

        print(role)
        if role.upper() not in ['ADMIN', 'MANAGER']:
            return {
                'status': False,
                'message': 'User is not admin or manager, please contact with admin'
            }

        return {
            'status': True,
            'message': 'Token verification success',
            'data': user
        }


class CustomAuthDBView(AuthDBView):
    login_template = 'appbuilder/general/security/login_db.html'

    @expose('/login/', methods=['GET', 'POST'])
    def login(self):
        redirect_url = self.appbuilder.get_url_for_index
        if request.args.get('redirect') is not None:
            redirect_url = request.args.get('redirect')

        if request.args.get('token') is not None:
            user_token = request.args.get('token', "")
            firebase_helper = FirebaseHelper()
            token_verification = firebase_helper.verify_token(user_token)
            print(token_verification)
            if not token_verification['status']:
                flash(token_verification['message'], 'warning')
                return super(CustomAuthDBView, self).login()

            # its successful not check flask user exits or not
            user = self.appbuilder.sm.find_user(username=token_verification['data']['email'])
            if not user:
                flash("User not found, please contact with support", 'warning')
                return super(CustomAuthDBView, self).login()

            # clear all sessions
            # self.appbuilder.sm.res
            login_user(user, remember=True)
            return redirect(redirect_url)
        elif g.user is not None and g.user.is_authenticated:
            return redirect(redirect_url)
        else:
            return super(CustomAuthDBView, self).login()


class CustomSecurityManager(SupersetSecurityManager):
    authdbview = CustomAuthDBView

    def __init__(self, appbuilder):
        super(CustomSecurityManager, self).__init__(appbuilder)
        self.appbuilder = appbuilder

    # Disable default login and logout
    def auth_user_oauth(self, user):
        pass

    def is_token_login(self):
        return True

    def auth_user_db(self, username, password):
        firebase_helper = FirebaseHelper()
        res = firebase_helper.using_email_password(username, password)
        print(res)
        if not res['status']:
            flash(res['message'], 'warning')
            return None

        user = res['data']
        email = user.get('email', "")
        if not email:
            flash("Email not found", 'warning')
            return None
        # get user from db
        user = self.find_user(username=email)
        if not user:
            flash("User not found", 'warning')
            return None
        # clear all sessions
        # self.appbuilder.sm.reset_user_login_session(user)
        return user

    def auth_user_remote_user(self, user):
        pass
```

The provided code seems to be a Python script related to Firebase authentication with HTTP. It includes the following classes and functions:

- `FirebaseHelper`: This class is responsible for verifying tokens and handling authentication using email and password. It has methods like `verify_token` and `using_email_password` to interact with the Firebase Authentication API.
- `CustomAuthDBView`: This class extends the `AuthDBView` class from Flask-AppBuilder and provides a custom login view. It includes a `login` method that handles token verification and user authentication based on the token.
- `CustomSecurityManager`: This class extends the `SupersetSecurityManager` class and provides custom authentication methods. It includes methods like `auth_user_db` and `auth_user_remote_user` to authenticate users based on email and password or remote user, respectively.

The code also imports various libraries and modules such as `superset.app`, `flask`, `flask_appbuilder`, `superset.security`, `flask_login`, `flask_appbuilder.security.sqla.models`, `requests`, `random`, `string`, `os`, and `json`.

Please note that the documentation for the code is not explicitly provided in the selection. If you need specific documentation for any of the classes or methods mentioned above, please let me know.