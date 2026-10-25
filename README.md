# Automated Network Request Management in ServiceNow

## About the Project

This project automates the process of managing network requests using ServiceNow. It was developed to simplify request submission, approval processing, task creation, and email communication.

Users can submit a network request through the Service Catalog. The request details are processed using Flow Designer, which creates the required records and manages the approval process. A separate flow handles the resolved email notification when the network task meets the configured closure conditions.

## Features

- **Network Request Form:** Collects request details such as connection type, mobile number, address, and other required information.
- **Automatic Record Creation:** Creates records in the custom Database Tables and Network Task Table.
- **Approval Management:** Processes approved and rejected requests using Flow Designer.
- **Task Tracking:** Maintains approval status, work status, and task state.
- **Email Notifications:** Sends request-related, approval, and rejection emails through configured flow actions.
- **Closure Notification:** Sends a resolved email when the network task meets the required closure conditions.
- **Configuration Backup:** Includes an exported ServiceNow Update Set for the captured flows.

## Technologies Used

- ServiceNow Platform
- Service Catalog
- Flow Designer
- Custom Tables
- Ask For Approval action
- Send Email action
- Update Sets
- GitHub

## How It Works

1. The user submits a request through the Network Request catalog item.
2. Flow Designer retrieves the submitted catalog variables.
3. A record is created in the Database Tables table.
4. A corresponding record is created in the Network Task Table.
5. The request proceeds through the configured approval process.
6. The database record and network task are updated based on the approval outcome.
7. The appropriate request, approval, or rejection email is sent through the configured actions.
8. When a network task reaches the required closure status, the separate Network Task Closure flow processes the resolved email notification.

## Network Task Closure Conditions

The closure flow uses a Record Updated trigger on the Network Task Table.

The resolved email is configured to run when all three conditions are met:

| Field | Value |
|---|---|
| Approval Status | Approved |
| Work Status | Completed |
| State | Closed Complete |

The email recipient is mapped to the Requester Email field on the network task record.

## Project Structure

```text
servicenow-network-request-automation/
├── README.md
├── update-set/
│   └── ServiceNow Update Set XML
└── screenshots/
    ├── Network Request Flow
    ├── Approval Configuration
    ├── Database Record Creation
    ├── Network Task Creation
    ├── Network Task Closure Flow
    ├── Email Configuration
    ├── Request Form
    └── Record and Execution Evidence
```

The screenshot names shown above describe the intended contents. The actual filenames may differ in the repository.

## Setup and Configuration

The project was configured in a ServiceNow Personal Developer Instance (PDI).

To recreate the workflow in another instance:

1. Configure the required custom tables and fields.
2. Create the Network Request catalog item and its variables.
3. Configure the `Network Request` flow with a Service Catalog trigger.
4. Add the record creation, approval, conditional update, and email actions.
5. Configure the `Network Task Closure` flow with a Record Updated trigger.
6. Set the closure conditions and configure the email recipient.
7. Test request submission, approval processing, task closure, and notifications.

### Update Set

The repository includes an exported Update Set XML containing the captured `Network Request` and `Network Task Closure` flow records.

The export has not been verified as a complete backup of the custom tables, fields, catalog item, and all related configuration. These components may need to be exported separately before the entire project can be recreated in another instance.

## Testing

The following checks can be used to verify the workflow:

- Submit a new network request.
- Check whether the database and network task records are created automatically.
- Verify the relationship between the two records.
- Test the approved and rejected paths.
- Check the initial and updated task statuses.
- Verify that email actions have valid recipients.
- Close a task using the required status values.
- Check the flow execution and email logs for the resolved notification.

## Future Improvements

- Add a dashboard to monitor network requests and task status.
- Introduce reminders for pending approvals.
- Improve error handling for incomplete request details.
- Add reports for request processing and completion times.
- Expand testing for different approval and closure scenarios.
