# Github Workflows


## Events that will trigger workflows:
https://docs.github.com/en/actions/reference/events-that-trigger-workflows



## Important environment variables:
## When pushing:
GITHUB_SHA = The ID of the commit that was pushed, unless deleting a branch
GITHUB_REF = The ID of the current branch



## Dispatch event:
https://docs.github.com/en/rest/reference/repos#create-a-repository-dispatch-event

POST request to:
https://api.github.com/repos/{owner}/{repo_name}/dispatches
https://api.github.com/repos/KenjiEmura/GitHub-Actions/dispatches

Inside your .yaml file, you have to add the 'repository_dipatch' hook after the 'on':
```
on:
  repository_dispatch:
    types: [webhook]
```

Auth:
Github API key

Header:
Accept -> application/vnd.github.v3+json

Body:
"event_type": "custom_event_name"
client_payload is a JSON payload with extra information about the webhook event that your action or worklow may use, for example:
"client_payload": {
  "build_type": "production",
  "description": "Some additional information..."
}



## Filter pattern:
https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions#filter-pattern-cheat-sheet



## Github ENV variables and encryption:
https://docs.github.com/en/actions/reference/environment-variables

To encrypt your ENV variables, you can simply add them to the Secrets (inside the settings of the repository)
and access them via the ${{ secrets.YOUR_SECRET_HERE }}, so for example if we have to put an API_KEY, we will do this:
```
  env:
    API_KEY: ${{ secrets.YOUR_SECRET_HERE }}
```



## Authentication in a workflow
https://docs.github.com/en/actions/reference/authentication-in-a-workflow

Without setting any secret, we have access to the ${{ secrets.GITHUB_TOKEN }} for authentication.

