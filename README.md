import asyncio
from telegram import Update, InlineKeyboardButton, InlineKeyboardMarkup
from telegram.ext import Application, CommandHandler, CallbackQueryHandler, ContextTypes

# --- REPLACE WITH YOUR BOT TOKEN ---
BOT_TOKEN = "8706402798:AAEaeNgzI1xGNgbAosimuYQ8xBQMDfUn9dw"

user_language = {}

messages = {
    'en': {
        'welcome': "👋 Welcome to Comfy Seasons Bot!\n\n📋 Available commands:\n/clustek - Clustek treatment info\n/spt - Skin Prick Test info\n/safety - Safety guidelines\n/language - Switch to Arabic",
        'clustek': "💉 **What is Clustek?**\n\nClustek is a subcutaneous immunotherapy (SCIT) for allergy related diseases.\n\n**Treats: Allergic Rhinitis, Allergic Conjunctivitis, Atopic Dermatitis and Asthma\n\n It's done by injecting a repeated tiny amounts of the specified allergen every month for about 3-5 years and last for yeats or even decades.\n\n*Manufacturer: Inmunotek, S.L.",
        'spt': "🔬 **What is the Skin Prick Test (SPT)?**\n\nSPT identifies the specific allergens causing your allergic reactions.\n\n**Covers Multiple allergens (The most common in Syria): Pollens, dust mites, molds, animal dander and others.\n\n*How it's done;a tiny ammount fo the allergens are being puttt in the front arm the pricked on yhe skin,If a papule tha is larger than 3mm in diameter appears thats a positive result.\n\n*Results:Within 15-20 minutes",
        'safety': "⚠️ **Safety Guidelines for Clustek**\n\n Clustek is efficatious and safe, most side effects are topical and mild*",
        'brief': "Allergen immunotherapy involves introducing tiny repeated amounts of identified allergens to the patient using a vaccine-like mechanism to modify the patient's immune response so that the patient's immune system responds in a way that stops or reduces allergy symptoms.",
        'importance': "The importance of allergy immunotherapy lies in stopping or reducing allergy symptoms associated with various allergic diseases (such as asthma, allergic rhinitis and conjunctivitis, atopic dermatitis).",
        'lang_changed': "✅ Language changed to English"
    },
    'ar': {
        'welcome': "👋 مرحبا بك في وسيلتك للراحة من التحسس!\n\n📋 الأوامر المتاحة:\n/SPT - معلومات عن اختبار وخز الجلد SPT\n/Clustek - معلومات عن العلاج\n/Safety- إرشادات الأمان\n/Lnguage- التبديل إلى الإنجليزية",
        '
        'spt': "🔬 **ما هو اختبار وخز الجلد (SPT Skin Prick Test)؟**\n\nاختبار SPT يحدد مسببات الحساسية (المؤرجات) المسؤولة عن أعراضك.\n\nيغطي عدد من المؤرجات الأشيع في سوريا:حبوب اللقاح، عث الغبار، العفن، وبر الحيوانات وغيرها.\n\n يتم الفحص بوضع قطرات صغيرة من المواد المحسسة على اليد ثم يتم وخزها بشكل سطحي فقط  \n\nالنتائج: تظهر النتيجة خلال 15-20 دقيقة بحيث تظهر حطاطة جلدية في موضع المادة المحسسة الايجابية \n\n للاستفسار التواصل على احد الأرقام التالية 0993394018 - 0993394031",
         'clustek': "💉 ما هو علاج Clustek؟\n\nكلاستيك هو علاج مناعي تحت الجلد (SCIT) لحساسية الجهاز التنفسي.\n\nيعالج: التهاب الأنف ويخفف أعراض الربو التحسسي والتهاب الملتحمة التحسسي وايضا التهاب الجلد التأتبي.\n\n يتم العلاج عن طريق حقن المريض بالمادة المحسسة (المؤرج) بعد تحديده بفحص ال SPT  بشكل متكرر وبكميات صغيرة جدا مرة كل شهر لمدة  3 الى 5 سنوات ليقوم جهازك المناعي بالاستجابة بطريقة اخف من حيث الأعراض ولفترة زمنية طويلة قد تمتد سنوات وعقود.\n\n للاستفسار التواصل على احد الأرقام التالية 0993394018 - 0993394031 \n\n **الشركة المصنعة:** Inmunotek, S.L.",
        'safety': "⚠️ **إرشادات الأمان لعلاج Clustek**\n\n كلاستيك علاج آمن وفعال , أغلب الاعراض الجانبية موضعية وخفيف كالحكة واحمرار الجلد",
        'brief': "📌 ما هو\n\nالعلاج المناعي للتحسس يعتمد على ادخال كميات صغيرة ومتكررة من المواد المحسسة بعد تحديدها لدى المريض بآلية تشبه اللقاح وذلك لتعديل الاستجابة المناعية لدى المريض لتستجيب مناعة المريض بطريقة توقف او تخفف أعراض التحسس.",
        'importance': "📌 أهمية العلاج\n\nتتأتي أهمية العلاج المناعي للتحسس في ايقاف أو تخفيف أعراض التحسس المرافقة مع الأمراض التحسسية المختلفة (ك الربو ، التهاب الأنف والملتحة التحسسي و التهاب الجلد التأتبي). وهو العلاج الوحيد الذي يعالج المسبب وليس فقط علاج عرضي.",
        'lang_changed': "✅ تم تغيير اللغة إلى العربية"
    }
}

def get_lang(user_id):
    return user_language.get(user_id, 'en')

async def start(update, context):
    user_id = update.effective_user.id
    lang = get_lang(user_id)
    await update.message.reply_text(messages[lang]['welcome'])

async def clustek(update, context):
    user_id = update.effective_user.id
    lang = get_lang(user_id)
    await update.message.reply_text(messages[lang]['clustek'])

async def spt(update, context):
    user_id = update.effective_user.id
    lang = get_lang(user_id)
    await update.message.reply_text(messages[lang]['spt'])

async def safety(update, context):
    user_id = update.effective_user.id
    lang = get_lang(user_id)
    await update.message.reply_text(messages[lang]['safety'])

async def brief(update, context):
    user_id = update.effective_user.id
    lang = get_lang(user_id)
    await update.message.reply_text(messages[lang]['brief'])

async def importance(update, context):
    user_id = update.effective_user.id
    lang = get_lang(user_id)
    await update.message.reply_text(messages[lang]['importance'])

async def language_command(update, context):
    keyboard = [
        [InlineKeyboardButton("English 🇬🇧", callback_data='lang_en')],
        [InlineKeyboardButton("العربية 🇸🇦", callback_data='lang_ar')]
    ]
    await update.message.reply_text("Choose language:", reply_markup=InlineKeyboardMarkup(keyboard))

async def language_callback(update, context):
    query = update.callback_query
    await query.answer()
    user_id = query.from_user.id
    if query.data == 'lang_en':
        user_language[user_id] = 'en'
        await query.edit_message_text(messages['en']['lang_changed'])
    else:
        user_language[user_id] = 'ar'
        await query.edit_message_text(messages['ar']['lang_changed'])

def main():
    app = Application.builder().token(BOT_TOKEN).build()
    app.add_handler(CommandHandler("start", start))
    app.add_handler(CommandHandler("clustek", clustek))
    app.add_handler(CommandHandler("spt", spt))
    app.add_handler(CommandHandler("safety", safety))
    app.add_handler(CommandHandler("brief", brief))
    app.add_handler(CommandHandler("importance", importance))
    app.add_handler(CommandHandler("language", language_command))
    app.add_handler(CallbackQueryHandler(language_callback, pattern='^lang_'))
    print("Bot is running with Arabic/English support...")
    app.run_polling()

if __name__ == "__main__":
    main()
