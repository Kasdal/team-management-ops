# Team Management Operations

![GitHub Actions workflow status](https://github.com/KasdalOrg/team-management-ops/actions/workflows/team-management.yml/badge.svg)

A streamlined Issue Ops system for automated team management and repository permission handling in GitHub organizations.

## 📋 Overview

The Team Management Operations (TMO) system allows administrators to manage GitHub teams, members, and repository permissions through a simple issue-based workflow. Instead of manually configuring teams through the GitHub UI or using complex scripts, TMO enables team creation and management via structured GitHub issues.

## 🌟 Features

- **Issue-based Team Management**: Create and configure teams by opening properly formatted issues
- **Automated Team Creation**: Automatically creates teams and sub-teams in your organization
- **Member Management**: Add members to teams with appropriate permissions
- **Repository Access Control**: Assign repository permissions to teams
- **Team Hierarchy**: Automatically organizes teams under a parent team structure
- **Activity Logging**: Maintains detailed JSON records of all team management activities

## 🚀 Getting Started

### Prerequisites

- GitHub organization with admin permissions
- GitHub App with appropriate permissions configured
  - Organization admin permissions
  - Repository permissions
  - Issue read/write permissions

### Setup

1. **Fork or clone this repository** to your organization

2. **Configure GitHub App**:
   - Create a GitHub App with the necessary permissions
   - Generate a private key
   - Install the app to your organization

3. **Set up secrets**:
   Add the following secrets to your repository:
   - `APP_ID`: Your GitHub App ID
   - `APP_PRIVATE_KEY`: Your GitHub App private key

4. **Enable GitHub Actions**:
   Make sure GitHub Actions are enabled for the repository

## 📝 Usage

### Creating a New Team

To create a new team, open an issue with the `team-management` label and use the following template:

```markdown
# Team Management Request

### Application ID
your-app-id

### Application Tier
Tier1

### Team Name
your-team-name

### Team Members
username1
username2

### Sub-Team Name (optional)
your-sub-team-name

### Sub-Team Members (optional)
username3
username4

### Team Permission Level
read | write | admin

### Repository Assets
org-name/repo-name
org-name/another-repo
```

### Team Structure

All teams created through this system are automatically added as children of the `all-projects` parent team. If you create sub-teams, they will be children of their respective main teams.

### Permission Levels

The system supports the following permission levels:
- `read`: Read-only access to repositories
- `write`: Read and write access to repositories
- `admin`: Administrative access to repositories

## 📊 How It Works

1. **Issue Creation**: Create an issue with the required template and `team-management` label
2. **Automated Processing**: GitHub Actions workflow parses the issue and extracts team information
3. **Team Creation**: Teams and sub-teams are created in your organization
4. **Parent Assignment**: Teams are placed under the `all-projects` parent team
5. **Member Addition**: Specified users are added to their respective teams
6. **Permission Setting**: Repository permissions are set according to specified level
7. **Data Storage**: Team data is saved as JSON in the `teamDB` directory
8. **Notification**: The issue is updated with a comment summarizing the actions taken

## 📁 Repository Structure

```
team-management-ops/
├── .github/
│   └── workflows/
│       └── team-management.yml    # Main workflow file
├── teamDB/                        # Team data storage directory
│   └── [application-id]_[timestamp].json  # Team data records
└── README.md                      # This documentation
```

## 🔍 Understanding Team Data Records

Each team management operation creates a JSON file in the `teamDB` directory with the following structure:

```json
{
  "application_id": "app-name",
  "application_tier": "Tier1",
  "team_name": "team-name",
  "team_members": ["username1", "username2"],
  "sub_team": "sub-team-name",
  "sub_team_members": ["username3", "username4"],
  "permission_level": "write",
  "repo_assets": ["org/repo1", "org/repo2"],
  "created_at": "2025-04-11T08:04:58Z",
  "issue_number": "13"
}
```

## 🛠️ Troubleshooting

### Common Issues

1. **Team Creation Fails**:
   - Ensure the GitHub App has sufficient organization permissions
   - Check that provided usernames exist and are accessible to the app

2. **Permission Setting Fails**:
   - Verify that repositories exist and are accessible to the app
   - Check that the permission level is valid (read, write, admin)

3. **Parent Team Relationship Fails**:
   - If you don't see the team hierarchy, ensure the `all-projects` team exists
   - Verify that the GitHub App has team admin permissions

### Viewing Logs

Check the GitHub Actions logs for detailed information about any issues:
1. Go to the Actions tab in the repository
2. Select the relevant workflow run
3. Expand the "Create and manage GitHub teams" step to see detailed logs

## 🔄 Contributing

Contributions to improve the Team Management Operations system are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgements

- GitHub for providing the API and GitHub Actions infrastructure
- The GitHub issue-parser library for simplifying issue parsing

---

## Security Considerations

- The GitHub App token used in this workflow has organization admin permissions. Ensure your repository is secure.
- Consider implementing additional validation for input in the issues to prevent potential misuse.
- Regularly audit the team changes made by this system.

## Maintenance

This repository is actively maintained. For questions, feature requests, or issues, please open an issue in the repository.