# Discord Gen Z Mention Bot

Bot Discord chính thức dùng JavaScript, OpenRouter để nói chuyện kiểu Gen Z và chỉ trả lời khi được tag.

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
	Tạo API key tại [OpenRouter](https://openrouter.ai/keys), điền vào `OPENAI_API_KEY`, giữ `OPENAI_BASE_URL=https://openrouter.ai/api/v1` và dùng `OPENAI_MODEL=openrouter/free`.
	`openrouter/free` sẽ tự chọn một model miễn phí đang khả dụng. Nếu muốn tự chỉ định thứ tự fallback, dùng `OPENROUTER_MODELS=model-a:free,model-b:free,openrouter/free`.
	`ALLOW_PROFANITY=true` cho phép slang chửi nhẹ; đặt thành `false` để tắt.
	`REPLY_COOLDOWN_MS=8000` giới hạn thời gian giữa hai lần bot trả lời cùng một người, giúp tránh spam.
	`RANDOM_REACTION_CHANCE=0.12` là xác suất bot thả reaction vào tin nhắn thường; đặt `0` để tắt.
	`AUTO_REPLY_CHANCE=0.1` là xác suất 10% bot tự trả lời tin nhắn không được tag; đặt `0` để chỉ trả lời khi được tag.
	`AUTO_REPLY_COOLDOWN_MS=120000` giới hạn mỗi server chỉ có một lần bot tự trả lời trong 2 phút.
	`CHANNEL_HISTORY_LIMIT=12` là số tin nhắn gần đây bot đọc trong kênh để hiểu mạch trò chuyện.
6. Chạy bot:

```powershell
npm start
```

Khi tag bot trong server, bot sẽ gửi nội dung tới OpenRouter để tạo câu trả lời theo ngữ cảnh và style đã học. Nếu model gặp lỗi quota/rate limit, bot tự thử model tiếp theo trong danh sách. API key và token chỉ nằm trong `.env`, không commit lên Git.

## Điều khiển style

- Tag bot kèm `!style on` để bật học style.
- Tag bot kèm `!style off` để tắt học style.
- Tag bot kèm `!style forget` để xóa style đã lưu của server.
- Tag bot kèm `!reset` hoặc `!memory reset` để xóa toàn bộ bộ nhớ hội thoại và style của server. Người dùng cần quyền **Quản lý máy chủ**.

Bot giữ tối đa 16 lượt hội thoại gần nhất theo server, đọc thêm lịch sử gần đây của kênh khi trả lời, trả lời ngắn với cảm xúc phù hợp và đôi khi tự trả lời tin nhắn không được tag. Bot cần quyền `Read Message History`. Bot chỉ dùng emoji custom của server. Bot đôi khi tự thả reaction custom ngẫu nhiên; nếu server chưa có emoji custom thì sẽ không thả reaction. Cấp quyền `Use External Emojis` nếu muốn bot dùng emoji từ server khác. Bot chỉ dùng slang chung, không tạo slur, đe dọa hoặc nội dung công kích cá nhân.
