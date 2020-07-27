# Toumoro Slack Messaging

Interactive messaging services for Slack.

## Limitation

This action need a compatible backend using API Key from the header `X-API-Key`.

## Inputs

### `api_url`

**Required** API URL handling the messaging system.

### `api_key`

**Required** API KEY for authentication.

### `service`

**Required** Service using this action as `'github'`, `'gitlab'`, `'bitbucket'`.

### `project`

**Required** Name of the project.

### `channel`

**Required** Slack channel to post the message.

### `ref`

**Required** Repo reference as `GITHUB_REF`, `'refs/head/master'`, ...

### `run_id`

**Required** Runner ID as `GITHUB_RUN_ID`.

### `step`

**Required** Step triggering the call.

### `type`

**Required** Message type as (`'error'`, `'request'`, `'status'`).

### `status`

**Required** Inline status following the regex `(?(DEFINE)(?<status>\w*:(?:FAIL|PASS)))^(?&status)(?:;(?&status))*$` as `Build:PASS;Test:FAIL`.

### `issue_id`

**Required** Issue ID for internal reference.

### `actor`

**Required** Trigger Actor as `GITHUB_ACTOR`.

### `repository`

**Required** Repository as `GITHUB_REPOSITORY`, `'user/project'`.

### `workflow`

**Optional** Workflow reference for manual triggering, for GitHub it represent the workflow file name.

### `timestamp`

**Optional** Slack timestamp for editing a previous message.

### `verbose`

**Optional** Level of verbose, options: ['0', '1', '2'], default: '0'. **WARNING: Level 1 and 2 can print sensitive information.**

## Example usage

### GitHub Actions

```yml
jobs:
  tests:
  runs-on: ubuntu-latest
  steps:
    - uses: docker://kerberosmorphy/toumoro-slack-messaging:latest
      with:
        api_url: ${{ env.API_URL }}
        api_key: ${{ secrets.API_KEY }}
        service: github
        channel: my-channel
        ref: ${{ github.ref }}
        run_id: ${{ github.run_id }}
        step: Tests
        type: deploy
        status: Build:PASS;Test:PASS
        issue_id: '1234'
        actor: ${{ github.actor }}
        repository: ${{ github.repository }}
        workflow: 'my-next-workflow.yml'
        verbose: '0'
```

### GitLab CI

Not Implemented Yet

### Bitbucket Pipeline

Not Implemented Yet
