# N8N Facebook Automation Workflows

A collection of n8n workflows for Facebook Page automation.

## Structure

```
N8N_Facebook/
├── README.md
├── Facebook - Main Flow Webhook.json
├── Facebook - Messenger - Full Webhook Incoming Flow - Page Test.json
├── Facebook - Messenger - SubFlow - Human & AI - Page Test.json
├── Facebook - Comment - SubFlow - Page Test.json
├── Facebook - Post - Get Post Info - Page Test.json
├── Facebook - Post - Auto Save Posts - Page Test.json
├── Facebook - Post - Reaction - SubFlow - Page Test.json
├── Facebook - Extract Image Links.json
├── Facebook - Auto Get PageAccessToken - Page Test.json
└── Facebook - LarkSuite - Update Table After Agent Responded.json
```

## Workflows

### 1. Main Flow Webhook
**File:** `Facebook - Main Flow Webhook.json`

Main webhook handler for Facebook Page events. Classifies:
- `edited` - Post edited
- `added` - New post
- `messenger` - Messenger message
- `comment` - Comment on post

### 2. Messenger - Full Webhook Incoming Flow - Page Test
**File:** `Facebook - Messenger - Full Webhook Incoming Flow - Page Test.json`

Complete flow for processing Messenger messages:
- Receive webhook from Facebook
- Save to Supabase database (`messenger_api`)
- Process with AI automation

### 3. Messenger - SubFlow - Human & AI - Page Test
**File:** `Facebook - Messenger - SubFlow - Human & AI - Page Test.json`

SubFlow handling human/AI conversations:
- Conversation management with Redis
- PostgreSQL memory for LangChain
- Message classification (human / bot)

### 4. Comment - SubFlow - Page Test
**File:** `Facebook - Comment - SubFlow - Page Test.json`

SubFlow for processing post comments:
- Receive comment from webhook
- Call AI to generate response
- Reply to comment via Facebook Graph API

### 5. Post - Get Post Info - Page Test
**File:** `Facebook - Post - Get Post Info - Page Test.json`

Fetch post information from Facebook Page:
- Uses Facebook Graph API
- Fields: `id, message, created_time, permalink_url`

### 6. Post - Auto Save Posts - Page Test
**File:** `Facebook - Post - Auto Save Posts - Page Test.json`

Auto-save posts to Supabase Vector Store:
- Save to `documents` table
- Supports semantic search with embedding


### 7. Post - Reaction - SubFlow - Page Test
**File:** `Facebook - Post - Reaction - SubFlow - Page Test.json`

SubFlow for reaction/post engagement:
- Auto-send message on interaction
- Redirect to Zalo group: https://zalo.me/g/ujerqq444

### 8. Extract Image Links
**File:** `Facebook - Extract Image Links.json`

Extract image URLs from Facebook posts.

### 9. Auto Get PageAccessToken - Page Test
**File:** `Facebook - Auto Get PageAccessToken - Page Test.json`

Auto-fetch and update Page Access Token:
- Call `me/accounts` API
- Create new Facebook Graph API credential

### 10. LarkSuite - Update Table After Agent Responded
**File:** `Facebook - LarkSuite - Update Table After Agent Responded.json`

Update status in Supabase after agent responds:
- Filter: `status = "Pending"`
- Update: `status = "Done"`

## Tech Stack

- **N8N** - Workflow automation platform
- **Facebook Graph API** - Facebook Page integration
- **Supabase** - Database & Vector Store
- **Redis** - Message aggregation
- **LangChain** - AI/LLM integration (PostgreSQL memory)
- **LarkSuite** - Table update on completion

## How to Import Workflows

1. Open N8N dashboard
2. Click **Import from File**
3. Select the `.json` file to import
4. Configure Credentials:
   - `facebookGraphApi` - Facebook credentials
   - `supabaseApi` - Supabase connection
5. Activate workflow

## Credentials Configuration

### Facebook Graph API
```json
{
  "accessToken": "YOUR_PAGE_ACCESS_TOKEN"
}
```

### Supabase
```json
{
  "host": "YOUR_PROJECT.supabase.co",
  "port": 5432,
  "database": "postgres",
  "user": "postgres",
  "password": "YOUR_PASSWORD"
}
```

## License

Private project - All rights reserved © OTIMO
