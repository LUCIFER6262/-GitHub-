
        attachment = open(attachment, 'rb')

        part = MIMEBase('application', 'octet-stream')
        part.set_payload(attachment.read())
        encoders.encode_base64(part)
        part.add_header('Content-Disposition', f'attachment; filename= {filename}')
        msg.attach(part)step 1 - pip install secure-smtplib



step 2 - import smtplib
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from email.mime.base import MIMEBase
from email import encoders
import datetime

 step 3 - def send_email(to_email, subject, body, attachment=None):
    from_email = 'your_email@example.com'  # Replace with your email address
    password = 'your_password'  # Replace with your email password

    # Create message container
    msg = MIMEMultipart()
    msg['From'] = from_email
    msg['To'] = to_email
    msg['Subject'] = subject

    # Attach body
    msg.attach(MIMEText(body, 'plain'))

    # Attach file if provided
    if attachment:
        filename = attachment

    # Send the email
    server = smtplib.SMTP('smtp.example.com', 587)  # Replace with your SMTP server and port
    server.starttls()
    server.login(from_email, password)
    text = msg.as_string()
    server.sendmail(from_email, to_email, text)
    server.quit()


step 4--- def generate_daily_report():
    # Example function to generate a daily report
    today = datetime.date.today().isoformat()
    report = f"Daily Report - {today}\n\n"
    report += "Insert your report content here."
    return report

 step 5---   if __name__ == '__main__':
    # Generate daily report
    report_body = generate_daily_report()

    # Define email details
    to_email = 'recipient@example.com'  # Replace with recipient's email address
    subject = 'Daily Report'
    attachment = 'path_to_attachment_file.pdf'  # Replace with path to attachment file if any

    # Send email
    send_email(to_email, subject, report_body, attachment)



step 6---- 0 6 * * * python3 /path/to/email_reports.py
