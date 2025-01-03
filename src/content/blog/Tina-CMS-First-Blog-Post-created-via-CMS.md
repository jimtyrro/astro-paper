---
title: Tina CMS First Blog Post created via CMS
author: Dmitriy Salynin
slug: tina-cms-first-blog-post-created-via-cms
tags:
  - others
pubDatetime: 2024-10-27T18:30:00.000Z
description: >-
  A Blog Post created via Tina CMS and auto deployed from GitHub repository into
  Cloudflare Pages
---

## Table of Contents

When connected to your git repository, Pages allows you to control which environments and branches you would like to automatically deploy to. By default, Pages will trigger a deployment any time you commit to either your production or preview environment. However, with branch deployment controls, you can configure automatic deployments to suit your preference on a per project basis.

## Production branch control

Direct Upload

If your project is a [Direct Upload](https://developers.cloudflare.com/pages/get-started/direct-upload/) project, you will not have the option to configure production branch controls. To update your production branch, you will need to manually call the [Update Project](https://developers.cloudflare.com/api/operations/pages-project-update-project) endpoint in the API.

Terminal windowcurl --request PATCH \\"https\://api.cloudflare.com/client/v4/accounts/{account\_id}/pages/projects/{project\_name}" \\--header "Authorization: Bearer \<API\_TOKEN>" \\--header "Content-Type: application/json" \\--data "{\\"production\_branch\\": \\"main\\"}"

To configure deployment options, go to your Pages project > Settings > Builds & deployments > Configure Production deployments. Pages will default to setting your production environment to the branch you first push, but you can set your production to another branch if you choose.

You can also enable or disable automatic deployment behavior on the production branch by checking the Enable automatic production branch deployments box. You must save your settings in order for the new production branch controls to take effect.

## Preview branch control

When configuring automatic preview deployments, there are three options to choose from.

* All non-Production branches: By default, Pages will automatically deploy any and every commit to a preview branch.
* None: Turns off automatic builds for all preview branches.
* Custom branches: Customize the automatic deployments of certain preview branches.

### Custom preview branch control

By selecting Custom branches, you can specify branches you wish to include and exclude from automatic deployments in the provided configuration fields. The configuration fields can be filled in two ways:

* Static branch names: Enter the precise name of the branch you are looking to include or exclude (for example, staging or dev).
* Wildcard syntax: Use wildcards to match multiple branches. You can specify wildcards at the start or end of your rule. The order of execution for the configuration is (1) Excludes, (2) Includes, (3) Skip. Pages will process the exclude configuration first, then go to the include configuration. If a branch does not match either then it will be skipped.

Wildcard syntax

A wildcard (\*) is a character that is used within rules. It can be placed alone to match anything or placed at the start or end of a rule to allow for better control over branch configuration. A wildcard will match zero or more characters.For example, if you wanted to match all branches that started with fix/ then you would create the rule fix/\* to match strings like fix/1, fix/bugsor fix/.

Example 1:

If you want to enforce branch prefixes such as fix/, feat/, or chore/ with wildcard syntax, you can include and exclude certain branches with the following rules:

* Include Preview branches: fix/\*, feat/\*, chore/\*
* Exclude Preview branches: “

Here Pages will include any branches with the indicated prefixes and exclude everything else. In this example, the excluding option is left empty.

Example 2:

If you wanted to prevent [dependabot ↗](https://github.com/dependabot) from creating a deployment for each PR it creates, you can exclude those branches with the following:

* Include Preview branches: \*
* Exclude Preview branches: dependabot/\*

Here Pages will include all branches except any branch starting with dependabot. In this example, the excluding option means any dependabot/ branches will not be built.

Example 3:

If you only want to deploy release-prefixed branches, then you could use the following rules:

* Include Preview branches: release/\*
* Exclude Preview branches: \*

This will deploy only branches starting with release/.
