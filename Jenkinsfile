job('upstreamJob') {
    scm {
        git {
            remote {
                github('test-owner/test-project')
                refspec('+refs/pull/*:refs/remotes/origin/pr/*')
            }
            branch('${sha1}')
        }
    }

    triggers {
        pullRequest {
            admin('user_1')
            admins(['user_2', 'user_3'])
            userWhitelist('you@you.com')
            userWhitelist(['me@me.com', 'they@they.com'])
            orgWhitelist('my_github_org')
            orgWhitelist(['your_github_org', 'another_org'])
            cron('H/5 * * * *')
            triggerPhrase('OK to test')
            onlyTriggerPhrase()
            useGitHubHooks()
            permitAll()
            autoCloseFailedPullRequests()
            displayBuildErrorsOnDownstreamBuilds()
            whiteListTargetBranches(['master','test', 'test2'])
            allowMembersOfWhitelistedOrgsAsAdmin()
            extensions {
                commitStatus {
                    context('deploy to staging site')
                    triggeredStatus('starting deployment to staging site...')
                    startedStatus('deploying to staging site...')
                    addTestResults(true)
                    statusUrl('http://mystatussite.com/prs')
                    completedStatus('SUCCESS', 'All is well')
                    completedStatus('FAILURE', 'Something went wrong. Investigate!')
                    completedStatus('PENDING', 'still in progress...')
                    completedStatus('ERROR', 'Something went really wrong. Investigate!')
                }
            }
        }
    }
    publishers {
        mergeGithubPullRequest {
            mergeComment('merged by Jenkins')
            onlyAdminsMerge()
            disallowOwnCode()
            failOnNonMerge()
            deleteOnMerge()
        }
    }
}

job('downstreamJob') {
    wrappers {
        downstreamCommitStatus {
            context('CONTEXT NAME')
            triggeredStatus("The job has triggered")
            startedStatus("The job has started")
            statusUrl()
            completedStatus('SUCCESS', "The job has passed")
            completedStatus('FAILURE', "The job has failed")
            completedStatus('ERROR', "The job has resulted in an error")
        }
    }
}
