# 📧 Cold Email Assistant MCP Server

A Model Context Protocol (MCP) server that automates cold email outreach for job applications. Parse job postings, generate personalized emails using AI, and send or save them as drafts directly from Claude Desktop.

## ✨ Features

- **Job Posting Parser**: Extract company name, role, email, location, stipend, and requirements from WhatsApp messages
- **Resume & Prompt Loading**: Read resume and email templates from Word documents
- **Email Sending**: Send personalized emails with resume attachments via Gmail
- **Draft Saving**: Save emails to Gmail Drafts folder for review before sending
- **Resume Attachment**: Automatically attach your resume (PDF) to all emails

## 🚀 Quick Start

### Prerequisites

- Python 3.8+
- Gmail account with App Password enabled
- Claude Desktop app with MCP support
- Resume file (`resume.pdf`)
- Optional: `resume.docx` and `prompt.docx` for AI personalization

### Installation

```bash
# Clone the repository
git clone <repository-url>
cd cold-email-assistant

# Install dependencies
pip install fastmcp python-docx
```

### Gmail App Password Setup

1. Enable 2-Factor Authentication on your Google account
2. Go to [Google App Passwords](https://myaccount.google.com/apppasswords)
3. Generate a new app password for "Mail"
4. Use this password in the MCP server (not your regular Gmail password)

### Configure MCP Server

Add to your Claude Desktop config file:

**MacOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
**Windows**: `%APPDATA%/Claude/claude_desktop_config.json`

```json
{
  "mcpServers": {
    "cold-email": {
      "command": "python",
      "args": ["/path/to/your/cold_email_mcp.py"]
    }
  }
}
```

### Update Email Credentials

Edit the `cold_email_mcp.py` file and replace with your details:

```python
sender_email: str = 'your-email@gmail.com'
sender_password: str = 'your-app-password'
resume_path: str = "resume.pdf"
```

## 📖 How to Use

### 1. Parse Job Postings

Copy a job posting from WhatsApp and ask Claude:

```
Parse this job message:
[paste job posting text]
```

### 2. Load Your Resume

```
Load my resume from resume.docx
```

### 3. Generate Personalized Email

```
Using the job details and my resume, generate a personalized cold email
```

### 4. Save as Draft

```
Save this email as a draft to recruiter@company.com
```

### 5. Or Send Directly

```
Send this email to recruiter@company.com
```

## 🛠️ Available Tools

### `parse_job_message`
Extracts structured data from job postings:
- Company name
- Role/Position
- Email address
- Location
- Stipend/Salary
- Batch/Graduation year
- Requirements

### `load_resume`
Reads your resume from a `.docx` file for AI personalization

### `load_prompt`
Loads custom email templates from a `.docx` file

### `send_email_tool`
Sends email with resume attachment via Gmail SMTP

### `save_to_draft_tool`
Saves email to Gmail Drafts folder for review

## 📁 Project Structure

```
cold-email-assistant/
├── cold_email_mcp.py      # MCP server code
├── resume.pdf             # Your resume (PDF format)
├── resume.docx            # Resume for text extraction (optional)
├── prompt.docx            # Email template (optional)
└── README.md
```

## 💡 Usage Tips

- **Review Drafts**: Use `save_to_draft_tool` to review emails before sending
- **Customize Templates**: Store your email template in `prompt.docx` for consistency
- **Batch Processing**: Parse multiple job postings and save drafts for later review
- **AI Personalization**: Let Claude analyze job requirements and tailor your email
- **Privacy**: App passwords are safer than using your main Gmail password

## 🔒 Security

- Uses Gmail App Passwords (not your main password)
- App Password is hardcoded in the script (keep file secure)
- Consider using environment variables for production use
- Emails sent over TLS-encrypted connection

## 🔧 Troubleshooting

**"Error: Resume file not found"**
- Ensure `resume.pdf` is in the same directory as the script
- Check the `resume_path` parameter

**"Authentication failed"**
- Verify 2FA is enabled on your Google account
- Generate a new App Password
- Update `sender_password` in the script

**"Connection refused"**
- Check your internet connection
- Verify Gmail SMTP/IMAP is enabled
- Check firewall settings

**Draft not appearing in Gmail**
- Wait a few seconds and refresh
- Check "All Mail" folder
- Ensure IMAP is enabled in Gmail settings

## 🚧 Future Enhancements

- [ ] Environment variable support for credentials
- [ ] Support for multiple email providers
- [ ] Email template library
- [ ] Batch email sending with delays
- [ ] Email tracking and follow-up reminders
- [ ] Support for HTML email formatting

## 📝 Example Workflow

```
1. You: "Parse this job posting: [WhatsApp message]"
2. Claude: Extracts company, role, email, requirements

3. You: "Load my resume"
4. Claude: Reads resume.docx content

5. You: "Generate a personalized email for this role"
6. Claude: Creates tailored email based on job requirements

7. You: "Save as draft to recruiter@company.com"
8. Claude: Saves to Gmail Drafts with resume attached

9. Review draft in Gmail, make edits if needed, and send!
```

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!

---

**Made with ❤️ using FastMCP and Claude AI**