# N8N Facebook Automation Workflows

Bộ sưu tập các workflow n8n tự động hóa Facebook.

## Cấu Trúc

```
N8N_Facebook/
├── README.md
├── Facebook - Main Flow Webhook.json
├── Facebook - Messenger - Luồng đầy đủ webhook gọi vào - Page Test.json
├── Facebook - Messenger - SubFlow - Người Thật & AI - Page Test.json
├── Facebook - Comment - SubFlow - Page Test.json
├── Facebook - Post -  Lấy thông tin bài viết - Page Test.json
├── Facebook - Post  - Tự Động Lưu Bài Viết - Page Test.json
├── Facebook - Post - Reaction - SubFlow - Page Test.json
├── Facebook - Lấy link hình ảnh.json
├── Facebook - Tự Động Lấy PageAccessToken - Page Test.json
└── Facebook - LarkSuite - Cập Nhật Bảng Sau Khi Nhân Viên Đã Trả Lời Xong Với Khách Hàng.json
```

## Danh Sách Workflows

### 1. Main Flow Webhook 
**File:** `Facebook - Main Flow Webhook.json`

Webhook chính xử lý sự kiện từ Facebook Page. Phân loại:
- `added` - Lưu bài viết mới
- `messenger` - Tin nhắn messenger
- `comment` - Comment trên bài viết

### 2. Messenger - Luồng đầy đủ webhook gọi vào - Page Test
**File:** `Facebook - Messenger - Luồng đầy đủ webhook gọi vào - Page Test.json`

Luồng hoàn chỉnh xử lý tin nhắn Messenger:
- Nhận webhook từ Facebook
- Lưu vào Supabase database (`messenger_api`)
- Xử lý tự động với AI

### 3. Messenger - SubFlow - Người Thật & AI - Page Test
**File:** `Facebook - Messenger - SubFlow - Người Thật & AI - Page Test.json`

SubFlow xử lý hội thoại giữa người thật và AI:
- Quản lý conversation với Redis
- Memory PostgreSQL cho LangChain
- Phân loại tin nhắn (người thật / bot)

### 4. Comment - SubFlow - Page Test
**File:** `Facebook - Comment - SubFlow - Page Test.json`

SubFlow xử lý comment trên bài viết:
- Nhận comment từ webhook
- Gọi AI để tạo phản hồi
- Reply comment qua Facebook Graph API


### 5. Post - Lấy thông tin bài viết - Page Test
**File:** `Facebook - Post -  Lấy thông tin bài viết - Page Test.json`

Lấy thông tin bài viết từ Facebook Page:
- Sử dụng Facebook Graph API
- Fields: `id, message, created_time, permalink_url`


### 6. Post - Tự Động Lưu Bài Viết - Page Test
**File:** `Facebook - Post  - Tự Động Lưu Bài Viết - Page Test.json`

Tự động lưu bài viết vào Supabase Vector Store:
- Lưu vào bảng `documents`
- Hỗ trợ semantic search với embedding


### 7. Post - Reaction - SubFlow - Page Test
**File:** `Facebook - Post - Reaction - SubFlow - Page Test.json`

SubFlow xử lý reaction/post engagement:
- Gửi tin nhắn tự động khi có tương tác
- Redirect sang group Zalo: https://zalo.me/g/ujerqq444


### 8. Lấy link hình ảnh
**File:** `Facebook - Lấy link hình ảnh.json`

Trích xuất URL hình ảnh từ bài viết Facebook.

### 9. Tự Động Lấy PageAccessToken - Page Test
**File:** `Facebook - Tự Động Lấy PageAccessToken - Page Test.json`

Tự động lấy và cập nhật Page Access Token:
- Gọi `me/accounts` API
- Tạo credential mới cho Facebook Graph API

### 10. LarkSuite - Cập Nhật Bảng Sau Khi Nhân Viên Đã Trả Lời Xong Với Khách Hàng
**File:** `Facebook - LarkSuite - Cập Nhật Bảng Sau Khi Nhân Viên Đã Trả Lời Xong Với Khách Hàng.json`

Cập nhật trạng thái trong Supabase sau khi nhân viên trả lời:
- Filter: `status = "Pending"`
- Update: `status = "Done"`

## Công Nghệ Sử Dụng

- **N8N** - Workflow automation platform
- **Facebook Graph API** - Kết nối Facebook Page
- **Supabase** - Database & Vector Store
- **Redis** - Message aggregation
- **LangChain** - AI/LLM integration (PostgreSQL memory)
- **LarkSuite** - Cập nhật bảng khi hoàn thành

## Cách Import Workflow

1. Mở N8N dashboard
2. Click **Import from File**
3. Chọn file `.json` cần import
4. Cấu hình Credentials:
   - `facebookGraphApi` - Facebook credentials
   - `supabaseApi` - Supabase connection
5. Activate workflow

## Cấu Hình Credentials

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
