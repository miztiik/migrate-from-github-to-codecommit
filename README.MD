# Migrate from Github to AWS CodeCommit
You can migrate an existing Git repository to a CodeCommit repository. This demos shows you how to migrate a project hosted on another Git repository to CodeCommit.

![Fig : Migrate from Github to AWS CodeCommit](https://raw.githubusercontent.com/miztiik/serverless-kms-sentry/master/images/serverless-kms-sentry.png)

#### Follow this article in [Youtube](https://youtu.be/UYaV-VfnbT8)

## Prerequisites
1. Setup CodeCommit [Get help here](https://www.youtube.com/watch?v=78KM7AXN4AA)

## Customize your variables
```sh
migration_dir="./_trash"
git_url="https://github.com/miztiik/lex-faq-bot.git"
aws_region="eu-central-1"
codecommit_repo_name="lex-faq-bot"
```

## Initiate Migration
```sh
# Create CodeCommit Repo
aws codecommit create-repository --repository-name ${codecommit_repo_name} --repository-description "My shiny new chat bot"

# Clone Git to local (only for migration purposes; not for local development)
git clone --mirror ${git_url} ${migration_dir}

# Push the repo to CodeCommit
cd ${migration_dir}
git push ssh://git-codecommit.${aws_region}.amazonaws.com/v1/repos/${codecommit_repo_name} --all
git push ssh://git-codecommit.${aws_region}.amazonaws.com/v1/repos/${codecommit_repo_name} --tags

# CleanUp - Remove local copy
rm -rf ${migration_dir}
```