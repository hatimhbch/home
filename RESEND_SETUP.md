# Resend API Setup Guide

This application has been configured to use [Resend](https://resend.com) for sending confirmation emails instead of SMTP.

## Setup Instructions

### 1. Get Your Resend API Key

1. Sign up for a free account at [resend.com](https://resend.com)
2. Navigate to the API Keys section in your dashboard
3. Create a new API key
4. Copy the API key (it starts with `re_`)

### 2. Configure the API Key

You can set your Resend API key in one of the following ways:

#### Option A: Environment Variable (Recommended)
Set the environment variable `RESEND_API_KEY`:

```bash
export RESEND_API_KEY=re_your_actual_api_key_here
```

#### Option B: Application Properties
Update the `application.yml` file:

```yaml
resend:
  api:
    key: re_your_actual_api_key_here
```

### 3. Configure Your Domain (Optional)

By default, emails are sent from `noreply@blogprototype.com`. To use your own domain:

1. Add and verify your domain in the Resend dashboard
2. Update the `from.email` configuration in `application.yml`:

```yaml
resend:
  from:
    email: noreply@yourdomain.com
```

### 4. Test the Configuration

Start your application and try registering a new user. Check the console logs for successful email sending messages.

## Benefits of Using Resend

- ✅ Better deliverability rates
- ✅ Simple API integration
- ✅ No SMTP configuration needed
- ✅ Built-in analytics and tracking
- ✅ Free tier includes 3,000 emails/month

## Migration Notes

The following changes were made to migrate from SMTP to Resend:

1. **Dependencies**: Removed `spring-boot-starter-mail`, kept `resend-java`
2. **Configuration**: Replaced SMTP settings with Resend API configuration
3. **EmailService**: Updated to use Resend API instead of JavaMailSender
4. **Email Templates**: No changes needed - Thymeleaf templates still work

## Troubleshooting

- **401 Unauthorized**: Check that your API key is correct
- **403 Forbidden**: Verify your domain is verified in Resend dashboard
- **404 Not Found**: Ensure you're using the correct API endpoint
- **Rate Limiting**: Check your Resend plan limits

For more information, visit the [Resend documentation](https://resend.com/docs). 