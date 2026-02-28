import telebot
import yt_dlp
import os

# ضع التوكن الذي حصلت عليه من BotFather هنا
API_TOKEN = '8642638664:AAHPp3Yfv8-r4rfPBsIbVL92kTIJjI_g9DM'
bot = telebot.TeleBot(API_TOKEN)

@bot.message_handler(commands=['start'])
def send_welcome(message):
    bot.reply_to(message, "أهلاً بك في بوت التحميل الخاص بي! 📥\nأرسل لي رابط فيديو من تيك توك أو إنستغرام وسأقوم بتحميله لك.")

@bot.message_handler(func=lambda message: True)
def download_video(message):
    url = message.text
    bot.send_message(message.chat.id, "جاري معالجة الرابط... انتظر قليلاً ⏳")

    # إعدادات التحميل وحفظ الحقوق
    ydl_opts = {
        'format': 'best',
        'outtmpl': 'video.mp4', # اسم الملف المؤقت
        'quiet': True,
    }

    try:
        with yt_dlp.YoutubeDL(ydl_opts) as ydl:
            ydl.download([url])
        
        # إرسال الفيديو مع "حقوقك" في الوصف (Caption)
        with open('video.mp4', 'rb') as video:
            bot.send_video(
                message.chat.id, 
                video, 
                caption="✅ تم التحميل بواسطة: [اسم بوتك أو معرفك]\nتابعنا للمزيد!"
            )
        
        # حذف الملف بعد الإرسال لتوفير المساحة
        os.remove('video.mp4')

    except Exception as e:
        bot.reply_to(message, "عذراً، حدث خطأ. تأكد من أن الرابط صحيح أو مدعوم.")
        print(f"Error: {e}")

print("البوت يعمل الآن...")
bot.polling()
