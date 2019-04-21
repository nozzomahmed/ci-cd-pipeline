# aws-ci-cd-pipeline-github
AWS Cloudformation template that creates ci/cd pipeline supported by Github as
a code storage and source of events.

This stack is designed to create pipeline that will deploy itself and another
stack.

First deployment of this stack on cloudformation has to be done manually in
order to make it work.

Make sure to update default values in the parameters to make the stack
deployable non-interactively.

You have to create SecretsManager record to store Github token as well. Things
to do:
- Create new secret for Github token with one key. You can name the key "Token".
To get token from Github go to https://github.com/settings/tokens and generate
one.
- Provide secret's name and key to the template's parameters before runtime.
