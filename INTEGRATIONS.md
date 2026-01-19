# Integrations Guide

Connect your StellarAdvisor forms to capture and manage leads.

---

## Option 1: Airtable (Recommended)

### Setup Steps

1. **Create Airtable Base**
   - Go to [airtable.com](https://airtable.com)
   - Create new base: "StellarAdvisor Leads"
   - Add table with fields:
     - Name (Single line text)
     - Email (Email)
     - Company (Single line text)
     - Revenue Range (Single select)
     - Challenge (Single select)
     - Source (Single select: Hero Form, Quiz, Modal)
     - Created (Created time)
     - Status (Single select: New, Contacted, Qualified, Intro Made)

2. **Get API Key**
   - Go to [airtable.com/create/tokens](https://airtable.com/create/tokens)
   - Create new token with:
     - Scope: `data.records:write`
     - Access: Your base

3. **Update Form Submission**

Replace the `submitLeadForm` function in `index.html`:

```javascript
async function submitLeadForm(e) {
  e.preventDefault();
  
  const formData = {
    fields: {
      Name: document.getElementById('name').value,
      Email: document.getElementById('email').value,
      Company: document.getElementById('company').value,
      'Revenue Range': document.getElementById('revenue').value,
      Challenge: document.getElementById('challenge').value,
      Source: 'Hero Form'
    }
  };
  
  try {
    await fetch('https://api.airtable.com/v0/YOUR_BASE_ID/Leads', {
      method: 'POST',
      headers: {
        'Authorization': 'Bearer YOUR_API_KEY',
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(formData)
    });
    
    document.getElementById('leadForm').style.display = 'none';
    document.getElementById('formSuccess').classList.add('active');
  } catch (error) {
    alert('Something went wrong. Please try again.');
  }
}
```

⚠️ **Security Note:** For production, use a serverless function (Vercel/Netlify) to hide your API key.

---

## Option 2: Tally.so (No-Code)

### Setup Steps

1. **Create Tally Form**
   - Go to [tally.so](https://tally.so)
   - Create form matching your fields
   - Get the embed code

2. **Replace Form HTML**

```html
<div class="hero-form-card" id="hero-form">
  <iframe 
    src="https://tally.so/embed/YOUR_FORM_ID?hideTitle=1" 
    width="100%" 
    height="500" 
    frameborder="0"
    style="border: none;">
  </iframe>
</div>
```

3. **Connect to Airtable**
   - In Tally: Settings → Integrations → Airtable
   - Connect and map fields

---

## Option 3: Zapier Automation

### Workflow: Form → Airtable → Email Notification

1. **Trigger:** Webhook (form submission)
2. **Action 1:** Create Airtable record
3. **Action 2:** Send email notification
4. **Action 3:** Send Slack message (optional)

### Form Code with Zapier Webhook

```javascript
async function submitLeadForm(e) {
  e.preventDefault();
  
  const data = {
    name: document.getElementById('name').value,
    email: document.getElementById('email').value,
    company: document.getElementById('company').value,
    revenue: document.getElementById('revenue').value,
    challenge: document.getElementById('challenge').value,
    timestamp: new Date().toISOString()
  };
  
  await fetch('https://hooks.zapier.com/hooks/catch/YOUR_HOOK_ID', {
    method: 'POST',
    body: JSON.stringify(data)
  });
  
  document.getElementById('leadForm').style.display = 'none';
  document.getElementById('formSuccess').classList.add('active');
}
```

---

## Calendly Integration

### Add Booking Button

```html
<a href="https://calendly.com/YOUR_USERNAME/strategy-call" 
   target="_blank" 
   class="nav-cta">
  Book Strategy Call
</a>
```

### Embed Calendar

```html
<!-- Add after form success message -->
<div class="calendly-inline-widget" 
     data-url="https://calendly.com/YOUR_USERNAME/strategy-call" 
     style="min-width:320px;height:630px;">
</div>
<script src="https://assets.calendly.com/assets/external/widget.js"></script>
```

---

## Email Notifications

### Using Resend (Free tier)

1. Sign up at [resend.com](https://resend.com)
2. Create API key
3. Add serverless function:

```javascript
// api/notify.js (Vercel serverless function)
export default async function handler(req, res) {
  const { name, email, company } = req.body;
  
  await fetch('https://api.resend.com/emails', {
    method: 'POST',
    headers: {
      'Authorization': 'Bearer YOUR_RESEND_API_KEY',
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({
      from: 'StellarAdvisor <notifications@stellaradvisor.com>',
      to: 'ryan@youremail.com',
      subject: `New Lead: ${name} from ${company}`,
      html: `<p>New lead submitted:</p>
             <ul>
               <li>Name: ${name}</li>
               <li>Email: ${email}</li>
               <li>Company: ${company}</li>
             </ul>`
    })
  });
  
  res.json({ success: true });
}
```

---

## CRM Sync Options

### HubSpot

```javascript
// Using HubSpot Forms API
await fetch('https://api.hsforms.com/submissions/v3/integration/submit/PORTAL_ID/FORM_ID', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    fields: [
      { name: 'email', value: email },
      { name: 'firstname', value: name },
      { name: 'company', value: company }
    ]
  })
});
```

### Pipedrive

Use Zapier to connect form submissions to Pipedrive deals.

### Monday.com

Use Zapier or Monday's native form integration.

---

## Analytics Setup

### Google Analytics 4

Add before `</head>`:

```html
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

### Track Form Submissions

```javascript
// Add to form submission function
gtag('event', 'generate_lead', {
  currency: 'USD',
  value: 100 // estimated lead value
});
```

### Meta Pixel

```html
<script>
  !function(f,b,e,v,n,t,s)
  {if(f.fbq)return;n=f.fbq=function(){n.callMethod?
  n.callMethod.apply(n,arguments):n.queue.push(arguments)};
  if(!f._fbq)f._fbq=n;n.push=n;n.loaded=!0;n.version='2.0';
  n.queue=[];t=b.createElement(e);t.async=!0;
  t.src=v;s=b.getElementsByTagName(e)[0];
  s.parentNode.insertBefore(t,s)}(window, document,'script',
  'https://connect.facebook.net/en_US/fbevents.js');
  fbq('init', 'YOUR_PIXEL_ID');
  fbq('track', 'PageView');
</script>
```

Track lead:
```javascript
fbq('track', 'Lead');
```

---

## Testing Checklist

- [ ] Form submits successfully
- [ ] Data appears in Airtable/CRM
- [ ] Email notification received
- [ ] Success message displays
- [ ] Mobile form works
- [ ] Analytics tracking fires

---

## Support

Need help setting up integrations?
- Check [Zapier's Airtable docs](https://zapier.com/apps/airtable/integrations)
- Join [Airtable Community](https://community.airtable.com)
- Ask in [Vercel Discord](https://vercel.com/discord)
