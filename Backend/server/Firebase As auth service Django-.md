---
Created by: Shudipto Trafder
Created time: 2023-10-18T20:24
Last edited by: Shudipto Trafder
Last edited time: 2023-12-04T20:42
tags:
  - django
  - firebase
---
This configuration will work in django

1. Create a firebase authentication file, with `authentication.BaseAuthentication`

`authentication.py`

```Plain
from django.utils import timezone
from rest_framework import authentication
from rest_framework.authtoken.admin import User

from api.db.user_model import UserTable
from recruit.exceptions import NoAuthToken, InvalidAuthToken, FirebaseError, InvalidUserAuth
from firebase_admin import auth


class FirebaseAuthentication(authentication.BaseAuthentication):
    def authenticate(self, request):
        auth_header = request.META.get("HTTP_AUTHORIZATION")
        if not auth_header:
            raise NoAuthToken("No auth token provided")

        id_token = auth_header.split(" ").pop()
        decoded_token = None
        try:
            decoded_token = auth.verify_id_token(id_token)
        except Exception:
            raise InvalidAuthToken("Invalid auth token")

        try:
            uid = decoded_token['uid']
        except Exception:
            raise FirebaseError()

        try:
            user = User.objects.get(username=uid)
            return user, None
        except UserTable.DoesNotExist:
            raise InvalidUserAuth()

```

### Now use it in django

`setting`

```Plain
'DEFAULT_AUTHENTICATION_CLASSES': [
        'recruit.authentication.FirebaseAuthentication',
        # 'rest_framework.authentication.TokenAuthentication',
    ],
```

### To use in the view

```Plain
class LikeView(GenericAPIView):

    permission_classes = [IsAuthenticated]
```

don't mention any type of authencation. Just pass permission class as `IsAuthenticated`