# Google_agenda neuron for Kalliope

## Synopsis

Get your next meetings from your google agenda

## Installation

kalliope install --git-url git@github.com:bacardi55/kalliope-google-calendar.git

## Options

| parameter          | required | default | choices | comment                                                                                                                                                                               |
|--------------------|----------|---------|---------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| credentials_file   | yes      |         |         | The json file downloaded on google calendar API, see the "Step 1: Turn on the Google Calendar API" of this page: https://developers.google.com/google-apps/calendar/quickstart/python |
| client_secret_file | yes      |         |         | The file where the oauth credentials will be written                                                                                                                                  |
| scopes             | yes      |         |         | The scopes of the api, in this case: https://www.googleapis.com/auth/calendar.readonly                                                                                                |
| application_name   | yes      |         |         | The name of your app as setup in google calendar api manager                                                                                                                          |
| max_results        | yes      |         | integer | The number of event you want to retrieve                                                                                                                                              |
| locale             | yes      |         |         | Your locale (eg: fr_FR.UTF-8). needs to be an installed locale on your system!                                                                                                        |
| file_template      | yes      |         |         | Template file to use                                                                                                                                                                  |
| meeting_intro_msg  | yes      |         |         | Message said before listing events                                                                                                                                                    |
| no_meeting_msg     | yes      |         |         | Message said in case of no next events found                                                                                                                                          |


## Return Values

| Name    | Description                                                                                                                                                                                          | Type   | sample |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------|--------|
| message | Plain text intro message (either meeting_intro_msg or no_meeting_msg)                                                                                                                                | string |        |
| events  | A list of events. Each event has the following information: event['summary'], event['time']['weekday'], event['time']['day'], event['time']['month'], event['time']['hour'], event['time']['minute'] | list   |        |


## Synapses example

This synapse will look for the {{ query }} spelt by the user on Wikipedia
```
---
  - name: "Google-agenda-next"
    signals:
      - order: "quels sont mes prochains rendez-vous"
    neurons:
      - google_calendar:
          credentials_file: "/path/to/credentials.json"
          client_secret_file: "/path/to/client_secret.json"
          scopes: "https://www.googleapis.com/auth/calendar.readonly"
          application_name: "App name"
          max_results: 3
          locale: fr_FR.UTF-8 # needs to be an installed locale
          no_meeting_msg: "You have no coming meetings"
          meeting_intro_msg: "Your 3 next meetings are"
          file_template: "templates/fr_google_calendar.j2"

```

