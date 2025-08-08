## Overview

This document outlines the major bugs that were discovered and resolved in the
Scheduling App
---

## Critical Fixes Implemented

### 1. Multiple time calling of send-confirmation.

**File**: `src/components/LeadCaptureForm.tsx`
**Severity**: Critical
**Status**: Fixed

#### Problem

In the LeadCaptureForm.tsx the suspense edge function service named " send-confirmation " is called twice.

#### Root Cause

One time is was called for saving the data in the database. Second time it was called for sending the email.

#### Fix

Removed multiple calling of send-confirmation module.

```typescript

```

#### Impact

- ✅ Api will be called only single time after form submission.

---

### 1. Supabase CLI local setup

**File**: `package.json, supabase/config.toml,`
**Severity**: High
**Status**: Fixed

#### Problem

Not able to start the backend on local.

#### Root Cause

Supabase dev dependency was missing from the package.json file.
Previous Version setup of configuration

#### Fix

Added supabase in dev dependency and updated config.toml file according to latest version.

```json
"devDependencies": {
    "supabase": "^2.33.9",
}
```

```toml
[auth.sms.test_otp]
"1234567890" = "123456"

#Removed code

[auth]
email_double_confirm_changes = true


[auth.sms]
test_otp = "123456"

[edge_runtime]
enabled = true
ip_version = "ipv4"

[[edge_runtime.policies]]
entrypoint = "main"
source = """
import "jsr:@supabase/functions-js/edge-runtime.d.ts"

console.log("Hello from Functions!")
"""

```

#### Impact

- ✅ Any user will be able to setup supabase locally.

---

### 3. Absense of OPENAI_API_KEY backup

**File**: `supabase/functions/send-confirmation/index.ts`
**Severity**: High
**Status**: ✅ Critical

#### Problem

There are no backup message for the absence of OPENAI_API_KEY in the function named generatePersonalizedContent.

#### Root Cause

No Backup message setup f


#### Fix

Added backup text message and in return statementwith with OR condition if OPENAI_API_KEY is not present. Added error condition.

```ts
// Backend
if (!apiKey) {
    console.warn("OPEN API KEY is missing");
    return `Hi ${name}! 🚀 Welcome to our innovation community! We're thrilled to have someone from the ${industry} industry join us. Get ready to discover cutting-edge insights, connect with fellow innovators, and unlock new opportunities that will transform how you work. This is just the beginning of your innovation journey!`;
  }

if (data.error) {
    console.error("OpenAI API Error: ", data.error);
    throw new Error(data.error.message || "OpenAI request failed");
}
```

# Welcome to your Lovable project

## Project info

**URL**: https://lovable.dev/projects/94b52f1d-10a5-4e88-9a9c-5c12cf45d83a

## How can I edit this code?

There are several ways of editing your application.

**Use Lovable**

Simply visit the [Lovable Project](https://lovable.dev/projects/94b52f1d-10a5-4e88-9a9c-5c12cf45d83a) and start prompting.

Changes made via Lovable will be committed automatically to this repo.

**Use your preferred IDE**

If you want to work locally using your own IDE, you can clone this repo and push changes. Pushed changes will also be reflected in Lovable.

The only requirement is having Node.js & npm installed - [install with nvm](https://github.com/nvm-sh/nvm#installing-and-updating)

Follow these steps:

```sh
# Step 1: Clone the repository using the project's Git URL.
git clone <YOUR_GIT_URL>

# Step 2: Navigate to the project directory.
cd <YOUR_PROJECT_NAME>

# Step 3: Install the necessary dependencies.
npm i

# Step 4: Start the development server with auto-reloading and an instant preview.
npm run dev
```

**Edit a file directly in GitHub**

- Navigate to the desired file(s).
- Click the "Edit" button (pencil icon) at the top right of the file view.
- Make your changes and commit the changes.

**Use GitHub Codespaces**

- Navigate to the main page of your repository.
- Click on the "Code" button (green button) near the top right.
- Select the "Codespaces" tab.
- Click on "New codespace" to launch a new Codespace environment.
- Edit files directly within the Codespace and commit and push your changes once you're done.

## What technologies are used for this project?

This project is built with:

- Vite
- TypeScript
- React
- shadcn-ui
- Tailwind CSS

## How can I deploy this project?

Simply open [Lovable](https://lovable.dev/projects/94b52f1d-10a5-4e88-9a9c-5c12cf45d83a) and click on Share -> Publish.

## Can I connect a custom domain to my Lovable project?

Yes, you can!

To connect a domain, navigate to Project > Settings > Domains and click Connect Domain.

Read more here: [Setting up a custom domain](https://docs.lovable.dev/tips-tricks/custom-domain#step-by-step-guide)
