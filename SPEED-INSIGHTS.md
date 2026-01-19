# Vercel Speed Insights Integration Guide

This document describes the Vercel Speed Insights integration for the StellarAdvisor Platform.

## What is Vercel Speed Insights?

Vercel Speed Insights is a performance monitoring tool that helps you understand and optimize your website's Core Web Vitals and other performance metrics. It provides real-world usage data from actual visitors to your site.

## Implementation

### HTML Integration (Static Site)

Since StellarAdvisor is a static HTML site, we've integrated Speed Insights using the HTML script approach:

1. **Speed Insights initialization script** - Added to `index.html` before closing `</body>`:
```html
<script>
  window.si = window.si || function () { (window.siq = window.siq || []).push(arguments); };
</script>
<script defer src="/_vercel/speed-insights/script.js"></script>
```

This script:
- Initializes the Speed Insights queue
- Loads the Speed Insights tracking script asynchronously
- Collects performance data automatically

### Configuration Files

**package.json** - Project metadata and scripts
- Tracks project dependencies and build information
- Enables integration with Vercel deployment

**vercel.json** - Vercel deployment configuration
- Configures static site serving
- Sets up security headers
- Ensures proper file routing

**.gitignore** - Git ignore rules
- Prevents tracking of build artifacts and dependencies
- Keeps repository clean

## Enabling Speed Insights

To enable Speed Insights in your Vercel dashboard:

1. Go to [Vercel Dashboard](https://vercel.com/dashboard)
2. Select the StellarAdvisor project
3. Click the **Speed Insights** tab
4. Click **Enable** in the dialog

> **Note:** Enabling Speed Insights will add new routes (scoped at `/_vercel/speed-insights/*`) after your next deployment.

## Deployment

Deploy to Vercel using:

```bash
# Using Vercel CLI
vercel deploy

# Or connect your GitHub repository for automatic deployments
# Every push to main branch will trigger a deployment
```

## Viewing Your Data

Once deployed and users have visited your site:

1. Go to [Vercel Dashboard](https://vercel.com/dashboard)
2. Select the StellarAdvisor project
3. Click the **Speed Insights** tab
4. After a few days of user visits, you'll see performance metrics

## Metrics Tracked

Speed Insights automatically collects data on:

- **Largest Contentful Paint (LCP)** - How quickly the main content loads
- **First Input Delay (FID)** - Responsiveness to user interactions
- **Cumulative Layout Shift (CLS)** - Visual stability of the page
- **First Contentful Paint (FCP)** - Speed of first paint
- **Time to First Byte (TTFB)** - Server response time

## Privacy & Compliance

Vercel Speed Insights complies with privacy and data protection standards. For more information, see the [Privacy Policy](https://vercel.com/docs/speed-insights/privacy-policy).

## Next Steps

1. Deploy to Vercel
2. Enable Speed Insights in the dashboard
3. Wait for user data to accumulate (typically 1-3 days)
4. Analyze metrics and optimize performance
5. Refer to [Using Speed Insights](https://vercel.com/docs/speed-insights/using-speed-insights) for detailed guidance

## Troubleshooting

**Script not loading?**
- Ensure `/_vercel/speed-insights/script.js` is accessible (appears after deployment)
- Check browser console for any errors
- Verify Speed Insights is enabled in your Vercel dashboard

**No data showing up?**
- Wait 1-3 days for user data to accumulate
- Ensure real users are visiting your site
- Speed Insights only tracks real user interactions, not synthetic tests

## Additional Resources

- [Speed Insights Documentation](https://vercel.com/docs/speed-insights)
- [Speed Insights Package Documentation](https://vercel.com/docs/speed-insights/package)
- [Web Vitals Guide](https://vercel.com/docs/speed-insights/metrics)
- [Vercel Deployment Guide](https://vercel.com/docs/deployments/overview)
