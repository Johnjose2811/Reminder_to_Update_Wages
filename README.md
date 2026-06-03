# Reminder to Update Wages

This repository contains Power Automate cloud flows developed for companies to automate business processes and improve operational efficiency. The flows are designed to be reusable, well-documented, and easy to deploy across different environments.

## Overview

This collection of Power Automate flows helps organizations streamline their wage management and compliance processes. The primary flow included is the **Minimum Wage Report Notification Flow**, which automates minimum wage change monitoring and notification.

## Contents

### Flows

- **[Minimum Wage Report Flow](./flows/min-wage-report/)** - Automated notification system for minimum wage changes

## Minimum Wage Report Notification Flow

### Description

This Power Automate flow monitors upcoming minimum wage changes and automatically sends reminder emails one week before the effective date. It ensures your organization stays compliant and updated with regulatory wage changes across different jurisdictions.

### Key Features

- ✅ **Automated Monitoring** - Scheduled daily checks for upcoming wage changes
- ✅ **Advance Notifications** - Sends reminders exactly 7 days before effective date
- ✅ **Multi-Jurisdiction Support** - Handles wage changes across multiple jurisdictions
- ✅ **Easy Configuration** - Clear setup instructions and flexible parameters
- ✅ **Error Handling** - Built-in troubleshooting and monitoring capabilities

### How It Works

#### Trigger
- **Type**: Scheduled Recurrence
- **Frequency**: Daily
- **Time**: 10:00 AM India Standard Time (IST)

#### Process Flow

1. **Read Data from Excel** - Retrieves minimum wage data from a SharePoint-hosted Excel file
2. **Filter Upcoming Changes** - Identifies wage changes scheduled for exactly 7 days from today
3. **Send Notification Emails** - Sends high-priority reminder emails to designated recipients

### Date Conversion Logic

Excel stores dates as serial numbers (days since December 30, 1899). The flow converts these using:

```
formatDateTime(addDays('1899-12-30', int(float(item()?['Effective Date']))), 'yyyy-MM-dd')
```

## Requirements

### Licenses & Services
- Microsoft 365 License
- SharePoint Online
- Office 365 Outlook
- Power Automate

### Connectors Required
- **Excel Online (Business)** - For reading minimum wage data
- **Office 365 Outlook** - For sending notifications

### Excel File Structure

The Excel data source (`Min Wage Reporting.xlsx`) must contain a table with:

| Column | Description |
|--------|-------------|
| **Jurisdiction** | Name of the jurisdiction (state, country, etc.) |
| **Effective Date** | Date when minimum wage change takes effect (Excel date format) |
| **[Other columns]** | Additional wage change details as needed |

## Getting Started

### 1. Import the Flow

1. Download the flow package from this repository
2. Navigate to [Power Automate Portal](https://flow.microsoft.com)
3. Select **My flows** → **Import** → **Import Package (Legacy)**
4. Upload the flow package file

### 2. Configure Connections

During import, map the following connections:
- **Excel Online (Business)**: Select your Office 365 account
- **Office 365 Outlook**: Select your Office 365 account

### 3. Update Flow Parameters

After import, open the flow for editing:

#### Configure Excel Data Source
1. Edit the **List rows present in a table** action
2. Select your SharePoint site
3. Choose the document library containing the Excel file
4. Select `Min Wage Reporting.xlsx`
5. Choose the appropriate table

#### Configure Email Recipients
1. Edit the **Send an email (V2)** action
2. Set recipient email addresses in **To** and **Cc** fields
3. Customize the email body if needed (see template below)

#### Adjust Schedule (Optional)
1. Edit the **Recurrence** trigger
2. Modify time, frequency, or time zone as desired
3. Default: Daily at 10:00 AM IST

## Email Notification Template

### Subject
```
Reminder: Minimum wage rate change for [Jurisdiction] from [Effective Date]
```

### Body
```
Hello Team,

It's a gentle reminder: We are expecting minimum wage rate changes for [Jurisdiction] effective from [Effective Date].

Please update new rates in the system.

[Link to Source File]

Thanks & Regards,
[Your Name]
Data Analyst
Ashley Furniture India Pvt. Ltd.
```

## Testing

### Test the Flow

1. Add a test record to the Excel file with `Effective Date = Today + 7 days`
2. In Power Automate, open the flow and select **Test** → **Manually**
3. Verify that the email is sent correctly
4. Confirm that the date conversion works properly

### Verify Filter Logic

1. Add multiple test records with various dates
2. Ensure only records with `Effective Date = Today + 7 days` trigger emails
3. Validate that emails are sent with correct jurisdiction and date information

## Monitoring & Maintenance

### Check Flow Health

1. Open the flow in Power Automate portal
2. Review **Run History** for any failures
3. Monitor common issues:
   - Excel file moved or renamed
   - Permissions changed
   - Date format errors
   - Connection authentication expired

### Update the Excel File

- Keep the table structure consistent
- Use proper Excel date formatting for the **Effective Date** column
- Don't rename or move the file without updating the flow reference

## Troubleshooting

### Flow Not Triggering
- ✓ Verify the flow is enabled (toggle switch is on)
- ✓ Check that the recurrence schedule is correct
- ✓ Confirm the flow owner's Microsoft 365 license is active

### No Emails Sent
- ✓ Verify records exist with `Effective Date = Today + 7 days`
- ✓ Check filter logic in the flow
- ✓ Confirm email addresses are valid
- ✓ Review **Run History** for error messages

### Date Conversion Issues
- ✓ Ensure the **Effective Date** column uses Excel date format (not text)
- ✓ Verify the date serial number conversion formula
- ✓ Check time zone settings match your location

### Permission Errors
- ✓ Ensure the flow has access to the SharePoint site
- ✓ Verify Excel file permissions
- ✓ Confirm connections are properly authenticated

## Important Notes

- The flow uses Excel date serial numbers (days since December 30, 1899)
- Emails are sent exactly **7 days before** the effective date
- Notifications are marked with **High** importance
- Multiple emails will be sent if multiple jurisdictions have changes on the same date
- The flow requires the flow owner's license to remain active

## Version History

- **v1.0** (Current) - Initial release with daily scheduling and 7-day advance notification

## Support

For issues, questions, or to report bugs:
1. Check the **Troubleshooting** section above
2. Review Power Automate run history for detailed error messages
3. Contact your Power Automate administrator or IT support team
4. Open an issue in this repository

## License

This flow is provided as-is for organizational use. Ensure compliance with your organization's policies and Microsoft 365 licensing agreements.

## Contributing

To contribute improvements or report issues:
1. Create a new branch for your changes
2. Document any modifications thoroughly
3. Submit a pull request with a clear description of changes

## Related Documentation

- [Power Automate Documentation](https://learn.microsoft.com/power-automate/)
- [Excel Online Connector](https://learn.microsoft.com/connectors/excel/)
- [Office 365 Outlook Connector](https://learn.microsoft.com/connectors/office365/)
