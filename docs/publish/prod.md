# How to install your tool in production?

Your code is ready for deployment. Well done bucko! Now what do I do?

The steps below may vary according to your tool. The gist of installing your tool to production will be along following lines:

(all scripts are in `/proj/production/servers/resources`)

- Create a PR
- Get the PR reviewed and approved ... but don't merge yet
    - Get someone to review your code
      - Is the code adhering to the language standards?
      - Where is the unit test?
      - Did any signatures of existing functions or methods change?
      - Check [the code review guide](code-review.md) to see that you didn't miss anything.
- Test the PR on stage by deploying your branch
    - Do this with your reviewer
    - Announce on TTNs daily standup
    - Delete current stage
    - Clone prod to stage: `condacopy-prod-to-stage.sh`
    - Switch to stage: `usestage`
    - Install branch into stage with the tool's update script: `update-tool-stage.sh`
- If it passes, merge the PR into master
    - Add a small risk assessment to the merge message describing the potential impact on existing functionality
    - Remove or rewrite any nonsense in the merge message into descriptive text
- Delete the branch
- Delete the development branch in conda
- Bumpversion on master
- Test the installation of the new master on stage
    - But only test that the installation succeeds
- If it passes, deploy on prod!
    - Announce on stand up
    - Take backup of prod: e.g. `savetheconda prod170926`
    - Install with the tool's update script: `update-tool-prod.sh`
