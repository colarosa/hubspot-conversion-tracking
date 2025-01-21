# 📋 HubSpot Form Submission Tracking Script

This script enables seamless tracking of HubSpot form submissions using the `dataLayer`. It listens for HubSpot form submission events and pushes relevant data to the `dataLayer`, making it compatible with analytics platforms such as Google Tag Manager.

## ✨ Features
- 🛠️ **Event Listener**: Listens for HubSpot form submission events.
- 🗂️ **Key Data Captured**:
  - **Form ID**: Unique identifier for the form.
  - **Conversion ID**: Conversion tracking ID (if applicable).
  - **Form GUID**: Globally unique identifier for the form.
  - **Submission Inputs**: Data submitted through the form.
- 📊 **Analytics-Ready**: Pushes the data into the `dataLayer` for tracking and integration.

## 🚀 Installation

1. Copy and paste the script below into the `<head>` or `<body>` section of your website where the HubSpot forms are used:
   ```html
   <script>
       // Listen for messages sent to the window object
       window.addEventListener("message", function(event) {
           // Check if the event data matches the desired HubSpot form submission callback
           if (!(event.data.type === 'hsFormCallback' && event.data.eventName === 'onFormSubmitted')) return;

           // Initialize the dataLayer array if it doesn't already exist
           window.dataLayer = window.dataLayer || [];

           // Push the HubSpot form submission data into the dataLayer for analytics tracking
           dataLayer.push({
               event: 'hubspot_form_submit', // Custom event name for form submission
               formId: event.data.id, // The unique ID of the form
               conversionId: event.data.data.conversionId, // Conversion ID (if applicable)
               formGuid: event.data.data.formGuid, // GUID associated with the form
               inputs: event.data.data.submissionValues // Form submission inputs
           });
       });
   </script>
