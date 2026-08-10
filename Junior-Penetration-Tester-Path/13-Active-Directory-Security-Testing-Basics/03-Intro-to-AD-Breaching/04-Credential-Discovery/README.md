# 04 - Credential Discovery

## Overview

Explored how credentials can be discovered in exposed
Git repositories and CI/CD services.

## Topics Covered

- Credential discovery
- Git repositories
- Git commit history
- Configuration files
- Hardcoded secrets
- CI/CD pipelines
- Jenkins
- Build logs
- Environment variables
- Workspace files
- TruffleHog
- Git grep
- Jenkins API

## Git Credential Discovery

Credentials may remain in Git history even after they have
been removed from the latest version of a file.

Important locations to investigate:

- Commit history
- Configuration files
- Source code
- CI/CD pipeline definitions

Common files include:

    .env
    web.config
    appsettings.json
    config.php
    database.yml
    Jenkinsfile
    .gitlab-ci.yml
    .github/workflows/*.yml

## Git History

Search commit history for sensitive keywords:

    git log -p | grep -i "password\|secret\|token\|key\|credential"

Automated scanning:

    trufflehog git file:///path/to/repo

## Jenkins Credential Discovery

Jenkins may expose credentials through:

- Build console output
- Job configuration
- Environment variables
- Workspace files

Build logs can contain:

- Environment variables
- Connection strings
- Deployment commands
- Credentials

## Jenkins API

Build console output can also be retrieved through the
Jenkins API:

    curl http://ci.thm.loc/job/JOB_NAME/lastBuild/consoleText | grep -i "password\|secret\|token\|credential"

## Practical Methodology

### Git

1. Locate accessible repository.
2. Inspect current files.
3. Review commit history.
4. Search for credentials and secrets.
5. Check configuration files.
6. Review CI/CD definitions.

### Jenkins

1. Access Jenkins.
2. Review build history.
3. Inspect console output.
4. Review job configuration.
5. Check environment variables.
6. Inspect workspace files.

## Other Potential Sources

Credentials may also appear in:

- Internal wikis
- Documentation portals
- Network-share configuration files
- LDAP anonymous binds
- SNMP community strings

## Key Takeaways

Removing a secret from the latest Git commit does not remove
it from Git history.

CI/CD systems such as Jenkins can also expose credentials
through logs, configurations and build environments.