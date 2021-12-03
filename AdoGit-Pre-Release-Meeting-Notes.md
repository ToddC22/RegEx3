# Acrolinx for Azure DevOps Pre-Release Meeting

Starting with the next updates, we'll also provide a diff for fast reading.

## Overall Status

- The development of the Azure DevOps is moving smoothly forward. No
  blockers are currently identified. We nearly reached the point to
  test the webhook with realistic incoming events.

## Next steps

- Dalton agreed on meeting us again on January 10.

- Samir and Hugo will provide updates every two weeks on Tuesday until
  we have our next meeting.

- Acrolinx (Samir) will get read access to a low confidentiality
  repository from Dalton/Dom. The repository will be set up to send
  Pull Request events to the development webhook EC2 instance.

- Joanna will work with KC to get early approval to install the
  webhook on their confidential repositories once we reach the status
  of an official release. The purpose is to identify any security
  concerns at an early stage.

## Development status

- The webhook can now receive incoming events from Azure DevOps
- Files in the last commit are sent to the Acrolinx server and processed
- A content analysis dashboard is generated
- A comment is written back to the pull request comment thread (primitive at the time of the demo)
- the global configuration file and repository list are on GitHub

## Next development steps (non-exhaustive list)

- Finish the work on writing the comments back
- Implement writing the status back
- Update all tests and verify each configuration option
- Moving in stages toward production
- Baseline will be done after the pull requests are in production

## Security relevant tasks

- We need to protect our webhook development environment with TLS (it
  will be done before using any access to existing MS repositories).

- Implement the "refetch" of the incoming event information (incoming
  events can only be tested to have the proper secret set in the HTTP
  headers but are not signed like on GitHub).

## Not covered yet in the demo

- Status (passive quality gate)
- Baseline operations

## A4GH will have a multigit provider approach

- The goal is to be able to support multiple git repository technologies with one single code base.

### Separate environments

IMPORTANT: although it will be possible to use the GitHub and ADO Git
services as if they were a single git service, it is of course
possible to set up separate environments:

- One purely for ADO Git
- One purely for GitHub

## Mixed environments

- The global configuration files (including the repository list) will
  be on either GitHub or ADO Git

- The repository list will contain repositories from both git services
  (GitHub and ADO Git)

- It will be possible to run the same webhook for both GitHub and ADO Git

- Global remote configuration and the repository list
  (repositories.edn) can be managed from either GitHub or ADO Git.

## Current location of the global configurations

We are currently using
<https://github.com/MicrosoftDocs/acrolinx-devrel-config/tree/master/global-config>
to manage all our instances hook setups.

## JSON-based configurations

We are currently working on moving all configuration files (global
config file, repository list and repo configurations) to the JSON
format. The resulting JSON will be very close to the current EDN
files.

The reason for that is that some production issues are related to
broken EDN configuration files (EDN is not supported natively on most
editors).

The JSON format is editable via the web editors of both GitHub and ADO
Git with syntax support (broken files are immediately identifiable).

We might later support also the JSONC format. This format is however
not supported natively on the web editor of ADO.

## Updates

- (12/03/2021) The integration now support Azure DevOps PR comments and status written back.
