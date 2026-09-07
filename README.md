# Discord Gen Z Mention Bot

Bot Discord chính thức dùng JavaScript, OpenAI để nói chuyện kiểu Gen Z và chỉ trả lời khi được tag.

Bot ghi nhớ tối đa 80 mẫu tin nhắn ngắn theo từng server để lấy từ lóng/cách nói chung. Bot không lưu tên người dùng và không lặp nguyên văn mẫu tin nhắn.

## Cài đặt

1. Tạo application và bot tại Discord Developer Portal.
2. Bật **Message Content Intent** trong phần Bot > Privileged Gateway Intents.
3. Tạo invite trong OAuth2 URL Generator với scope `bot` và quyền `Send Messages`.
4. Cài dependency:

```powershell
npm install
```

5. Sao chép `.env.example` thành `.env`, rồi điền bot token. Không chia sẻ token này.
	`OPENAI_API_KEY` là API key OpenAI của bạn; `OPENAI_MODEL` mặc định là `gpt-4o-mini`.
	`ALLOW_PROFANITY=true` cho phép slang chửi nhẹ; đặt thành `false` để tắt.
	`REPLY_COOLDOWN_MS=8000` giới hạn thời gian giữa hai lần bot trả lời cùng một người, giúp tránh spam.
	`RANDOM_REACTION_CHANCE=0.12` là xác suất bot thả reaction vào tin nhắn thường; đặt `0` để tắt.
6. Chạy bot:

```powershell
npm start
```

Khi tag bot trong server, bot sẽ gửi nội dung tới OpenAI để tạo câu trả lời theo ngữ cảnh và style đã học. API key và token chỉ nằm trong `.env`, không commit lên Git.

## Điều khiển style

- Tag bot kèm `!style on` để bật học style.
- Tag bot kèm `!style off` để tắt học style.
- Tag bot kèm `!style forget` để xóa style đã lưu của server.
- Tag bot kèm `!reset` hoặc `!memory reset` để xóa toàn bộ bộ nhớ hội thoại và style của server. Người dùng cần quyền **Quản lý máy chủ**.

Bot giữ tối đa 16 lượt hội thoại gần nhất theo server, trả lời ngắn với cảm xúc phù hợp và đôi khi tự thả reaction ngẫu nhiên. Bot chỉ dùng slang chung, không tạo slur, đe dọa hoặc nội dung công kích cá nhân.
