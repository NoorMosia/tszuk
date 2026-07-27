---
inclusion: fileMatch
fileMatchPattern: '**/api/**'
---

# Contact Form API

Rules and patterns for the `/api/contact` endpoint.

## Endpoint Spec

- **Path:** `POST /api/contact`
- **Content-Type:** `application/json`

## Request Payload

```typescript
interface ContactPayload {
  name: string;        // Required, non-empty after trim
  email: string;       // Required, basic email format
  projectType: "brand-identity-web" | "artist-management" | "other"; // Optional
  message: string;     // Required, non-empty after trim
}
```

## Response Shapes

```typescript
// 200 — success
{ success: true }

// 400 — validation error
{ error: "Name, email, and message are required" }
{ error: "Please provide a valid email address" }

// 500 — server/Resend failure
{ error: "Failed to send message. Please try again later." }
{ error: "An unexpected error occurred" }
```

## Validation Rules

1. Trim all string fields before validation.
2. Check `name`, `email`, `message` are present and non-empty — return 400 if not.
3. Validate email with a basic regex (contains `@` and `.` after `@`) — return 400 if invalid.
4. `projectType` is optional; ignore if missing or invalid.

## Resend Integration

```typescript
import { Resend } from 'resend';

const resend = new Resend(import.meta.env.RESEND_API_KEY);

await resend.emails.send({
  from: 'tszuk <noreply@tszuk.com>',
  to: 'hello@tszuk.com',
  subject: `New inquiry from ${name}`,
  text: `Name: ${name}\nEmail: ${email}\nProject Type: ${projectType}\n\n${message}`,
});
```

## Error Handling

- Wrap the Resend call in try/catch.
- On Resend failure: log the error server-side, return 500 with a user-friendly message.
- Never expose internal error details or stack traces to the client.

## Security

- No authentication required (public form).
- Consider rate limiting at the Cloudflare level if spam becomes an issue.
- Sanitize all inputs before including in email body (trim whitespace, no HTML injection).
