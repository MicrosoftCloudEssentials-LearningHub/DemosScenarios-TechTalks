# Azure DevOps - Overview 

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Extensions overview](https://learn.microsoft.com/en-us/azure/devops/extend/overview?view=azure-devops)
- [Extensions for Azure DevOps VS marketplace](https://marketplace.visualstudio.com/azuredevops/)
- [Azure DevOps About GitHub integration](https://learn.microsoft.com/en-us/azure/devops/cross-service/github-integration?view=azure-devops)
- [Planning and tracking work for your team or project](https://docs.github.com/en/issues/tracking-your-work-with-issues/configuring-issues/planning-and-tracking-work-for-your-team-or-project)
- [Best Practices for Managing Multiple Teams with GitHub Issues and Projects (V2)](https://github.com/orgs/community/discussions/137358)
- [FAQs about working across projects](https://learn.microsoft.com/en-us/azure/devops/project/work-across-projects-faqs?view=azure-devops)
- [Migrating repositories from Azure DevOps to GitHub Enterprise Cloud](https://docs.github.com/en/migrations/using-github-enterprise-importer/migrating-from-azure-devops-to-github-enterprise-cloud/m)
- [Azure DevOps Cross-Organization Reporting and Analysis using Power BI](https://devblogs.microsoft.com/premier-developer/azure-devops-cross-organization-reporting-and-analysis-using-power-bi/)
- [Customizing the board layout](https://docs.github.com/en/issues/planning-and-tracking-with-projects/customizing-views-in-your-project/customizing-the-board-layout)
- [Manage priorities and gain visibility across teams](https://learn.microsoft.com/en-us/azure/devops/boards/plans/visibility-across-teams?view=azure-devops)
- [About configuring and customizing Azure Boards](https://learn.microsoft.com/en-us/azure/devops/boards/configure-customize?view=azure-devops&tabs=agile-process)
- [Azure DevOps Migration overview](https://learn.microsoft.com/en-us/azure/devops/migrate/migration-overview?view=azure-devops)
  
</details>

<details>
<summary><b>Table of Contents</b> (Click to expand)</summary>

- [Overview](#overview)
- [Azure Boards](#azure-boards)
- [Azure Repos](#azure-repos)
- [Azure Pipelines](#azure-pipelines)
- [Azure Test Plans](#azure-test-plans)
- [Azure Artifacts](#azure-artifacts)
- [Setting Up a GitHub Board to Track Items Across Multiple Repositories](#setting-up-a-github-board-to-track-items-across-multiple-repositories)
- [Setting Up an Azure DevOps Board to Track Items Across Multiple Repositories](#setting-up-an-azure-devops-board-to-track-items-across-multiple-repositories)
</details>

## Overview

| **Azure DevOps Application** | **Purpose**                                      | **Features**                                                                 |
|------------------------------|--------------------------------------------------|------------------------------------------------------------------------------|
| **Azure Boards**             | Supports Agile project management and tracking   | Kanban boards, Scrum boards, work item tracking, backlogs, sprints, customizable workflows |
| **Azure Repos**              | Provides version control for code repositories   | Git repositories, Team Foundation Version Control (TFVC), pull requests, branch policies, code reviews |
| **Azure Pipelines**          | Facilitates continuous integration and delivery (CI/CD) | Build automation, release pipelines, deployment to various environments, integration with multiple tools and services, support for various programming languages and platforms |
| **Azure Test Plans**         | Manages testing processes and ensures software quality | Manual testing, automated testing, test case management, test execution, reporting |
| **Azure Artifacts**          | Manages and shares packages within the development team | Package feeds for Maven, npm, NuGet, and Python, versioning, dependency management, integration with CI/CD pipelines |

## Azure Boards

> Supports Agile project management and tracking.

<details>
  <summary>Features</summary>

  - **Kanban Boards**: Visualize work items and their flow through various stages. Teams can customize columns to reflect their workflow and easily move tasks across the board.
  - **Scrum Boards**: Manage sprints and backlogs, track progress, and plan iterations. Scrum boards help teams organize work into manageable chunks and deliver incremental value.
  - **Work Item Tracking**: Create and manage work items such as user stories, tasks, bugs, and features. Work items can be linked to code changes, builds, and releases.
  - **Backlogs**: Prioritize and manage the product backlog. Teams can break down features into user stories and tasks, estimate effort, and plan sprints.
  - **Sprints**: Plan and manage sprint cycles, track sprint progress, and review completed work. Teams can use sprint planning tools to allocate work and monitor velocity.
  - **Customizable Workflows**: Tailor workflows to match team processes. Customize states, transitions, and rules for work items to ensure they align with team practices.

</details>

## Azure Repos

> Provides version control for code repositories.

<details>
  <summary>Features</summary>

  - **Git Repositories**: Host and manage Git repositories. Teams can clone, commit, push, and pull code changes, and collaborate using branches and pull requests.
  - **Team Foundation Version Control (TFVC)**: An alternative to Git, TFVC is a centralized version control system. It allows teams to manage code with check-ins and branching.
  - **Pull Requests**: Facilitate code reviews and collaboration. Developers can create pull requests to propose code changes, review code, discuss modifications, and merge changes.
  - **Branch Policies**: Enforce best practices and quality standards. Teams can set policies for branch protection, requiring code reviews, and ensuring builds pass before merging.
  - **Code Reviews**: Conduct thorough code reviews to ensure code quality and adherence to standards. Reviewers can comment on code, suggest changes, and approve or reject pull requests.
</details>

## Azure Pipelines

> Facilitates continuous integration and continuous delivery (CI/CD).

<details>
  <summary>Features</summary>

  - **Build Automation**: Automate the building of code. Pipelines can compile code, run tests, and produce artifacts for deployment.
  - **Release Pipelines**: Automate the deployment process. Teams can define release pipelines to deploy applications to various environments, such as development, staging, and production.
  - **Deployment to Various Environments**: Deploy applications to multiple environments, including on-premises servers, cloud services, and containers. Pipelines support deployment to Azure, AWS, GCP, Kubernetes, and more.
  - **Integration with Multiple Tools and Services**: Integrate with a wide range of tools and services, such as GitHub, Docker, Jenkins, and Terraform. Pipelines can trigger builds and deployments based on code changes and other events.
  - **Support for Various Programming Languages and Platforms**: Build and deploy applications written in different languages, including .NET, Java, Node.js, Python, and PHP. Pipelines support Windows, Linux, and macOS platforms.

</details>

## Azure Test Plans

> Manages testing processes and ensures software quality.

<details>
  <summary>Features</summary>

  - **Manual Testing**: Create and execute manual test cases. Testers can document test steps, expected results, and actual outcomes.
  - **Automated Testing**: Integrate automated tests into CI/CD pipelines. Teams can run automated tests as part of the build and release process to ensure code quality.
  - **Test Case Management**: Organize and manage test cases, test suites, and test plans. Teams can track test coverage, prioritize tests, and manage test execution.
  - **Test Execution**: Execute tests and record results. Testers can run tests manually or automatically, capture test results, and log defects.
  - **Reporting**: Generate reports and dashboards to track test progress, test results, and quality metrics. Teams can use these insights to make informed decisions and improve software quality.

</details>

## Azure Artifacts

> Manages and shares packages within the development team.

<details>
  <summary>Features</summary>

  - **Package Feeds**: Create and manage package feeds for different package types, including Maven, npm, NuGet, and Python. Teams can publish, consume, and share packages.
  - **Versioning**: Manage package versions to ensure compatibility and stability. Teams can use versioning to track changes and maintain different versions of packages.
  - **Dependency Management**: Manage dependencies between packages. Teams can define dependencies, resolve conflicts, and ensure that applications use the correct versions of packages.
  - **Integration with CI/CD Pipelines**: Integrate package management with CI/CD pipelines. Teams can automate the publishing and consumption of packages as part of the build and release process.
</details>

## Setting Up an Azure DevOps Board to Track Items Across Multiple Repositories

1. **Create Work Item Queries**: Filter and view work items across multiple repositories.
    1. Navigate to Azure Boards and select `Queries`.
    2. Create a new query and define the criteria to include work items from multiple repositories.
    3. Save and run the query to view the filtered work items.
2. **Set Up Delivery Plans**: Gain visibility into deliverables scheduled across multiple teams and repositories.
    1. Navigate to Azure Boards and select `Delivery Plans`.
    2. Create a new delivery plan and select the teams and backlog levels of interest.
    3. Configure the plan to overlay backlogs onto your delivery schedule.
3. **Configure Dashboards**: Visualize work item status, progress, and trends across multiple repositories.
    1. Navigate to Azure Boards and select `Dashboards`.
    2. Create a new dashboard or edit an existing one.
    3. Add widgets to display data from multiple projects, such as burndown charts, query-based widgets, and embedded webpages.
4. **Use Portfolio Backlogs**: Track features and epics across multiple teams and repositories.
    1. Configure teams and backlogs to support the views you want.
    2. Add a management team for a group of feature teams and turn on the Epic portfolio backlog level.
    3. Add feature teams to manage features, stories, and tasks, and turn on the stories and features backlog levels.
    4. Break down epics into features and map them to the epics on the management backlog.
5. **Consistent Labeling Across Repositories**: Use consistent labels to categorize and filter work items.
    1. Create consistent labels across repositories (e.g., `epic`, `story`, `task`).
    2. Apply labels to work items and use filters in Azure Boards to view related items.
6. **Customizing Board Layouts**: Customize board layouts to fit your workflow and make it easier to track progress.
    1. Customize columns in your project board to reflect your workflow stages.
    2. Use fields such as status, priority, or team to organize work items within columns.
    3. Regularly update and maintain the board to ensure it reflects the current state of work.
7. **Automate Workflows with Azure Pipelines**: Automate repetitive tasks and ensure consistency across repositories.
    1. Set up Azure Pipelines to automate tasks such as labeling, assigning work items, and updating project boards.
    2. Use workflows to trigger actions based on events (e.g., work item creation, pull request merge).
8. **Regular Reviews and Updates**: Ensure the board remains up-to-date and accurately reflects the project’s status.
    1. Schedule regular reviews of the project board with the team.
    2. Update the status of work items, close completed tasks, and adjust priorities as needed.
    3. Use the board to facilitate team meetings and discussions.

## Setting Up a GitHub Board to Track Items Across Multiple Repositories

1. **Create an Overarching Repository for Epics** Use an overarching repository to house high-level issues (e.g., epics) that span multiple repositories.
    1. Create a new repository dedicated to tracking high-level issues.
    2. Create issues in this repository that represent epics or large stories.
    3. Link these high-level issues to detailed issues in other repositories using references (e.g., `#issue_number`).
2. **Use GitHub Projects for Cross-Repository Tracking**: GitHub Projects allows you to create boards that include issues and pull requests from multiple repositories.
    1. Go to the GitHub Projects section and create a new project.
    2. Add issues from multiple repositories to the project board.
    3. Use columns to organize the workflow (e.g., To Do, In Progress, Done).
3. **Leverage Milestones for Multi-Repo Coordination**: Milestones help group issues from multiple repositories under a common goal.
    1. Create a milestone in each repository that will be part of the epic.
    2. Assign relevant issues to these milestones.
    3. Use the milestone view to track progress across repositories.
4. **Consistent Labeling Across Repositories**: Use consistent labels to categorize and filter issues.
    1. Create consistent labels across repositories (e.g., `epic`, `story`, `task`).
    2. Apply labels to issues and use filters in GitHub Projects to view related issues.
5. **Customizing Board Layouts**: Customize board layouts to fit your workflow and make it easier to track progress.
    1. Customize columns in your project board to reflect your workflow stages.
    2. Use fields such as status, priority, or team to organize issues within columns.
    3. Regularly update and maintain the board to ensure it reflects the current state of work.
6. **Automate Workflows with GitHub Actions**: Automate repetitive tasks and ensure consistency across repositories.
    1. Set up GitHub Actions to automate tasks such as labeling, assigning issues, and updating project boards.
    2. Use workflows to trigger actions based on events (e.g., issue creation, pull request merge).
7. **Regular Reviews and Updates**: Ensure the board remains up-to-date and accurately reflects the project’s status.
    1. Schedule regular reviews of the project board with the team.
    2. Update the status of issues, close completed tasks, and adjust priorities as needed.
    3. Use the board to facilitate team meetings and discussions.

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1443-limegreen" alt="Total views">
  <p>Refresh Date: 2025-09-05</p>
</div>
<!-- END BADGE -->
