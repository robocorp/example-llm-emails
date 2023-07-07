# OpenAI LLM email assistant

Learn how to use OpenAI's large language models to summarise, extract information and suggest replies with emails! We've made this for a specific use case described below, but with very little changes to the LLM prompts you can fit this to pretty much any email based context.

## USE CASE - Helping Accounts Receivables Payment Collectors

> Imagine working at a large enterprise company selling industrial goods accross the globe. Invoices your customers are supposed to pay are typically large, so the cash flow impact of a payment date is significant. The team sends out massive quantities of messages about approaching due dates and unpaid invoices, and need to read replies manually and update the information back to accounts receivables solution. 

Our automation helps the payment collectors by generating a summary and reply suggestions as well as a list of invoices that are being discussed, with a status based on customer's replies. The bot works in email threads: getting it's inputs as automatically forwarded emails to [Robocorp Control Room](https://cloud.robocorp.com/) (that trigger the bot execution automatically) and then replying back to the same thread. So essentially nothing needs to be installed on the end user machine to use the assistant.

This is how it looks in practise:

![Example reply email from the bot](/img/email-example.png)

## 👉 This is what the bot does

- Get an incoming email to trigger a bot (in Robocorp Control Room)
- Read email contents
- Call [OpenAI](https://openai.com/) `gpt-4` for summary, suggested reply and list of invoices along with their data
- Take OpenAI response and create an email body (HTML) out of it
- Use [SendGrid](https://sendgrid.com/) to send the email back to the user's email inbox

## Prerequisites

In order to run the bot as-is, you'll need the following in place.

- [Robocorp Control Room](https://cloud.robocorp.com/) and Vault connected to your VS Code.
- [Sendgrid](https://app.sendgrid.com/) account for sending emails. Free accounts were available at the time of writing this for limited usage.
- [OpenAI](https://platform.openai.com/) account with access to `gpt-4` model.
- Following Vault entries either exactly spelled as below, or edit the names in code to match your own:
    - Vault `OpenAI` containing entry `key` that has your OpenAI API key.
    - Vault `Sendgrid` containing two entries, `SENDGRID_API_KEY` that has your API key and `FROM_EMAIL` that has the "from" email address.

## Setting the Process up in Control Room

When configuring the process in to Control Room, remember to create an email trigger under `Schedule` step. Also remember to keep the Trigger Process and Parse email checkboxes checked.

![Process Email Trigger screenshot](/img/email-trigger.png)

## Running in VS Code

The example provides [one email as an example](/devdata/work-items-in/test-email/work-items.json). Use that as a template to create more of your own test work items! When you run the bot in VS Code, remember to choose the given input work item when prompted.