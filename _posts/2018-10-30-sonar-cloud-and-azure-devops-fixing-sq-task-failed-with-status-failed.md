---
ID: 5279
post_title: 'Sonar Cloud and Azure DevOps &#8211; Fixing [SQ] Task failed with status FAILED'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2018/10/30/sonar-cloud-and-azure-devops-fixing-sq-task-failed-with-status-failed/
published: true
post_date: 2018-10-30 13:25:33
---
A pull request build in Azure DevOps failed with the error: "[SQ] Task failed with status FAILED".

This was the only information given, when de build failed.

Luckily, the manual build gave more information:

Error: /home/vsts/work/1/s/gradlew failed with return code: 1

FAILURE: Build failed with an exception.

2018-10-30T10:51:56.3943110Z

2018-10-30T10:51:56.3943526Z * What went wrong:

2018-10-30T10:51:56.3960616Z Execution failed for task ':sonarqube'.

2018-10-30T10:51:56.3961713Z &gt; 'feature/10691-fix-side-menu-not-working<span style="color: red;">]</span>-when-NOT-admin' <span style="color: red;">is not a valid branch name. It can only contain 'A-Z', 'a-z', '0-9', '-', '_', '.', and '/')
</span>

The problem was in the branch name, it accidentally contained a "]" character.