# Migrate from Github to AWS CodeCommit
You can migrate any existing Git repository to a CodeCommit repository. This demo shows you how to migrate a project hosted on  Git repository to CodeCommit.

![Fig : Migrate from Github to AWS CodeCommit](https://raw.githubusercontent.com/miztiik/migrate-from-github-to-codecommit/master/images/miztiik-github-to-codecommit.png)

#### Follow this article in [Youtube](https://www.youtube.com/watch?v=tRV2Yba_vHk&list=PLxzKY3wu0_FKuCD3X6Uc_XjCKXA5-zmIW&index=8)

## Prerequisites
1. Setup CodeCommit [Get help here](https://www.youtube.com/watch?v=78KM7AXN4AA)

## Migration Details
_Update the below values to match your requirements_
```sh
migration_dir="./_trash"
git_url="https://github.com/miztiik/lex-faq-bot.git"
aws_region="eu-central-1"
codecommit_repo_name="lex-faq-bot"
```

## Initiate Migration
```sh
# Create CodeCommit Repo
aws codecommit create-repository \
  --repository-name ${codecommit_repo_name} \
  --repository-description "My shiny new chat bot"

# Clone Git to local (only for migration purposes; not for local development)
git clone --mirror ${git_url} ${migration_dir}

# Push the repo to CodeCommit
cd ${migration_dir}
git push ssh://git-codecommit.${aws_region}.amazonaws.com/v1/repos/${codecommit_repo_name} --all
git push ssh://git-codecommit.${aws_region}.amazonaws.com/v1/repos/${codecommit_repo_name} --tags

# CleanUp - Remove local copy
rm -rf ${migration_dir}
```

## Support
Please open a [GitHub issue](https://github.com/miztiik/migrate-from-github-to-codecommit/issues/new).

## Feedback
Please open a [GitHub issue](https://github.com/miztiik/migrate-from-github-to-codecommit/issues/new). I do encourage you to contribute your changes and send me pull request.

##### References
[1] - [AWS Docs - Migrate a Git Repository](https://docs.aws.amazon.com/codecommit/latest/userguide/how-to-migrate-repository-existing.html)
