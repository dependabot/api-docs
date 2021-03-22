<p align="center">
  <img src="https://s3.eu-west-2.amazonaws.com/dependabot-images/logo-with-name-horizontal.svg?v5" alt="Dependabot" width="336">
</p>

# Dependabot API docs

Dependabot has a JSON API to make it easy to bulk-import projects. This API is also
used by the Dependabot dashboard.

**Please note that Dependabot cannot commit to maintaining backwards
compatibility of this API**. We will, however, update these docs
whenever breaking changes are made (likely to be infrequently). We recommend
you "watch" this repo to receive notifications of any changes.

## Authentication

Dependabot uses GitHub access tokens to authenticate users. To use the API:
- Create a [GitHub personal access token](https://github.com/settings/tokens)
  with `repo` permissions (so the token can see private repos)
- Add an `Authorization: Personal <token>` header to all requests using this
  access token

We use the access token you provide to ensure you have sufficient GitHub
permissions to undertake any actions you request through the Dependabot API.

## Endpoints

### Get Accounts

```
GET https://api.dependabot.com/accounts
```

Returns all Dependabot accounts that the authenticated user has access to.

<details>
<summary>Example response</summary>

```
{
    "data": [
        {
            "id": "27347476",
            "type": "accounts",
            "attributes": {
                "github-id": 27347476,
                "github-login": "dependabot",
                "github-account-type": "org",
                "access-granted-to-all-repos": true,
                "current-installation-id": 25920,
                "plan-name": "free",
                "plan-number": 7,
                "free-trial-end-date": null,
                "automatically-rebase-prs": true,
                "update-run-time": "05:00",
                "create-merge-commits": false,
                "weekly-update-run-day": "monday",
                "limit-initial-update-runs": true,
                "limit-open-pull-requests": true
            }
        },
        {
            "id": "1144873",
            "type": "accounts",
            "attributes": {
                "github-id": 1144873,
                "github-login": "greysteil",
                "github-account-type": "user",
                "access-granted-to-all-repos": true,
                "current-installation-id": 132882,
                "plan-name": "free",
                "plan-number": 7,
                "free-trial-end-date": null,
                "automatically-rebase-prs": true,
                "update-run-time": "02:15",
                "create-merge-commits": true,
                "weekly-update-run-day": "monday",
                "limit-initial-update-runs": true,
                "limit-open-pull-requests": true
            }
        }
    ]
}
```

</details>

### Get Repos for an account

```
GET https://api.dependabot.com/repos?account-id=27347476&account-type=org&installation-state=active
```

Returns active or inactive repos for the specified account.

#### Breaking change introduced 2019-12-02

- The `installation-state` param **must** be `active` or `inactive`
- `inactive` repos are paginated (100 repos per page)
  - Pass the `page=num` param to paginate the results (defaults to `page=1`)
  - The next page number is returned in the response: `response.meta.pages.next`

<details>
<summary>Example response</summary>

```
{
    "data": [
        {
            "id": "93163073",
            "type": "repos",
            "attributes": {
                "github-id": 93163073,
                "name": "dependabot-core",
                "installation-state": "active",
                "private": false,
                "fork": false,
                "github-url": "https://github.com/dependabot/dependabot-core",
                "primary-language": "ruby",
                "default-branch": "master",
                "using-config-file":true
            },
            "relationships": {
                "update-configs": {
                    "data": [
                        {
                            "id": "1332",
                            "type": "update-configs"
                        },
                        {
                            "id": "5061",
                            "type": "update-configs"
                        },
                        {
                            "id": "275",
                            "type": "update-configs"
                        },
                        {
                            "id": "879",
                            "type": "update-configs"
                        },
                        {
                            "id": "1672",
                            "type": "update-configs"
                        },
                        {
                            "id": "326",
                            "type": "update-configs"
                        },
                        {
                            "id": "3123",
                            "type": "update-configs"
                        }
                    ]
                },
                "account": {
                    "data": {
                        "id": "27347476",
                        "type": "accounts"
                    }
                }
            }
        },
        {
            "id": "131328855",
            "type": "repos",
            "attributes": {
                "github-id": 131328855,
                "name": "dependabot-script",
                "installation-state": "active",
                "private": false,
                "fork": false,
                "github-url": "https://github.com/dependabot/dependabot-script",
                "primary-language": "ruby",
                "default-branch": "master",
                "using-config-file":true
            },
            "relationships": {
                "update-configs": {
                    "data": [
                        {
                            "id": "4925",
                            "type": "update-configs"
                        }
                    ]
                },
                "account": {
                    "data": {
                        "id": "27347476",
                        "type": "accounts"
                    }
                }
            }
        }
    ],
    "included": [
        {
            "id": "1332",
            "type": "update-configs",
            "attributes": {
                "language": "javascript",
                "package-manager": "npm_and_yarn",
                "update-schedule": "live",
                "directory": "/helpers/npm",
                "automerge-rule-runtime-deps": "semver:patch",
                "automerge-rule-development-deps": "semver:minor",
                "target-branch": null,
                "lockfile-only": false,
                "security-updates-only": false
            },
            "relationships": {
                "repo": {
                    "data": {
                        "id": "93163073",
                        "type": "repos"
                    }
                }
            }
        },
        {
            "id": "5061",
            "type": "update-configs",
            "attributes": {
                "language": "java",
                "package-manager": "gradle",
                "update-schedule": "daily",
                "directory": "/helpers/gradle",
                "automerge-rule-runtime-deps": "never",
                "automerge-rule-development-deps": "never",
                "target-branch": null,
                "lockfile-only": false,
                "security-updates-only": false
            },
            "relationships": {
                "repo": {
                    "data": {
                        "id": "93163073",
                        "type": "repos"
                    }
                }
            }
        },
        {
            "id": "275",
            "type": "update-configs",
            "attributes": {
                "language": "php",
                "package-manager": "composer",
                "update-schedule": "live",
                "directory": "/helpers/php",
                "automerge-rule-runtime-deps": "semver:patch",
                "automerge-rule-development-deps": "semver:patch",
                "target-branch": null,
                "lockfile-only": false,
                "security-updates-only": false
            },
            "relationships": {
                "repo": {
                    "data": {
                        "id": "93163073",
                        "type": "repos"
                    }
                }
            }
        },
        {
            "id": "879",
            "type": "update-configs",
            "attributes": {
                "language": "javascript",
                "package-manager": "npm_and_yarn",
                "update-schedule": "live",
                "directory": "/helpers/yarn",
                "automerge-rule-runtime-deps": "semver:patch",
                "automerge-rule-development-deps": "semver:minor",
                "target-branch": null,
                "lockfile-only": false,
                "security-updates-only": false
            },
            "relationships": {
                "repo": {
                    "data": {
                        "id": "93163073",
                        "type": "repos"
                    }
                }
            }
        },
        {
            "id": "1672",
            "type": "update-configs",
            "attributes": {
                "language": "python",
                "package-manager": "pip",
                "update-schedule": "live",
                "directory": "/helpers/python",
                "automerge-rule-runtime-deps": "semver:patch",
                "automerge-rule-development-deps": "semver:patch",
                "target-branch": null,
                "lockfile-only": false,
                "security-updates-only": false
            },
            "relationships": {
                "repo": {
                    "data": {
                        "id": "93163073",
                        "type": "repos"
                    }
                }
            }
        },
        {
            "id": "326",
            "type": "update-configs",
            "attributes": {
                "language": "ruby",
                "package-manager": "bundler",
                "update-schedule": "live",
                "directory": "/",
                "automerge-rule-runtime-deps": "semver:patch",
                "automerge-rule-development-deps": "semver:patch",
                "target-branch": null,
                "lockfile-only": false,
                "security-updates-only": false
            },
            "relationships": {
                "repo": {
                    "data": {
                        "id": "93163073",
                        "type": "repos"
                    }
                }
            }
        },
        {
            "id": "3123",
            "type": "update-configs",
            "attributes": {
                "language": "elixir",
                "package-manager": "hex",
                "update-schedule": "live",
                "directory": "/helpers/elixir",
                "automerge-rule-runtime-deps": "semver:patch",
                "automerge-rule-development-deps": "semver:patch",
                "target-branch": null,
                "lockfile-only": false,
                "security-updates-only": false
            },
            "relationships": {
                "repo": {
                    "data": {
                        "id": "93163073",
                        "type": "repos"
                    }
                }
            }
        },
        {
            "id": "4925",
            "type": "update-configs",
            "attributes": {
                "language": "ruby",
                "package-manager": "bundler",
                "update-schedule": "daily",
                "directory": "/",
                "automerge-rule-runtime-deps": "never",
                "automerge-rule-development-deps": "never",
                "target-branch": null,
                "lockfile-only": false,
                "security-updates-only": false
            },
            "relationships": {
                "repo": {
                    "data": {
                        "id": "131328855",
                        "type": "repos"
                    }
                }
            }
        }
    ]
}
```

</details>

### Create an Update Config for a repo

```
POST https://api.dependabot.com/update_configs

{
  "repo-id": 93163073,
  "package-manager": "bundler",
  "update-schedule": "daily",
  "directory": "/",
  "account-id": "27347476",
  "account-type": "org",
}
```

Creates an update config. The following parameters can be passed:

| Attribute                         | Default        | Description                                  |
|-----------------------------------|----------------|----------------------------------------------|
| `repo-id`                         | None (required)| The GitHub ID of the repository              |
| `account-id`                      | None (required)| The GitHub ID of the repository owner        |
| `account-type`                    | None (required)| `org` or `user`                              |
| `directory`                       | None (required)| The directory of the dependency files. Normally `/` |
| `update-schedule`                 | None (required)| One of `live`, `daily`, `weekly` or `monthly` |
| `package-manager`                 | None (required)| One of `bundler`, `composer`, `docker`, `maven`, `npm_and_yarn`, `elm`, `submodules`, `hex`, `cargo`, `gradle`, `nuget`, `dep`, `go_modules`, `pip`, `terraform`, `github_actions` |
| `target-branch`                   | GitHub default | The branch to create PRs against |
| `lockfile-only`                   | false          | Ignore updates that are out-of-range of the manifest file |
| `security-updates-only`           | false          | Only generate PRs for updates that fix a security vulnerability |
| `automerge-rule-development-deps` | `never`        | One of `never`, `security:patch`, `semver:patch`, `semver:minor`, `in_range` or `all` |
| `automerge-rule-runtime-deps`     | `never`        | One of `never`, `security:patch`, `semver:patch`, `semver:minor`, `in_range` or `all` |


### Update an existing Update Config

```
PATCH https://api.dependabot.com/update_configs/:id

{
  "update-schedule": "live",
  "target-branch": "dev",
  "lockfile-only": true,
  "security-updates-only": false,
  "update-schedule": "daily",
  "automerge-rule-development-deps": "semver:patch",
  "automerge-rule-runtime-deps": "semver:minor"
}
```

Update an update config, for example, to change its update schedule.


### Delete an existing Update Config

```
DELETE https://api.dependabot.com/update_configs/:id
```

Delete an update config.


### Notify Dependabot of a private dependency release

```
POST https://api.dependabot.com/release_notifications/private

{
  "name": "your_dependency_name",
  "version": "1.5.0"
  "package-manager": "bundler"
}
```

Notifies Dependabot of a private dependency release. In response, Dependabot
will check all of the repos that belong to an organization your access token has
access to. If any use an outdated version of the dependency Dependabot will
create update PRs for them.

Note that this API is *not* a substitute for Dependabot being able to access
your registry. When notified of a new version Dependabot triggers update runs
which will query your registry for the latest version.

The `name` attribute should be the name of the dependency. For Java dependencies
the name is constructed from the `groupId` and `artifactId` of the dependency,
joined by a `:` (for example: `org.kohsuke:github-api`).

This endpoint is useful to get immediate updates to private dependencies.
However, if you release a new version of a private dependency but don't notify
Dependabot then it will still pick it up the following morning.
