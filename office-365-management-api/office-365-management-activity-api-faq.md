---
ms.TocTitle: Office 365 Management Activity API frequently asked questions
title: Office 365 Management Activity API frequently asked questions
description: Frequently asked questions about using the Office 365 Management Activity API
ms.ContentId:
ms.topic: reference (API)
ms.date: 
localization_priority: Priority
---

# Office 365 Management Activity API frequently asked questions

#### What events are audited for a specific Office 365 service?

Office 365 Management Activity API schema documentation has a comprehensive list of events. For details, see [Office 365 Management Activity API schema](office-365-management-activity-api-schema.md). Also see the "Audited activities" section in [Search the audit log in the Security & Compliance Center](https://docs.microsoft.com/en-us/office365/securitycompliance/search-the-audit-log-in-security-and-compliance#audited-activities) for a list of events for most of the Office 365 services that are audited.

#### How do I onboard to the Management Activity API?

To get started with the Office 365 Management Activity API, see [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md).
 
#### What is the throttling limit for the  Management Activity API?

The current throttling limit is 60K requests/minute per Publisher ID. 

#### We want to programmatically capture all events in all workloads. What is the most reliable way to do this?

You can do this by using the Office 365 Management Activity API. Also, we recommend that you use the **pull model** due to issues with using webhooks. For more information, see the "Using webhooks" section in [Troubleshooting the Office 365 Management Activity API](troubleshooting-the-office-365-management-activity-api.md#using-webhooks).

#### Is it true that mailbox auditing in Exchange Online can only be enabled by using PowerShell?

That used to be the case but since January 2019, mailbox auditing is now turned on by default for all Office 365 organizations. For more information, see [Manage mailbox auditing](https://docs.microsoft.com/office365/securitycompliance/enable-mailbox-auditing).

#### Are there any differences in the records that are fetched by the Management Activity API versus the records that are returned by using the audit log search tool in the Office 365 Security & Compliance Center?

The data that is returned by both methods is the same. There is no filtering that happens. The only difference is that with the API, you can get data for the last 7 days at a time. When searching the audit log in the Security & Compliance Center (or by using the corresponding [Search-UnifiedAuditLog](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance-audit/search-unifiedauditlog) cmdlet in Exchange Online), you can get data for the last 90 days. 

#### What happens if I disable auditing for my Office 365 organization? Will I still get events via the Management Activity API?

No. Office 365 unified auditing must be enabled for your organization to pull records via the Management Activity API. For instructions, see [Turn Office 365 audit log search on or off](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off).

#### Aren’t webhook notifications more immediate? After all, aren’t they event-driven?

No. Webhook notifications aren't event-driven in the sense that the event triggers the notification. The content blob must still be created, and the creation of the content blob is what triggers the notification delivery. Recently, there have been longer wait times for notifications when using a webhook compared to querying the API directly with the */content* operation. Therefore, the Management Activity API shouldn’t be thought of as a real-time security alert system. Microsoft has other products for that. As far as security is concerned, Management Activity API event notifications can more appropriately be used to determine usage patterns over extended periods of time.

#### When pulling the data from the Management Activity API, there is sometimes a delay of more than 3 to 5 days. Why is this?

At times, there are instances of a temporary outage or other issues in the Office 365 service. In those cases, some audit records are dropped and the service tries to backfill them. Although this happens for only about 5% to 10% of the records, these are the records that may be delayed in certain situations. If the delay is more than 5 days, check the Service Health Dashboard in the Office 365 admin center. If needed, you can also open a ticket with [Microsoft support](https://support.office.com/article/contact-support-for-business-products-admin-help-32a17ca7-6fa0-4870-8a8d-e25ba4ccfd4b#ID0EAADAAA=online).

#### I'm encountering a throttling error in the Management Activity API. What should I do?

Open a ticket with [Microsoft Support](https://support.office.com/article/contact-support-for-business-products-admin-help-32a17ca7-6fa0-4870-8a8d-e25ba4ccfd4b#ID0EAADAAA=online) and request a new throttling limit, and include a business justification for increasing the limit. We will evaluate the request, and if accepted, we will increase the throttling limit.

#### Why are TargetUpdatedProperties no longer in ExtendedProperties in the audit logs for Azure Active Directory activities?

TargetUpdatedProperties were appearing in ExtendedProperties. However, they have been removed from ExtendedProperties and now appear in ModifiedProperties.
