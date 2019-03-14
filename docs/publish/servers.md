# Servers

All you need to know on how to set up our servers.

Servers configurations and resources can be found in the servers repo.

If you have changed  something in that repo and want to deploy it you proceed much like with any other tool: 
- Create a PR
- Get the PR reviewed and approved ... but don't merge yet
    - Get someone to review your code
      - Is the code adhering to the language standards?
      - Did any signatures of existing functions or methods change?
- Test the PR on stage by deploying your branch
    - Do this with your reviewer
    - Announce on TTNs daily standup
    - Install branch into stage with the tool's update script: `update-servers-stage.sh`
- If it passes, merge the PR into master
    - Remove or rewrite any nonsense in the merge message into descriptive text
- Delete the branch
- Deploy on prod!
    - Announce on stand up
    - Install with the tool's update script: `update-servers-prod.sh`

Please note that some servers has no stage environment, then do for production what you would otherwise do for stage and then skip the rest.