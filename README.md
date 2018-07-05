![Dependabot](https://dependabot.com/images/dependabot-logo-full.svg)

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

Returns all repos for the specified account. Allowed states are `active` and `inactive`.

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
                "default-branch": "master"
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
                "default-branch": "master"
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
                "automerge-rule-runtime-deps": "patch",
                "automerge-rule-development-deps": "minor",
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
                "automerge-rule-runtime-deps": "patch",
                "automerge-rule-development-deps": "patch",
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
                "automerge-rule-runtime-deps": "patch",
                "automerge-rule-development-deps": "minor",
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
                "automerge-rule-runtime-deps": "patch",
                "automerge-rule-development-deps": "patch",
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
                "automerge-rule-runtime-deps": "patch",
                "automerge-rule-development-deps": "patch",
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
                "automerge-rule-runtime-deps": "patch",
                "automerge-rule-development-deps": "patch",
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

Creates an update config. In addition, the following parameters can also be
passed:

| Attribute                        | Default        | Description                                  |
|----------------------------------|-----------------------|----------------------------------------------|
| `target-branch`                    | GitHub default | The branch to create PRs against. |
| `lockfile-only`                    | false          | Ignore updates that are out-of-range of the manifest file. |
| `security-updates-only`            | false          | Only generate PRs for updates that fix a security vulnerability. |
| `automerge-rule-development-deps`  | "never"        | One of "never", "security", "patch", or "minor". |
| `automerge-rule-runtime-deps`     | "never"        | One of "never", "security", "patch", or "minor". |


### Update an existing Update Config

```
PATCH https://api.dependabot.com/update_configs/:id

{
  "update-schedule": "live",
  "target-branch": "dev",
  "lockfile-only": true,
  "security-updates-only": false,
  "update-schedule": "daily",
  "automerge-rule-development-deps": "patch",
  "automerge-rule-runtime-deps": "minor"
}
```

Update an update config, for example to change its update schedule.
