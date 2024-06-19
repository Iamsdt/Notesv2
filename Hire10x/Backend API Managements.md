
# V1

API Merge:
New API: user/<userid />

```
path("user/settings/", UserSettings.as_view(), name="user settings"),  
path("user/me/", CurrentUsers.as_view(), name="CurrentUsers"),
path(  
    "user/team/teams/", TeamEmployeeView.as_view(), name="TeamEmployeeView"  
),  # * done  
path(  
    "user/team/subordinate/",  
    ManageEmployeeView.as_view(),  
    name="Manage employee",  
),  # * done  
path(  
    "user/team/sibling/",  
    SiblingEmployeeView.as_view(),  
    name="Manage sibling",  
),  # * done  
path(  
    "user/team/allmembers/",  
    GetEmployeeDetails.as_view(),  
    name="Get employee details",  
),  # * done  
path(  
    "user/team/manager/", AllManagerView.as_view(), name="manager"  
),  # * done  
path(  
    "user/team/immediate/manager/",  
    ImmediateManagerView.as_view(),  
    name="Immediate manager",  
)
path(  
    "user/update/", UpdateUserInfoView.as_view(), name="update info"  
),
path(  
    "contract/user/update/",  
    UpdateContractUser.as_view(),  
    name="Update user",  
),
```

Authorization: Check user is admin
path("user/teams/", GetAllUsers.as_view(), name="GetAllUsers"),


Merge: customer/user/
```
path("user/create/", AddNewUser.as_view(), name="Add new user"),
path(  
    "contract/admin/", AddNewAdminUser.as_view(), name="Add new admin user"  
),
path("contract/user/", AddNewContractUser.as_view(), name="Add new user"),
```


Merge: jds/history/
```
path(  
    "jds/history/incomplete/",  
    IncompleteJDHistoryView.as_view(),  
    name="JDHistory Incomplete",  
),  # o

path(  
    "jds/history/complete/",  
    CompleteJDHistoryView.as_view(),  
    name="CompleteJDHistoryView",  
),  # ok
```

Merge: jd/:jd:int/
```
path(  
    "jd/delete/", JDDeleteView.as_view(), name="JDDeleteView"  # ok  
),  # * done

path("jds/save/", JDSaveView.as_view(), name="JDSave"),  # done  
path("jd/resave/", UpdateJDSaveView.as_view(), name="JDSave"),  # done
path("jd/details/", JDDetailsView.as_view(), name="JD Details"),
```


## DB Merge:
1. t_cv_matching_with_jd
2. t_cv_jd_mappings (keep)
Keep column:
ranking_score = models.FloatField(default=0.0)
