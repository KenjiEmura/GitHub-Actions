# Events that will trigger workflows:
https://docs.github.com/en/actions/reference/events-that-trigger-workflows

# Important environment variables:
## When pushing:
GITHUB_SHA = The ID of the commit that was pushed, unless deleting a branch
GITHUB_REF = The ID of the current branch

# Dispatch event:
https://docs.github.com/en/rest/reference/repos#create-a-repository-dispatch-event

POST request to:
https://api.github.com/repos/{owner}/{repo_name}/dispatches
https://api.github.com/repos/KenjiEmura/GitHub-Actions/dispatches

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

# Filter pattern:
https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions#filter-pattern-cheat-sheet

