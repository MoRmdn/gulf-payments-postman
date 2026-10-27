<div dir="rtl">

<div align="center">

# Gulf Payments Postman

**مجموعات Postman جاهزة للتشغيل لبوابات الدفع Moyasar و Tap Payments و HyperPay، مكتوبة للمبتدئين.**

استورد الملف، اضغط **Send**، وشاهد عملية دفع تجريبية تكتمل أمامك. كل طلب مشروح بالعربية والإنجليزية.

[![Collections](https://github.com/MoRmdn/gulf-payments-postman/actions/workflows/collections.yml/badge.svg)](https://github.com/MoRmdn/gulf-payments-postman/actions/workflows/collections.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

[English](README.md) · **العربية**

</div>

---

## لماذا هذا المستودع؟

كل تطبيق تقريباً في السعودية والخليج يحتاج إلى الدفع الإلكتروني، وكل بوابة دفع لها توثيق مختلف. هذا المستودع يعطيك **طريقاً واحداً بسيطاً ومُختبراً لكل بوابة**:

> أنشئ عملية دفع ← تحقق منها ← استرجع المبلغ

كل طلب يخبرك ماذا يفعل، وأي حقل في الرد يجب أن تنظر إليه، وما الطلب التالي. وهناك اختبارات صغيرة تفحص الرد نيابة عنك وتمرر الأرقام للطلب التالي تلقائياً.

## ماذا يوجد في الداخل؟

| البوابة | هل تحتاج تسجيلاً؟ | البداية السريعة (بدون متصفح) | يغطي أيضاً |
|---|---|---|---|
| **Moyasar** | نعم، مفتاح اختبار مجاني | دفع STC Pay ← رمز التحقق ← استرجاع | البطاقة مع 3-D Secure، روابط الدفع، الحجز ← الخصم / الإلغاء |
| **Tap Payments** | لا، انسخ مفتاح Tap التجريبي المشترك من توثيقها | عميل ← عملية دفع ← رابط دفع | الاسترجاع بعد الدفع، الحجز ← الخصم / الإلغاء |
| **HyperPay** | لا، حساب تجريبي مشترك مرفق | دفع بالبطاقة ← تحقق ← استرجاع | الحجز ← الخصم ← الاسترجاع، إلغاء الحجز، صفحة الدفع COPYandPAY |

كل شيء يعمل في **وضع الاختبار**. لا تتحرك أي أموال حقيقية.

## البداية السريعة (3 خطوات)

1. **حمّل** المستودع: الزر الأخضر **Code** ثم **Download ZIP** (أو استخدم `git clone`).
2. افتح [Postman](https://www.postman.com/downloads/) ثم **Import** واسحب المجلدين `collections` و `environments`.
3. اختر البيئة من الزاوية العلوية (مثلاً **HyperPay (test)**)، وافتح المجلد **1. Quick start (no browser)**، واضغط **Send** على كل طلب بالترتيب. راجع تبويب **Test Results** تحت الرد.

بالنسبة إلى **Tap** و **Moyasar** الصق أولاً مفتاح اختبار في الحقل `api_key` داخل البيئة. تنشر Tap مفتاحاً مشتركاً يستطيع أي شخص استخدامه، ومفتاح Moyasar مجاني. راجع [طريقة الحصول على مفاتيح الاختبار](docs/get-test-keys.ar.md).

## التشغيل من الطرفية

باستخدام [Postman CLI](https://learning.postman.com/docs/postman-cli/postman-cli-installation/):

</div>

```bash
postman collection run collections/hyperpay.postman_collection.json -e environments/hyperpay.postman_environment.json -i "1. Quick start (no browser)"
```

<div dir="rtl">

استبدل `hyperpay` بـ `tap` أو `moyasar`. مع Tap و Moyasar مرّر المفتاح دون حفظه في ملف:

</div>

```bash
postman collection run collections/moyasar.postman_collection.json -e environments/moyasar.postman_environment.json -i "1. Quick start (no browser)" --env-var "api_key=sk_test_YOUR_KEY"
```

<div dir="rtl">

## مقارنة البوابات الثلاث

| | Moyasar | Tap Payments | HyperPay |
|---|---|---|---|
| رابط الاختبار | `https://api.moyasar.com/v1` | `https://api.tap.company/v2` | `https://eu-test.oppwa.com` |
| المصادقة | Basic: المفتاح السري اسم مستخدم وكلمة المرور فارغة | `Bearer sk_test_...` | `Bearer <token>` مع الحقل `entityId` |
| صيغة الجسم | JSON | JSON | حقول نموذج (x-www-form-urlencoded) |
| كتابة مبلغ 10 ريال | `1000` (بالهللة) | `10` | `"10.00"` |
| كيف تعرف أن الدفع نجح | `status: "paid"` | `status: "CAPTURED"` | `result.code` يطابق نمط النجاح |
| بطاقة تجريبية تعمل مباشرة | `4111 1111 1111 1111` | `4508 7500 1574 1019`، الانتهاء `01/39`، الرمز `100` | `4200 0000 0000 0000` |

مزيد من البطاقات لكل بوابة: [docs/test-cards.ar.md](docs/test-cards.ar.md).

## تعلّم الأساسيات

- [كيف يعمل الدفع الإلكتروني](docs/how-online-payments-work.ar.md): وضع الاختبار والوضع الحقيقي، و 3-D Secure، والفرق بين الاسترجاع والإلغاء، وروابط الدفع، ولماذا يجب أن يتأكد خادمك من كل عملية دفع.
- [طريقة الحصول على مفاتيح الاختبار](docs/get-test-keys.ar.md) لكل بوابة.
- [البطاقات التجريبية](docs/test-cards.ar.md) للنجاح والرفض وعدم كفاية الرصيد.

## الأمان

- **مفاتيح الاختبار فقط.** لا تضع أبداً مفتاحاً حقيقياً (`sk_live_...`) في هذه الملفات أو في مستودع عام.
- احفظ مفاتيحك داخل بيئة Postman، وليس في ملفات JSON التي ترفعها. الملفات التي تنتهي بـ `.local.postman_environment.json` مستثناة مسبقاً في `.gitignore`.
- بيانات HyperPay الموجودة في `environments/` ومفتاح Tap المشترك هي **بيانات اختبار عامة** منشورة في توثيقهما. يستخدمها مطورون كثيرون، فلا ترسل بها بيانات شخصية حقيقية أبداً.
- إرسال أرقام البطاقات من خادمك مقبول للتعلم في وضع الاختبار. أما في التطبيق الحقيقي فاستخدم صفحة الدفع أو أداة الدفع التي توفرها البوابة، إلا إذا كنت حاصلاً على شهادة PCI DSS.

## المساهمة

تريد إضافة PayTabs أو Tabby أو Tamara أو Paymob أو بوابة أخرى؟ وجدت طلباً توقف عن العمل؟ راجع [CONTRIBUTING.md](CONTRIBUTING.md).

## إخلاء مسؤولية

هذا مشروع مجتمعي، وليس تابعاً لـ Moyasar أو Tap Payments أو HyperPay ولا معتمداً منها. جميع الأسماء والعلامات التجارية مملوكة لأصحابها. راجع دائماً التوثيق الرسمي قبل الإطلاق الحقيقي:
[Moyasar](https://docs.moyasar.com) · [Tap](https://developers.tap.company) · [HyperPay](https://hyperpay.docs.oppwa.com)

## الترخيص

[MIT](LICENSE)

---

<div align="center">

إذا وفّر عليك هذا المستودع وقتاً، فنجمة ⭐ منك تساعد مطورين آخرين على الوصول إليه.

</div>

</div>
