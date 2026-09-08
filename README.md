# Amplify Fusion GitHub-Slack Notification Agent

Amplify Fusion project based on this pair of NodeJS based agents: [Github Update A2A Agent](https://github.com/lbrenman/github-monitor-ai-agent-a2a-helloworld) and [Slack Notifier A2A Agent](https://github.com/lbrenman/slack-notifier-agent-ai-agent-a2a-helloworld)

Currently not implemented as true A2A but will revise as necessary. Implemented as a scheduled integration that checks Github branch create/delete events and commits for a list of repos for a given GitHub user.

Calls the [Amplify Fusion Slack Notifier A2A Agent](https://github.com/lbrenman/amplify-fusion-slack-notifier-agent) to send the Slack message. If this agent is not running, falls back to an implementation of the agents functionality implemented in Fusion as a Service.

To use:

* Get a Claude API Key [here](https://platform.claude.com/settings/workspaces/default/keys)
* Get a GitHub personal access token [here](https://github.com/settings/tokens)
* Create a slack webhook connector as described [here](https://api.slack.com/messaging/webhooks)
* Configure and Postgres database table using the following sql. This is required to store branch states per repo for determineing new and deleted branches. I use [Neon](https://neon.com/).
    ```sql
    CREATE TABLE repo_branch_state (
        github_user  VARCHAR(255)  NOT NULL,
        repo         VARCHAR(255)  NOT NULL,
        branches     JSONB         NOT NULL DEFAULT '[]',
        updated_at   TIMESTAMPTZ   NOT NULL DEFAULT NOW(),
        PRIMARY KEY (github_user, repo)
    );
    ```
* Import project export, GitHubNotifier_Agent.zip, in this repo, in Fusion Manager
* Go to the imported project in Fusion Design and update all connectors for your system
* In Manager -> Environment -> Properties add property GITHUB_NOTIFIER_AGENT_CONFIG and paste your agent properties as JSON (replace with your GItHub username and respos to watch):
    ```json
    {
        "github_username":"lbrenman",
        "github_repo_list": ["Sonos-Vibe-Coded-Loopstation"]
    }
    ```
* You may need to look that lastRunDt timestamp to see if it changed names on import. If so, then some small refactoring will be required. This will impact commit checks