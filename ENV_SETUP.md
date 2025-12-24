# Environment Configuration Guide

## Email Verification Setup

This project now requires email OTP verification for user sign up. To enable email sending, you need to configure your email service in the `.env` file.

## Step 1: Create `.env` file

Create a file named `.env` in the `backend` directory with the following content:

```env
# Server Configuration
PORT=4000

# Email Configuration for OTP Verification
# Option 1: Gmail (Recommended for development)
MAIL_SERVICE=gmail
MAIL_USER=your-email@gmail.com
MAIL_PASS=your-app-password
MAIL_FROM=your-email@gmail.com

# Option 2: Custom SMTP (Alternative)
# MAIL_HOST=smtp.example.com
# MAIL_PORT=587
# MAIL_USER=your-email@example.com
# MAIL_PASS=your-password
# MAIL_FROM=your-email@example.com

# JWT Secret (for token generation)
JWT_SECRET=your-super-secret-jwt-key-change-this-in-production
```

## Step 2: Gmail Setup (Recommended)

### For Gmail users:

1. **Enable 2-Step Verification:**
   - Go to your Google Account: https://myaccount.google.com/security
   - Enable "2-Step Verification" if not already enabled

2. **Generate App Password:**
   - Go to: https://myaccount.google.com/apppasswords
   - Select "Mail" as the app
   - Select "Other (Custom name)" as the device
   - Enter "SmartCart" as the name
   - Click "Generate"
   - Copy the 16-character password (it will look like: `abcd efgh ijkl mnop`)

3. **Update `.env` file:**
   - Set `MAIL_SERVICE=gmail`
   - Set `MAIL_USER` to your Gmail address
   - Set `MAIL_PASS` to the 16-character app password (you can include or remove spaces)
   - Set `MAIL_FROM` to your Gmail address

## Step 3: Custom SMTP Setup (Alternative)

If you prefer to use a different email service:

1. Get your SMTP settings from your email provider
2. Update `.env` file with:
   - `MAIL_HOST` - SMTP server hostname
   - `MAIL_PORT` - SMTP port (usually 587 for TLS, 465 for SSL)
   - `MAIL_USER` - Your email address
   - `MAIL_PASS` - Your email password or app password
   - `MAIL_FROM` - Sender email address

## Step 4: Restart Backend

After configuring the `.env` file, restart your backend server:

```bash
cd backend
npm run dev
```

## Development Mode

If email is not configured, the OTP will still be generated and displayed in the backend console for development purposes. You can use this OTP to complete the verification process.

## Testing

1. Start the backend server
2. Go to the sign up page
3. Enter your email, name, and password
4. Click "Send Verification Code"
5. Check your email inbox (or backend console if email not configured)
6. Enter the 6-digit OTP
7. Click "Verify & Create Account"

## Troubleshooting

### OTP Not Arriving?
- Check spam/junk folder
- Verify app password is correct (for Gmail)
- Check backend console for error messages
- Ensure `MAIL_SERVICE=gmail` is set (for Gmail)
- OTP is valid for 10 minutes - request a new one if expired

### Email Send Errors?
- Verify all environment variables are set correctly
- For Gmail, ensure you're using an App Password (not your regular password)
- Check backend console for detailed error messages
- Ensure 2-Step Verification is enabled (for Gmail)

