# Dental_AI_Project

مشروع لبناء (إكمال) الأسنان على ملفات STL (فارغة أو بها أجزاء مفقودة) باستخدام Python وFastAPI. هذا الإصدار يحتوي على pipeline جاهز للاختبار مع نموذج تجريبي بسيط (mirror-based completion). يمكن استبداله لاحقًا بنموذج مدرّب (PCN, GRNet,...).

محتوى المشروع:
- src/app: تطبيق FastAPI + واجهة ويب لرفع STL والحصول على STL مملوء
- src/data: تحويل STL إلى point cloud utilities
- src/models: نموذج إكمال بسيط (baseline)
- src/infer.py: CLI لاستدعاء الموديل
- Dockerfile: لبناء صورة وتشغيل السيرفر
- .github/workflows/ci.yml: GitHub Actions workflow للاختبار

المتطلبات الأساسية:
- Python 3.9+
- pip
- (اختياري) Docker لتشغيل الحاوية

تشغيل محلي سريع:
1. استنسخ الريبو (ساكتب أوامر إنشاء الريبو ورفعها في README أدناه).
2. إعداد env:
   python3 -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt
3. شغل السيرفر:
   export PYTHONPATH=src
   uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
4. افتح المتصفح على: http://localhost:8000/ وتحمّل ملف STL لاختباره.

تشغيل عبر Docker:
1. docker build -t dental_ai:latest .
2. docker run -p 8000:8000 dental_ai:latest
3. افتح http://localhost:8000/

ملحوظات:
- هذا الإصدار يستخدم نموذج تجريبي بسيط (mirror completion) لتوليد أسنان. ليس نموذجًا سريريًا. قبل استخدام أي نتائج مع مرضى، يجب تدريب/تقويم النموذج والحصول على مراجعة طبية.
- لا ترفع بيانات حساسة أو ملفات مرضى إلى GitHub علناً.