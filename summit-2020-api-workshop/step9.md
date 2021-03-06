# Send Tweets to the Global Events API

The final part of our startup file will be to send any tweets that we get to the Global Events endpoint.

We will need to use the [Events API](https://developer.pagerduty.com/api-reference/reference/events-v2/openapiv3.json/paths/~1enqueue/post) for this.

Fill out the `send_twitter_statuses_to_events_API()` function in `startup.py`

## Completed Code

```python
def send_twitter_statuses_to_events_API(integration_key, statuses):
    print("Send Twitter Statuses to Events API.")
    session = EventsAPISession(integration_key)

    for status in statuses:
        print("Triggering on Events API")
        response = session.trigger(
            f"Matching tweet from user @{status['user']['screen_name']}",
            "twitter.com",
            severity="info",
            custom_details=status)
```{{copy}}

## Run the server again

`flask run`{{execute}}

### You should see: Triggering on Events API

```
Starting Up!
Get or create Escalation Policy
Found 1 escalation policy: PXXXXXX
Got an Escalation Policy Id: PXXXXXX
Get or Create Service.
Found already existing service.
Got a Service Id: PXXXXXX
Get Events Integration Key.
Get existing Ruleset
Got an Integration Key: RXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
Create Event Rule.
Event Rule already exists, moving on.
Event Rule Created!
Querying Twitter...
Twitter returned 1 tweets.
Send Twitter Statuses to Events API.
Triggering on Events API
```

Press Command-C or Ctrl-C to quit the loop

### Need a shortcut

You can use this command to copy over completed code and skip this step.

`cp ../completed/completed-startup-step9.py startup.py && flask run`{{execute}}

**Close the file editor, and click here to refresh it** -> `./app/skeleton/startup.py`{{open}}
