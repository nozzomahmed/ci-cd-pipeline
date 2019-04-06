# aws-ci-cd-pipeline-github
AWS Cloudformation that creates ci/cd pipeline supported by github as a code
storage and source of events.

First deployment of this stack on cloudformation has to be done manually in
order to make it work.

Make sure to update default values in the parameters to make the stack
deployable non-interactively.

You have to create SecretsManager record to store Github token as well.
