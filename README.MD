# publish-javadoc github action
## Goal
This action provides an easy and clean way of publishing JavaDocs to [jd.projectshard.dev](https://jd.projectshard.dev). 

The general URL format is `https://jd.projectshard.dev/PROJECT_NAME/VERSION`. The VERSION parameter can be replaced by `latest` which points to the most recently changed version.

## Usage
Inside the job, create a task that uses `projectshard/publish-javadoc`. See [releases](https://github.com/projectshard/publish-javadoc/tags) for latest version!

Use the [gradle ci-cd plugin](https://repo.projectshard.dev/#browse/browse:maven-releases:dev%2Fprojectshard%2Fbuild%2Fci-cd) for easy access to project name and version!

```yaml
  - name: 📣 Publish JavaDocs on server
    uses: projectshard/publish-javadoc@v0.0.12
    id: publish-jd
    with:
      JAVA_DOC_TEMP_DIR: build/docs/javadoc/
      PROJECT_NAME: MyProject
      PROJECT_VERSION: "1.0.0"
      SSH_KEY: ${{ secrets.SSH_KEY }}
```

### Input variables
* JAVA_DOC_TEMP_DIR - Location where JavaDoc files are stored
* PROJECT_NAME - Project name, used in published url
* PROJECT_VERSION - Project version, used in published url
* SSH_KEY - Private key to access the JavaDoc publish server 

Use [GitHub secrets](https://docs.github.com/en/actions/security-for-github-actions/security-guides/using-secrets-in-github-actions#about-secrets) to safely store the ssh key! 

### Output variables
* URL - URL to access the JavaDoc just published

```yaml
  - name: 📣 Announce new JavaDocs URL
    run: |
      echo "New JavaDocs URL: ${{ steps.publish-jd.outputs.url }}"
      
    # -> New JavaDocs URL: https://jd.projectshard.dev/MyProject/latest/
```