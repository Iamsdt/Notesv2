---
Created by: Shudipto Trafder
Created time: 2024-04-04T17:52
Last edited by: Shudipto Trafder
Last edited time: 2024-04-04T17:53
---
```Python
import os
import uuid

from google.cloud.dialogflowcx_v3 import SessionsClient
from google.cloud.dialogflowcx_v3.types import session
from google.oauth2 import service_account

DIALOGFLOW_PROJECT_ID = "gpuworks"
DIALOGFLOW_LOCATION = "us-central1"
DIALOGFLOW_AGENT_ID = "6cd4af06-9e2a-480b-a6a9-920a63a5f369"


def get_dialogflow_response(client: SessionsClient, text: str,
                            session_id: str):
    language_code = "en-us"
    text_input = session.TextInput(text=text)
    query_input = session.QueryInput(text=text_input,
                                     language_code=language_code)

    session_path = client.session_path(
        DIALOGFLOW_PROJECT_ID,
        DIALOGFLOW_LOCATION,
        DIALOGFLOW_AGENT_ID,
        session_id,
    )

    request = session.DetectIntentRequest(session=session_path,
                                          query_input=query_input)

    response = client.detect_intent(request=request)

    return response.query_result


def get_detected_intent(results):
    return results.intent.display_name


def get_dialogflow_responses(results):
    output = []
    for msg in results.response_messages:
        output.extend(msg.text.text)

    return output


def get_match_intent(results):
    match = results.match
    try:
        return match.intent.display_name
    except Exception:
        return ""


def get_dialog_flow_params(results):
    match = results.match
    di = {}
    try:
        for i in match.parameters.items():
            try:
                di[i[0]] = i[1]
            except Exception:
                pass
    except Exception:
        pass

    return di


def get_client():
    DIALOGFLOW_CONFIG = os.path.join(
        "/home/shudipto/10xScale/RecruitRest/recruit",
        "config/dialgoflow.json")
    creds = service_account.Credentials.from_service_account_file(
        DIALOGFLOW_CONFIG)
    location_id = "us-central1"
    api_endpoint = f"{location_id}-dialogflow.googleapis.com:443"
    client_options = {"api_endpoint": api_endpoint}
    print(client_options)
    DIALOGFLOW_CLIENT = SessionsClient(credentials=creds,
                                       client_options=client_options)

    return DIALOGFLOW_CLIENT


def handle_text_response(clinet, text, session_id):
    res = get_dialogflow_response(clinet, text, session_id)

    intent = get_detected_intent(res)
    match_intent = get_match_intent(res)
    response = get_dialogflow_responses(res)
    params = get_dialog_flow_params(res)

    message = ""
    for text in response:
        message += text + "\n"

    print("\nResponse")
    print(message)
    print("Intent", intent)
    print("Match", match_intent)
    print("Params:", params)


if __name__ == "__main__":
    client = get_client()
    session_id = uuid.uuid4()
    while True:
        inp = input()
        if inp == "exit":
            break

        handle_text_response(client, inp, session_id)
```