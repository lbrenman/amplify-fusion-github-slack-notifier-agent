# Amplify Fusion GitHub-Slack Notification Agent

Amplify Fusion project based on this pair of NodeJS based agents: [Github Update A2A Agent](https://github.com/lbrenman/github-monitor-ai-agent-a2a-helloworld) and [Slack Notifier A2A Agent](slack-notifier-agent-ai-agent-a2a-helloworld)

Currently not implemented as true A2A but will revise as necessary. Implemented as a scheduled integration that checks Github branch create/delete events and commits for a list of repos for a given GitHub user.

Calls the [Slack Notifier A2A Agent](slack-notifier-agent-ai-agent-a2a-helloworld) to send the Slack message. If this agent is not running, falls back to an implementation of the agents functionality implemented in Fusion as a Service.