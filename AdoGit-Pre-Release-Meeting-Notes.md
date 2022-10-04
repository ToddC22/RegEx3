# Acrolinx for Azure DevOps Pre-Release Meeting
## Overall Status

- The development of the Azure DevOps is moving smoothly forward.
- No blockers are currently identified.
- We reached the point to test the webhook with realistic incoming
  events.

## Next Steps

- Acrolinx is waiting for the personal access tokens to the first
  Microsoft repositrories on Azure DevOps Git to proceed.

## Development Status

- The webhook receives and processes incoming events from Azure DevOps.
- All files in the pull requests are sent to the Acrolinx server and
  processed. This is triggered for each pull request creation and update.
- A content analysis dashboard is generated.
- A comment is written back to the pull request comment thread. It
  contains editable links to the files.
- The quality gate is working fine
- The global configuration file and repository list are on GitHub; The
  webhook checks for each pull request if the global configuration
  file has been changed and updates it if changed.

## Next Development Steps (non-exhaustive list)

- Waiting currently for the personal access tokens
- Update all tests and verify each configuration option
- Moving in stages toward production
- Baseline will be done after the pull requests are in production

## Open Security Relevant Tasks

All current tasks done.

## A4GH Upcoming Multi-Git Provider Approach

- The goal is to be able to support multiple git repository
  technologies with one single code base.

### Separate environments

IMPORTANT: although it will be possible to use the GitHub and ADO Git
services as if they were a single git service, it is of course
possible to set up separate environments:

- One purely for ADO Git
- One purely for GitHub

## Mixed Environments

- The global configuration files (including the repository list) will
  be on either GitHub or ADO Git

- The repository list will contain repositories from both git services
  (GitHub and ADO Git)

- It will be possible to run the same webhook for both GitHub and ADO Git

- Global remote configuration and the repository list
  (repositories.edn) can be managed from either GitHub or ADO Git.

## Current Location of The Global Configurations

We are currently using
<https://github.com/MicrosoftDocs/acrolinx-devrel-config/tree/master/global-config>
to manage all our instances hook setups.

## JSON-based Configurations

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

## Installation

To install the ADO Git integration please note following:

### Pre-requisite
   * The remote config directory must be on GitHub (for now)

* Generating the personal access token on Azure DevOps
   * Current minimal set of rights for the personal access token:
     * Code: read and status
     * Pull request threads: Read and write

### Configure The Service Hooks Subscriptions

**IMPORTANT:** You must create the following two types of subscription (for now)

1. Pull Request Updated (minimum required for testing)
2. Pull Request Created

Please follow the following selections for both types of subscriptions

   * HTTPS must be used to connect with the webhook
     * For MS-QA (Testing phase)
        ```https://ms-qa-adogit.acrolinx.cloud/githubhook/listen/```
     * For MS-Prod (Production)
        ```https://ms-adogit.acrolinx.cloud/githubhook/listen/```
   * **Basic authentication must be used**
   * The user name must be the word "**secret**" (without quotes)
   * The ADO secret must be entered as the password of this user
     * **Please work with Acrolinx to get the corresponding ADO GIT secret to complete this step** 
   * "Resource details to send" must be set to "**All**" (for now)
   * "Messages to send" shall be set to "**None**"
   * "Detailed messages to send" shall be set to "**None**"

* Configuration changes:
   * The GitHub secret config option is now :gh-secret (changed from :secret)
   * The Azure DevOps token config option name is :ado-token (this is the personal access token)
   * The ADO secret config option name is :ado-secret

## Updates (visible changes)

- 2021-12-03
  - The integration now supports Azure DevOps PR comments and status
    written back to the Ado Git system.
- 2022-01-07
  - DONE Finish the work on writing the comments back
  - DONE Implement writing the status back
  - DONE Store the shared secret in the basic authentication, in order
    to obfuscate the secret in the Azure DevOps user interface.
  - DONE The file links in the comment section should be editable (based
    on the same branch as the pull request)
  - DONE We need to protect our webhook development environment with TLS (it
    will be done before using any access to existing MS repositories).
  - DONE Implement the "refetch" of the incoming event information (incoming
    events can only be tested to have the proper secret set in the HTTP
    headers but are not signed like on GitHub).
2022-02-03
  - DONE Document ID is now a proper full URI
2022-03-01
  - DONE Remote config now reloads upon each pull request
