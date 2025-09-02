const TelegramBot = require('node-telegram-bot-api');

// توکن ربات - جایگزین کن!
const token = '8388704424:AAFwasSz4-QWwKDbuXyQ4mY54lS28-FjxeQ';

console.log('🔧 شروع تست ربات...');
console.log('🔑 توکن:', token.substring(0, 10) + '...');

// بررسی توکن
if (token === '8388704424:AAFwasSz4-QWwKDbuXyQ4mY54lS28-FjxeQ') {
    console.error('❌ خطا: توکن ربات را تنظیم نکرده‌اید!');
    console.log('💡 توکن را از @BotFather دریافت کرده و در کد قرار دهید');
    process.exit(1);
}

// ایجاد ربات
const bot = new TelegramBot(token, { polling: true });

console.log('🤖 ربات ایجاد شد، در حال اتصال...');

// تست اتصال
bot.getMe().then((info) => {
    console.log('✅ اتصال موفق!');
    console.log('🤖 نام ربات:', info.first_name);
    console.log('👤 یوزرنیم:', '@' + info.username);
    console.log('🆔 آیدی ربات:', info.id);
    console.log('📡 وضعیت: آنلاین و آماده دریافت پیام');
}).catch((error) => {
    console.error('❌ خطا در اتصال:', error.message);
    if (error.message.includes('401')) {
        console.log('💡 احتمالاً توکن اشتباه است');
    }
});

// پاسخ به /start
bot.onText(/\/start/, (msg) => {
    console.log('📨 دستور /start از کاربر:', msg.from.first_name);
    const chatId = msg.chat.id;
    bot.sendMessage(chatId, `سلام ${msg.from.first_name}! 👋\nمن کار می‌کنم! ✅`)
        .then(() => console.log('✅ پیام ارسال شد'))
        .catch((err) => console.error('❌ خطا در ارسال:', err));
});

// پاسخ به همه پیام‌ها
bot.on('message', (msg) => {
    const user = msg.from.first_name || msg.from.username || msg.from.id;
    const message = msg.text || '[فایل/عکس]';

    console.log(`📥 پیام جدید از ${user}: ${message}`);

    // اگه پیام دستور نبود
    if (msg.text && !msg.text.startsWith('/')) {
        const chatId = msg.chat.id;
        bot.sendMessage(chatId, `دریافت کردم: "${msg.text}" ✅`)
            .then(() => console.log('✅ پاسخ ارسال شد'))
            .catch((err) => console.error('❌ خطا در پاسخ:', err));
    }
});

// مدیریت خطاها
bot.on('error', (error) => {
    console.error('❌ خطای ربات:', error);
});

bot.on('polling_error', (error) => {
    console.error('❌ خطای polling:', error);

    if (error.code === 'EFATAL') {
        console.log('💡 ربات متوقف شد، در حال ری‌استارت...');
        setTimeout(() => {
            process.exit(1);
        }, 5000);
    }
});

console.log(`
🎯 مراحل تست:
1. توکن چک شد
2. اتصال برقرار شد  
3. در تلگرام ربات را پیدا کنید: @your_bot_username
4. /start را بفرستید
5. یک پیام عادی بفرستید

❓ اگر کار نکرد:
- توکن را دوباره چک کنید
- VPN روشن کنید (اگر فیلتر است)
- فایروال را بررسی کنید

🛑 برای توقف: Ctrl+C
`);