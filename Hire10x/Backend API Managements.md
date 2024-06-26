
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


# V2

Task details:
/v1/jd/shortlisted/ -> GET (JD -id, task type)
```
path("jds/tasks/", JDTasksView.as_view(), name="JD Tasks"),  
path(  
    "jds/tasks/contact/",  
    JDTasksContactView.as_view(),  
    name="JDTasksContactView",  
),  
path(  
    "jds/tasks/details/",  
    JDTaskDetailsView.as_view(),  
    name="JD Task Details",  
),  
path(  
    "jds/tasks/details/update/",  
    JDTaskDetailsUpdateView.as_view(),  
    name="JDTaskDetailsUpdateView",  
),
```

Post call also:

Table Changes:
1. remove t_jd_task_details
2. remove t_jd_linkedin_matching
3. New Table
```
class JdTaskTable(models.Model):  
    # ACCOUNT_SINGALHIRE = "SIGNALHIRE"  
    # ACCOUNT_CONNECT = "CONNECT"    # ACCOUNT_ENTERPRISE = "ENTERPRISE"    # ACCOUNT_FREE = "FREE"    #    # account_TYPE_OPTIONS = (    #     (ACCOUNT_ENTERPRISE, "ENTERPRISE"),    #     (ACCOUNT_SINGALHIRE, "SIGNALHIRE"),    #     (ACCOUNT_FREE, "FREE"),    # )    id = models.BigAutoField(primary_key=True)  
    jd = models.ForeignKey(  
        JDTable,  
        on_delete=models.CASCADE,  
        related_name="jdTask",  
        blank=True,  
        null=True,  
    )    company = models.ForeignKey(  
        CompanyTable,  
        on_delete=models.CASCADE,  
        related_name="jdTaskCompany",  
        blank=True,  
        null=True,  
    )    user = models.ForeignKey(  
        UserTable,  
        on_delete=models.CASCADE,  
        related_name="jdTaskUser",  
        blank=True,  
        null=True,  
    )    # template_id = models.ForeignKey(CompanyEmailTemplateModel, on_delete=models.DO_NOTHING to on_delete=models.DO_NOTHING, default=0)  
    template = models.ForeignKey(  
        CompanyEmailTemplateModel,  
        on_delete=models.DO_NOTHING,  
        blank=True,  
        null=True,  
        related_name="jd_task_template",  
        db_column="template_id",  
    )  
    cv = models.ForeignKey(  
        CandidateTable,  
        on_delete=models.CASCADE,  
        related_name="jd_task_cv",  
        blank=True,  
        null=True,  
    )  
    # cid = models.IntegerField(default=0, db_index=True)  
    link = models.CharField(default="", max_length=100, db_index=True)  
    # 0 -> nothing, 1 -> requested -> 2 -> success 3 -> not found  
    details_status = models.IntegerField(default=0)  
  
    # task type: Linkedin connect and linkedin contact  
    task_type = models.IntegerField(default=0)  
    # dates  
    created_at = models.DateTimeField(auto_now_add=True)  
    updated_at = models.DateTimeField(auto_now=True)  
  
    # status  
    status = models.IntegerField(default=1)  
  
    def __str__(self):  
        return str(self.id)  
  
    class Meta:  
        db_table = "t_jd_task"  
        unique_together = [["jd", "cv"]]
```


Check this:
path(  
    "jds/tasks/newJd/",  
    JDTasksAddedNewJDView.as_view(),  
    name="JDTasksAddedNewJDView",  
),

merge
```
path("cv/raw/", CVRawView.as_view(), name="CvNaukri"),  # done
path(  
    "cv/profile/card/",  
    ProfileDetailsCard.as_view(),  
    name="CV Profile Details Card",  
),  # done  
path(  
    "cv/profile/details/",  
    CandidateDetails.as_view(),  
    name="CV Details Profile",  
),  # done

path("cv/details/", CvDetailsView.as_view(), name="CVDetailsView"),  # done
```

Merge
```
path(  
    "cv/status/", CvStatusUpdate.as_view(), name="CVStatusUpdate"  
),  # done  
path(  
    "cv/status/all/", CvStatusAllUpdate.as_view(), name="CVStatusAllUpdate"  
),  # done
```

Merge:
```
path("cv/click/", CvClickView.as_view(), name="CVClick"),  # done
path("cv/count/", CvCountUpdate.as_view(), name="CVCountUpdate"),  # done
```

Merge:
```
path(  
    "cv/ranking/update/", AdjustRankingAlgo.as_view(), name="CVComments"  
),  # done #SHIVA: appwrite  
path("cv/ranking/", RunRankingAlgo.as_view(), name="CVComments"),
```

```
# not using  
path(  
    "send/email/all/", ContactAllCVEmailView.as_view(), name="CVAllContact"  
),  # done
```

```
path(  
    "settings/email/setup/",  
    SetupEmailView.as_view(),  
    name="SetupEmailView",  
),  
path(  
    "settings/email/incoming/setup/",  
    SetupIncomingEmailView.as_view(),  
    name="SetupIncomingEmailView",  
),
```

```
path(  
    "settings/email/test/",  
    TestSetupEmailView.as_view(),  
    name="TestSetupEmailView",  
),  
path(  
    "settings/email/incoming/test/",  
    TestIncomingEmailView.as_view(),  
    name="TestSetupIncomingEmailView",  
),
```

```
path(  
    "settings/candidates/constant/",  
    CandidateJourneyContactTypeView.as_view(),  
    name="Contact Type",  
),  # done  
path(  
    "settings/candidates/contact/",  
    CandidateContactTypeView.as_view(),  
    name="Contact Type",  
),  # done  
path(  
    "settings/candidates/journey/",  
    CandidateJourneyTypeView.as_view(),  
    name="Journey Type",  
),  # done
```

```
# not required  
path(  
    "resume/bulkprocess/start/",  
    BulkProcessingStartView.as_view(),  
    name="Bulk processing",  
),
```

```
path(  
    "linkedin/stats/",  
    LinkedinStatsView.as_view(),  
    name="LinkedinStatsView",  
),  # ok  
path(  
    "linkedin/stats/unique/",  
    LinkedinStatsUniqueView.as_view(),  
    name="LinkedinStatsView",  
),  # ok
```


```
path("workflow/", WorkflowView.as_view(), name="WorkflowView"),  
#     path('workflow/all/', WorkflowAllView.as_view(), name="WorkflowAllView"),  
#     path('workflow/create/', WorkflowCreateView.as_view(), name="WorkflowCreateView"),  
#     path('workflow/execute/', WorkflowNodeExecute.as_view(), name="WorkflowNodeExecute"),  
path(  
    "workflownode/update/",  
    WorkflowNodeUpdate.as_view(),  
    name="WorkflowNodeUpdate",  
),
```

```
path(  
    "homepage_integrations/status/",  
    HomepageIntegrationCandidateStatus.as_view(),  
    name="HomepageIntegrationStatusView",  
),  
path(  
    "homepage_integrations/sourcing/",  
    HomepageIntergrationSourcing.as_view(),  
    name="HomepageIntegrationSourcingView",  
),  
path(  
    "homepage_integrations/jd_details/",  
    ContinueWorking.as_view(),  
    name="ContinueWorking",  
),
```