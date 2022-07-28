# Slack tips

## Slack API

### Get a user ID
![slack-id.png](slack-id.png "slack-id.png")


###  [Text formatting](https://api.slack.com/reference/surfaces/formatting)

#### [Links](https://api.slack.com/reference/surfaces/formatting#linking-urls)

```markdown
<example.com|Text>
```

Markdown equivalent

```markdown
[Text](example.com)
```

Email links

```markdown
<mailto:bob@example.com|Email Bob Roberts>
```



## Automated message on the last Thursday of the month

- `/remind` doesn’t work for “last Thursday of the month” 😥

1. Add the `IFTTT` slack app
    2. [The IFTTT date/time doesn't support this](https://superuser.com/a/1338315/1028339)
3. Create a 
    4. ![slack-automated-message-ifttt.png](slack-automated-message-ifttt.png)