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
Nonetheless, a secret can only be 64kb, so in that case we will need to encrypt and decrypt 'large' files that hold those secrets. Another case scenario is for example a CLI that takes as an argument the path to a file that contains all the keys and secrets, for example there might be a service that we want to use that instead of having the next structure `android deploy API_KEY_KEY` it might have this form `android deploy /folder1/folder2/ my_secret.json`. In this case, the file might be below 64kb, but since the command that we want to use requires us to pass in a path to a file, we are being forced to commit and push that ` my_secret.json` file. This will be another case in which we might need to use encryption and decryption of files.
https://docs.github.com/en/actions/reference/encrypted-secrets

For that we can use a tool called GnuPG (https://www.gnupg.org/) which can be easily installed using `brew install gnupg`

After installing it, we can run the next command to encrypt our file:
`$ gpg --symmetric --cipher-algo AES256 my_secret.json`

We then set our passphrase and to decrypt the file while running remotely inside the workflow, we can use:
`gpg --quiet --batch --yes --decrypt --passphrase="$PASSPHRASE" --output $HOME/decrypted.json my_secret.json.gpg`



## Authentication in a workflow
https://docs.github.com/en/actions/reference/authentication-in-a-workflow
Without setting any secret, we have access to the ${{ secrets.GITHUB_TOKEN }} for authentication.



## Expressions ${{  }} context and functions
You can put variables and also functions inside `${{}}`.

The objects created by Github and available inside an expression are called **context**, so for example, in `${{ secrets.PASSPHRASE }}`, the context will be the 'secrets' context. In the link below, you can find a list of all available context:
https://docs.github.com/en/actions/reference/context-and-expression-syntax-for-github-actions

We also have some fuctions that we can run inside the expressions, for a more detailed explanation, check the official documentation:
https://docs.github.com/en/actions/reference/context-and-expression-syntax-for-github-actions#functions



