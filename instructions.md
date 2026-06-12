# 👑 وثيقة تعليمات هندسة وبناء أدوات منصة Creator King الموطنة (Master Instructions)

## 🛠️ أولاً: معايير الجودة والواجهة والترجمة الموحدة (Global Core Framework)

### 1. فلسفة الواجهة وتجربة المستخدم (Premium UI/UX Architecture)
* **ثنائية التحكم (Presets vs Custom):** في أي أداة تتطلب مقاسات، أبعاد، نسب، أو معدلات؛ يجب توفير أزرار سريعة ومصممة بعناية للخيارات الجاهزة (Presets) لأشهر منصات السوشيال ميديا، وبجوارها مباشرة حقول إدخال رقمية أو يدوية مخصصة (Custom Inputs) تمنح المستخدم حرية التحكم المطلقة بالبكسل أو القيمة الدقيقة.
* **التوافق التام مع اللمس والتابلت (Tablet & Touch First):** الواجهات مبنية بالكامل لتكون مريحة جداً للمس على أجهزة التابلت والشاشات المحمولة. الأزرار عريضة، عناصر التحكم متباعدة، والقوائم منسدلة بذكاء لمنع الضغط الخاطئ بدون الحاجة لماوس.
* **التفاعل الحي والجاذبية البصرية (Micro-Details & Animations):**
  * مناطق رفع الملفات (Drag & Drop Zone) يجب أن تتوهج بنبضات النيون عند سحب الملفات فوقها.
  * أشرطة التقدم (Progress Bars) يجب أن تكون تفاعلية ومتحركة، وتعرض النسبة المئوية بدقة مع رسائل نصية تتغير ديناميكياً لتعكس خطوة المعالجة الحالية.
  * تأثيرات الحفز الحركي (CSS Transitions) ناعمة وسلسة لجميع العناصر عند التمرير (Hover) أو النقر (Active).

### 2. البنية التقنية والمعالجة المحلية (100% Client-Side Processing)
* **الخصوصية والتكلفة الصفرية:** تتم معالجة كافة العمليات، الفيديوهات، الصور، النصوص، والملفات محلياً بنسبة 100% داخل متصفح المستخدم (Client-Side) باستخدام طاقة جهاز المستخدم الذاتية وبدون أي رفع للسيرفرات أو استدعاءات لواجهات برمجية مدفوعة.
* **نظام معالجة الأخطاء الذكي (Graceful Error Handling):** يمنع تماماً انهيار الأداة أو تجمد الواجهة. إذا حدث خطأ (ملف تالف، صيغة خاطئة، تجاوز حجم)، يتم التقاط الخطأ وعرض نافذة منبثقة أنيقة ومفسرة (Toast Notification) تشرح للمستخدم المشكلة والحل بدقة.

### 3. نظام الترجمة الدولي الصارم (Mandatory i18n Architecture)
* **منع النصوص الصلبة:** ممنوع منعاً باتاً كتابة أي نص (عربي أو إنجليزي أو غيره) بشكل صلب وثابت داخل ملفات الـ HTML أو أكواد الـ JavaScript للأدوات.
* **آلية الاستدعاء:** يتم استدعاء كافة النصوص، العناوين، الأزرار، التلميحات (Placeholders)، ورسائل الخطأ عبر دالة الترجمة الموحدة `t('tools.tool_id.key')`.
* **مزامنة ملفات اللغة:** عند بناء أو صيانة أي أداة، يجب توليد وتحديث المفاتيح المقابلة لها في ملف اللغات الدولي `locales/en.json` بناءً على الهيكل الدقيق المرفق أسفل كل أداة في هذه الوثيقة.

---

## 📂 ثانياً: تفاصيل بناء الأدوات الـ 38 وهياكل ترجمتها

### 📑 قسـم 1: أدوات الفيديو والصوت (12 أداة)

#### 1. مقطع الفيديوهات (Video Cutter)
* **خيارات التحكم والـ UI/UX:** شريط زمني مرئي (Timeline Slider) بمؤشرين عريضين متوافقين مع اللمس لتحديد البداية والنهاية بالسحب، وحقول إدخال رقمية يدوية للوقت (ساعة : دقيقة : ثانية : جزء من الثانية). يتزامن الشريط والحقول حياً، مع زر لمعاينة اللقطة المحددة قبل التصدير.
* **تعليمات الوكيل التقنية:** استخدم `FFmpeg.wasm`. تأكد من تحديث المدخلات الرقمية تلقائياً عند حركة السلايدر والعكس صحيح لضمان الدقة المطلقة للمستخدم.
* **هيكل ترجمة locales/en.json المطلوب:**
"video_cutter": {
  "title": "Video Cutter",
  "desc": "A precise client-side tool that allows content creators to slice and cut local video files instantly using an interactive timeline slider or manual timestamp fields.",
  "upload_btn": "Upload Video File",
  "start_time": "Start Cut Point",
  "end_time": "End Cut Point",
  "preview": "Preview Selected Segment",
  "export": "Cut & Export Video",
  "error_format": "Unsupported video file format."
}

#### 2. دمج الفيديوهات (Video Merger)
* **خيارات التحكم والـ UI/UX:** منطقة سحب وإفلات نيون لرفع ملفات متعددة، قائمة مرئية للمقاطع المرفوعة مع أزرار صعود وهبوط أو سحب لإعادة الترتيب باللمس، وأزرار خيارات جاهزة لتوحيد الأبعاد (تطابق أبعاد الفيديو الأول، جعل الكل 16:9، أو جعل الكل 9:16) لحل مشكلة اختلاف مقاسات الفيديوهات المرفوعة.
* **تعليمات الوكيل التقنية:** استخدم `FFmpeg.wasm`. برمج الأداة لتقوم بعمل تدوير أو تغيير حجم تلقائي (Scale/Pad) للمقاطع لتتطابق مع الخيار المختار قبل عملية الـ `concat`.
* **هيكل ترجمة locales/en.json المطلوب:**
"video_merger": {
  "title": "Video Merger",
  "desc": "Combines multiple video clips into one cohesive video file locally, featuring canvas auto-scaling and visual reordering controls optimized for touch screens.",
  "drop_zone": "Drag & Drop Multiple Videos Here",
  "reorder": "Reorder Selected Clips",
  "resolution_preset": "Unified Output Resolution",
  "merge_btn": "Merge Videos Now",
  "processing": "Merging files locally, please wait..."
}

#### 3. ضاغط الفيديو (Video Compressor)
* **خيارات التحكم والـ UI/UX:** أزرار خيارات جاهزة لنسب الضغط (ضغط خفيف 20%، ضغط متوازن 50%، ضغط فائق لتيك توك وواتساب)، وبجوارها شريط تمرير (Slider) يدوي لتحديد حجم الملف المستهدف بالميغابايت (مثال: أقصى حجم 25 ميغابايت للديسكورد). يظهر عداد حي يوضح الحجم الأصلي والحجم المتوقع بدقة.
* **تعليمات الوكيل التقنية:** استخدم `FFmpeg.wasm`. اربط السلايدر بقيم الـ CRF برمجياً (من 18 إلى 35)، واجعل الكود يحسب الحجم التقريبي بناءً على طول الفيديو والـ Bitrate المختار.
* **هيكل ترجمة locales/en.json المطلوب:**
"video_compressor": {
  "title": "Video Compressor",
  "desc": "Reduces large video file sizes in the browser using custom CRF scaling, targeting specific social media network limits without destroying key visual quality.",
  "preset_low": "Light Compression (High Quality)",
  "preset_mid": "Balanced Compression",
  "preset_high": "Maximum Compression (Smallest Size)",
  "custom_size": "Target File Size (MB)",
  "original_size": "Original Size",
  "estimated_size": "Estimated Target Size",
  "compress_btn": "Compress Video Now"
}

#### 4. مستخرج الصوت (Audio Extractor)
* **خيارات التحكم والـ UI/UX:** أزرار جاهزة لاختيار صيغة الصوت النهائية (MP3 للانتشار، WAV للجودة الاحترافية)، وقائمة منسدلة لتحديد الـ Bitrate (128kbps, 192kbps, 320kbps)، مع خيار إضافي لتفعيل شريط مؤقت لقص جزء محدد من الصوت المستخرج فقط بدلاً من استخراجه كاملاً.
* **تعليمات الوكيل التقنية:** استخدم `FFmpeg.wasm`. برمج الأوامر بناءً على الصيغة والـ Bitrate المختار، مع استخدام المعالجة المباشرة للأداء السريع.
* **هيكل ترجمة locales/en.json المطلوب:**
"audio_extractor": {
  "title": "Audio Extractor",
  "desc": "Rips and extracts audio tracks directly out of video files locally, saving them into optimized formats like high-fidelity MP3 or lossless WAV.",
  "format": "Target Audio Format",
  "bitrate": "Audio Quality Bitrate",
  "extract_btn": "Extract Audio File",
  "success_msg": "Audio file extracted successfully!"
}

#### 5. محول الصيغ والـ GIF (Video to GIF & Format Converter)
* **خيارات التحكم والـ UI/UX:** قائمة منسدلة لاختيار الصيغ المستهدفة للتحويل (MP4, WebM, GIF). عند اختيار GIF، يظهر للمستخدم تلقائياً شريط تمرير لتحديد عدد الإطارات في الثانية (10fps, 15fps, 24fps) ومقاس العرض (320px, 480px, أو حقل كاستم يدوي).
* **تعليمات الوكيل التقنية:** استخدم `FFmpeg.wasm`. اضبط قيم أبعاد الـ GIF والـ Framerate برمجياً بناءً على مدخلات المستخدم لتقليل تضخم الحجم النهائي للملف.
* **هيكل ترجمة locales/en.json المطلوب:**
"video_converter": {
  "title": "Format & GIF Converter",
  "desc": "Converts local videos into standard web formats or loops them into high-performance animated GIFs with frame-rate and scaling optimization options.",
  "target_format": "Convert Target To",
  "fps_label": "Frames Per Second (GIF)",
  "width_label": "Output Width (Pixels)",
  "convert_btn": "Start Conversion Process"
}

#### 6. عاكس الفيديو (Video Reverser)
* **خيارات التحكم والـ UI/UX:** أزرار خيارات لمعالجة الصوت المصاحب للفيديو المعكوس: (عكس الصوت مع الفيديو، كتم الصوت تماماً، أو إبقاء الصوت الأصلي يعمل للأمام بينما الفيديو يعود للخلف).
* **تعليمات الوكيل التقنية:** استخدم `FFmpeg.wasm`. برمج الفلاتر المعقدة لتعزل مسار الصوت وتطبق عليه الأمر المختار (`-af areverse` أو حذف الصوت تماماً عبر `-an`).
* **هيكل ترجمة locales/en.json المطلوب:**
"video_reverser": {
  "title": "Video Reverser",
  "desc": "Reverses video play order local-side to create captivating rewind loop effects, offering dedicated modes to handle the accompanying audio track sync.",
  "audio_mode": "Audio Channel Handling",
  "audio_reverse": "Reverse Audio with Video",
  "audio_mute": "Mute Audio Track",
  "audio_keep": "Keep Audio Running Forward",
  "reverse_btn": "Reverse Video Track"
}

#### 7. متحكم السرعة (Speed Changer)
* **خيارات التحكم والـ UI/UX:** أزرار سرعة جاهزة سريعة (0.5x لإبطاء، 2x لتسريع)، وبجوارها شريط تمرير مخصص (Custom Slider) يبدأ من 0.25x وحتى 4.0x بخطوات دقيقة (0.05)، مع زر Toggle لتفعيل أو تعطيل ميزة "الحفاظ على نبرة الصوت النظيفة" (Pitch Correction).
* **تعليمات الوكيل التقنية:** استخدم `FFmpeg.wasm`. طبق فلتر `atempo` وفلتر `setpts` وتأكد من مضاعفة فلاتر الصوت برمجياً إذا تجاوزت السرعة المحددة 2x لأن فلتر المتصفح يقف عند 2x كحد أقصى.
* **هيكل ترجمة locales/en.json المطلوب:**
"speed_changer": {
  "title": "Video Speed Controller",
  "desc": "Speeds up or slows down locally imported videos with sub-decimal accuracy, utilizing real-time audio pitch adjustments to keep voices sounding crisp.",
  "custom_speed": "Select Dynamic Speed",
  "pitch_lock": "Maintain Vocal Pitch (Clean Voice)",
  "process_btn": "Apply Speed Engine"
}
بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 8. إضافة العلامة المائية (Watermark Adder)]

* **خيارات التحكم والـ UI/UX:** زر خيار لتحديد نوع العلامة المائية (صورة لوغو مرفوعة، أو نص مكتوب يفتح حقل نصي مخصص، ومنقي ألوان وقائمة خطوط)، شبكة اتجاهات جاهزة من 9 مربعات لتحديد الزاوية، وبجوارها حقلان رقميان لـ (X Offset و Y Offset بالبكسل) لتحريك العلامة بدقة متناهية، وسلايدر للتحكم في الشفافية (Opacity من 0% إلى 100%).

* **تعليمات الوكيل التقنية:** استخدم `FFmpeg.wasm` وفلاتر الـ `overlay` البرمجية لدمج المدخلات فوق إحداثيات الفيديو بدقة وموثوقية محلية.

* **هيكل ترجمة locales/en.json المطلوب:**
"watermark_adder": {
  "title": "Watermark Adder",
  "desc": "Brands user videos client-side by watermarking them with highly adjustable textual markers or geometric brand images using precise placement offsets.",
  "type_text": "Text Watermark Style",
  "type_image": "Logo/Image Watermark Style",
  "text_input_placeholder": "Type your watermark text here...",
  "position_grid": "Watermark Alignment Position",
  "opacity": "Opacity Transparency Level",
  "apply_btn": "Burn Watermark into Video"
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 9. مسجل الشاشة والكاميرا (Screen & Camera Recorder)]

* **خيارات التحكم والـ UI/UX:** أزرار اختيار مصادر التسجيل (الشاشة فقط، الكاميرا فقط، أو الشاشة + الكاميرا معاً)، تفعيل/تعطيل الميكروفون، وقائمة خيارات لوضع الكاميرا (دائرة عائمة أسفل اليسار، مستطيل جانبي، أو وضع تقسيم الشاشة نصفين).

* **تعليمات الوكيل التقنية:** استخدم مكاتب المتصفح المدمجة (`MediaRecorder` و `Canvas API`). ارسم دفق الكاميرا فوق دفق الشاشة بداخل الـ Canvas بناءً على الإعداد المختار حياً أثناء عملية التسجيل.

* **هيكل ترجمة locales/en.json المطلوب:**
"recorder": {
  "title": "Screen & Camera Recorder",
  "desc": "A zero-latency native browser-based recorder that captures desktop screens alongside webcam video overlays, encoding the stream straight to WebM/MP4.",
  "source_select": "Capture Source Target",
  "audio_mic": "Include Microphone Capture",
  "cam_layout": "Camera Overlay Structure Layout",
  "start_btn": "Start Recording Session",
  "stop_btn": "Stop & Save Capture Locally"
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 10. صانع النغمات والمقاطع الصوتية (Audio Cutter)]

* **خيارات التحكم والـ UI/UX:** رسم بياني للموجة الصوتية مع إمكانية التكبير والتصغير (Zoom In/Out)، مدخلات رقمية دقيقة للوقت بالدقائق والثواني والأجزاء من الثانية، وأزرار لتفعيل ميزات مخصصة (تلاشي الصوت تدريجياً في البداية Fade-in، وتلاشي الصوت في النهاية Fade-out) مع تحديد مدتها بالثواني عبر حقول رقمية.

* **تعليمات الوكيل التقنية:** استخدم `Web Audio API` لاقتطاع الـ ArrayBuffer وتطبيق معادلات الـ Gain لخفت ورفع الصوت تدريجياً محلياً.

* **هيكل ترجمة locales/en.json المطلوب:**
"audio_cutter": {
  "title": "Audio Cutter & Ringtone Maker",
  "desc": "Trims down long audio segments utilizing a clean visual wave renderer with customizable algorithmic amplitude fade-ins and fade-outs.",
  "fade_in": "Fade-In Dynamic Duration (seconds)",
  "fade_out": "Fade-Out Dynamic Duration (seconds)",
  "cut_btn": "Cut Audio Track File"
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 11. منقي الصوت الأساسي (Basic Audio Purifier)]

* **خيارات التحكم والـ UI/UX:** أزرار جاهزة لنوع التصفية المطلوبة: (إزالة وشيش الخلفية، تضخيم صوت التعليق الصوتي الضعيف، أو إزالة الترددات الحادة للميكروفونات)، مع شريط تمرير للتحكم في قوة الفلتر المستهدف (Intensity من 1 إلى 10).

* **تعليمات الوكيل التقنية:** استخدم الـ `BiquadFilterNode` المدمج في المتصفح، واضبط مرشحات التمرير (Low-pass, High-pass, Band-pass) لتتفاعل قيمها الحسابية ديناميكياً مع السلايدر.

* **هيكل ترجمة locales/en.json المطلوب:**
"audio_purifier": {
  "title": "Audio Noise Purifier",
  "desc": "Implements local audio equalizers and biquad noise filtering modules to suppress low-frequency hums and enhance dialogue speech patterns.",
  "filter_type": "Select Purification Profile",
  "profile_noise": "Remove Background Noise/Hiss",
  "profile_boost": "Vocal/Voiceover Power Boost",
  "intensity": "Purification Filter Strength Level",
  "purify_btn": "Purify Audio Track Now"
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 12. عداد الـ BPM والمؤقت الموسيقي (BPM Counter & Audio Analyzer)]

* **خيارات التحكم والـ UI/UX:** تبويبان للتحكم؛ الوضع التلقائي: زر لرفع ملف الصوت ليقوم النظام بتحليله وعرض رقم الـ BPM الثابت، والوضع اليدوي: زر ضخم ومريح للمس مكتوب عليه "اضغط هنا مع الإيقاع (Tap)"، يضغط عليه صانع المحتوى مع دقات الموسيقى، ليظهر الـ BPM حياً بناءً على متوسط نقراته المتتالية.

* **تعليمات الوكيل التقنية:** برمج دالة حسابية تقيس الفارق الزمني بالملي ثانية بين النقرات المتتالية لعرض الـ BPM في الوضع اليدوي، وخوارزمية فحص القمم للطاقة الصوتية في الملفات المرفوعة.

* **هيكل ترجمة locales/en.json المطلوب:**
"bpm_counter": {
  "title": "BPM Beat Counter",
  "desc": "Tracks and identifies musical tempo metrics through interactive touch-tap triggers or via local algorithmic file-peak threshold audio analysis.",
  "tap_btn": "Tap to the Beat Rhythm Here",
  "auto_analyze": "Or Upload File for Automatic Detection",
  "result_label": "Calculated Beats Per Minute (BPM)"
}

---

### 📑 قسـم 2: أدوات التصميم والغرافيك (7 أدوات)

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل 

[#### 13. صانع الصور المصغرة (Thumbnail Maker)]

* **خيارات التحكم والـ UI/UX:** أزرار مقاسات جاهزة بضغطة زر (يوتيوب 1280x720، فيسبوك بوست، إنستغرام مربع)، وبجوارها حقول تخصيص الأبعاد يدوياً بكتابة العرض والطول بالبكسل. أدوات التحكم في النصوص: حقل النص، زر اختيار الخط، حجم الخط، لون النص، ولون وحجم حد النص (Stroke) لجعله بارزاً، مع زر لإضافة ظل أسود خلف النص والتحكم بمدى انتشاره.

* **تعليمات الوكيل التقنية:** استخدم الـ HTML5 Canvas بالكامل، واجعل كل نص مضاف عبارة عن كائن (Object) يملك إحداثيات (X, Y) قابلة للتعديل والتحريك عبر الماوس أو اللمس على التابلت.

* **هيكل ترجمة locales/en.json المطلوب:**
"thumbnail_maker": {
  "title": "Thumbnail Layout Designer",
  "desc": "A lightweight HTML5 Canvas graphic layout workstation equipped with pre-sized platform grids, font stroke styling, and real-time element drag tracking.",
  "text_stroke": "Text Border Outline (Stroke)",
  "text_shadow": "Enable Premium Drop Shadow",
  "add_text": "Add New Text Layer",
  "download_png": "Download High-Res PNG Thumbnail"
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 14. قاص ومغير أبعاد الصور (Image Cropper & Resizer)]

* **خيارات التحكم والـ UI/UX:** أزرار مقاسات ونسب جاهزة للسوشيال ميديا (1:1 بوست، 9:16 ريلز وتيك توك، 16:9 يوتيوب)، زر خيار حر (Freeform) يتيح سحب أطراف مربع القص بحرية تامة، وحقول إدخال رقمية يدوية لكتابة العرض والارتفاع المستهدف بالبكسل مباشرة مع زر تفعيل "قفل النسبة والتناسب" (Lock Aspect Ratio).

* **تعليمات الوكيل التقنية:** ادمج مكتبة `Cropper.js`. اربط قيم الواجهة والحقول الرقمية بأحداث المكتبة (`data.width`, `data.height`) لتحديث العرض والارتفاع بشكل فوري ومتزامن.

* **هيكل ترجمة locales/en.json المطلوب:**
"image_cropper": {
  "title": "Image Cropper & Resizer",
  "desc": "Enables localized imagery cropping under locked geometric aspect ratios or arbitrary manual configurations via touch-responsive viewport anchors.",
  "free_ratio": "Free Aspect Ratio Mode",
  "lock_ratio": "Lock Proportional Ratio",
  "width_px": "Target Width (px)",
  "height_px": "Target Height (px)",
  "crop_btn": "Crop & Download Image"
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 15. ضاغط ومحول الصور (Image Compressor & Converter)]

* **خيارات التحكم والـ UI/UX:** قائمة منسدلة لاختيار صيغة الحفظ النهائية (JPEG, PNG, WebP)، شريط تمرير (Slider) لتحديد جودة وضغط الصورة من 
10% إلى 100%)، وحقل اختياري لتحديد أقصى عرض للصورة بالبكسل لتصغير الأبعاد والوزن معاً. يعرض الحجم الأصلي والحجم الجديد ونسبة التوفير فوراً.

* **تعليمات الوكيل التقنية:** استخدم `canvas.toDataURL` لتغيير صيغة وجودة الصورة محلياً داخل المتصفح وعرض النتائج بشكل فوري وحي للمستخدم.

* **هيكل ترجمة locales/en.json المطلوب:**
"image_compressor": {
  "title": "Image Compressor & Converter",
  "desc": "Compresses heavy raw photography locally by converting files into modern WebP extensions while reporting byte size alterations on the fly.",
  "quality_label": "Target Compression Quality",
  "max_width": "Max Allowed Width Limit (Optional)",
  "saved_space": "Total Storage Space Saved"
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 16. مستخرج بالتة الألوان (Color Palette Extractor)]

* **خيارات التحكم والـ UI/UX:** قائمة منسدلة لاختيار عدد الألوان المطلوب استخراجها من الصورة المرفوعة (5 ألوان، 8 ألوان، أو 12 لوناً)، وزر للتبديل بين صيغ عرض كود
  اللون (HEX, RGB, HSL)، مع زر "نسخ الكل" بضغطة واحدة بجانب أزرار النسخ الفردية لكل كرت لون مستخرج.

* **تعليمات الوكيل التقنية:** ارسم الصورة على Canvas مصغر واقرأ مصفوفة الألوان عبر `getImageData`، واعرض لوحة الألوان المستخرجة مع نظام تفاعلي يظهر كلمة "تم النسخ!" عند النقر.

* **هيكل ترجمة locales/en.json المطلوب:**
"palette_extractor": {
  "title": "Color Palette Extractor",
  "desc": "Scans structural data arrays of visual images local-side to sample dominant pixel color values into exportable design swatch systems.",
  "colors_count": "Number of Extracted Colors",
  "color_format": "Color Code Format System",
  "copy_all": "Copy Entire Palette Codes",
  "copied": "Copied Successfully!"
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 17. مصحح المناطق الآمنة (Social Media Safe Area Checker)]

* **خيارات التحكم والـ UI/UX:** أزرار لاختيار نوع واجهة العرض الشفافة التراكبية (واجهة تيك توك، واجهة ريلز إنستغرام، واجهة شورتس يوتيوب)، وشريط تمرير للتحكم في شفافية الواجهة التراكبية (Overlay Opacity من 10% إلى 100%) لرؤية تفاصيل التصميم، وزر "تحميل التصميم النظيف فقط".

* **تعليمات الوكيل التقنية:** استخدم طبقات CSS متراكبة بدقة ومطابقة لقياسات الهواتف الحقيقية (`position: absolute; pointer-events: none;`) لعرض أزرار وتفاصيل المنصات فوق الصورة المرفوعة بشكل دقيق.

* **هيكل ترجمة locales/en.json المطلوب:**
"safe_area": {
  "title": "Social Media Safe Area Checker",
  "desc": "Overlays calibrated translucent UI vector wireframes representing core app layouts to ensure background content avoids accidental placement overlap errors.",
  "select_platform": "Select UI Overlay Layout",
  "overlay_opacity": "Overlay Grid Transparency",
  "download_clean": "Export Clean Design Only"
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 18. صانع الـ QR Code المطور (Enhanced QR Code Maker)]

* **خيارات التحكم والـ UI/UX:** حقل النص أو الرابط المستهدف، منقي ألوان مزدوج (لون النقاط الداكنة، ولون الخلفية)، خيار رفع صورة (Logo) لوضعها في المنتصف، مع قائمة خيارات لحجم اللوغو (صغير، متوسط، كبير)، وأزرار جاهزة لاختيار شكل النقاط (مربعات كلاسيكية، نقاط دائرية Round، أو خطوط ممتدة).

* **تعليمات الوكيل التقنية:** استخدم مكتبة توليد QR مبنية على الـ Canvas لتتمكن من تخصيص رسم الأشكال المخصصة وإدراج اللوغو في المنتصف برمجياً ومحلياً 100%.

* **هيكل ترجمة locales/en.json المطلوب:**
"qr_maker": {
  "title": "Premium QR Code Generator",
  "desc": "Constructs thematic high-contrast matrix barcodes containing central branding emblems, dot shapes, and custom matrix color palettes fully inside the client browser.",
  "color_dots": "Custom Dots Color",
  "color_bg": "Custom Background Color",
  "logo_size": "Center Brand Logo Size",
  "dot_style": "Dot Shape Pattern Style"
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل 

[#### 19. فاحص تباين الألوان الاحترافي (Color Contrast Checker)]

* **خيارات التحكم والـ UI/UX:** منقي ألوان أو حقل نصي لكتابة كود لون الخلفية (Background HEX)، ومنقي ألوان أو حقل نصي لكتابة كود لون النص (Text HEX)، مع زر مخصص لتبديل الألوان عكسياً (Swap Colors) بضغطة واحدة لتسريع عملية الفحص والتحليل للمصممين.

* **تعليمات الوكيل التقنية:** طبق معادلات السطوع النسبي وحساب التباين المعتمدة عالمياً في WCAG، واعرض النتيجة الرقمية بوضوح مع إشارات ملونة توضح نجاح أو فشل معايير (AA للخط الصغير، AA للخط الكبير، AAA للخط الصغير، AAA للخط الكبير).

* **هيكل ترجمة locales/en.json المطلوب:**
"contrast_checker": {
  "title": "Color Contrast Checker (WCAG)",
  "desc": "Calculates luminance contrast math formulas automatically to measure visual clarity parameters according to strict accessible design standards.",
  "text_color": "Foreground Text Color",
  "bg_color": "Background Layout Color",
  "swap_btn": "Swap Background & Text",
  "score_label": "Contrast Ratio Result",
  "status_pass": "PASS (Accessible)",
  "status_fail": "FAIL (Low Contrast)"
}

---

### 📑 قسـم 3: أدوات النصوص والسكربت (13 أداة)

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 20. ملقن النصوص (Teleprompter)]

* **خيارات التحكم والـ UI/UX:** صندوق النص لكتابة أو لصق السكربت، أشرطة تمرير (Sliders) مخصصة وعريضة لكل من: سرعة التمرير التلقائي (Scroll Speed)، وحجم الخط (Font Size). أزرار تفعيل ميزات خاصة: زر قلب النص أفقياً (Mirror Text) للمرايا العاكسة، زر لتغيير المحاذاة، وزر لتغيير خلفية الشاشة (أسود/أبيض أو أزرق/أصفر).

* **تعليمات الوكيل التقنية:** استخدم `requestAnimationFrame` للتحكم الدقيق والمستقر بالسرعة ديناميكياً، وطبق تحويلات الـ CSS (`transform: scaleX(-1)`) لعمل خاصية المرآة بسلاسة فائقة.

* **هيكل ترجمة locales/en.json المطلوب:**
"teleprompter": {
  "title": "Smart Studio Teleprompter",
  "desc": "Launches a dynamic auto-scrolling reading platform built with high-velocity requestAnimationFrame code, offering mirror mirroring tricks for physical glass gear.",
  "speed": "Auto-Scrolling Speed",
  "font_size": "Display Text Font Size",
  "mirror_mode": "Mirror Mode (For Reflector Glass)",
  "start_tele": "Start Prompting Session"
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 21. منظم ومحرر السكربتات (Script Organizer & Editor)]

* **خيارات التحكم والـ UI/UX:** قائمة جانبية (Sidebar) تحتوي على قائمة السكربتات المحفوظة محلياً مع زر "سكربت جديد" وزر "حذف"، شريط أدوات للمحرر يحتوي على أزرار تنسيق سريعة (تظليل بلون أصفر للنقاط المهمة، كود عريض Bold، ووضع خط)، مع زر لتصدر السكربت كملف نصي خارجي (`.txt`) أو ملف وورد (`.docx`).

* **تعليمات الوكيل التقنية:** استخدم الـ `localStorage` لتخزين مصفوفة السكربتات بهيكل JSON يحتوي على (العنوان، النص، وتاريخ التعديل) لضمان بقائها وحفظها التلقائي في متصفح التابلت دائماً.

* **هيكل ترجمة locales/en.json المطلوب:**
"script_editor": {
  "title": "Script Organizer & Editor",
  "desc": "A locally sandboxed markup editor providing instant local storage session state updates, custom text color highlighter palettes, and text document downloads.",
  "new_script": "Create New Script",
  "auto_save": "Saved automatically to local storage",
  "export_txt": "Export as Clean TXT File"
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 22. مقسم النصوص (Thread Splitter)]

* **خيارات التحكم والـ UI/UX:** أزرار خيارات جاهزة للحد الأقصى للحروف (280 حرفاً لمنصة X، 3000 حرف للينكدإن، أو تخصيص يدوي عبر حقل رقمي)، وزر تفعيل/تعطيل إضافة الترقيم التلقائي في بداية أو نهاية كل جزء (مثال: 1/5، 2/5 أو أيموجي الخيط 🧵).

* **تعليمات الوكيل التقنية:** برمج خوارزمية ذكية تقسم النص بناءً على المسافات والفراغات النصية (`.lastIndexOf(' ')`) لتجنب قطع الكلمة الواحدة في المنتصف بشكل عشوائي مشوه.

* **هيكل ترجمة locales/en.json المطلوب:**
```json
"thread_splitter": {
  "title": "Social Media Thread Splitter",
  "desc": "Intelligently parses massive text blocks into segmented threads based on platform constraints without cleaving active vocabularies down the middle.",
  "char_limit": "Max Character Limit per Post",
  "auto_number": "Add Auto-Numbering (e.g., 1/3)",
  "split_btn": "Split Text Into Thread Now"
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 23. محلل العناوين والـ Hooks (Headline & Hook Analyzer)]

* **خيارات التحكم والـ UI/UX:** حقل كتابة العنوان المقترح، خيار تحديد المنصة المستهدفة عبر أزرار خيارات (يوتيوب، تيك توك، مقال ويب) لتغيير معايير وفلاتر الفحص المعتمدة لطول وملاءمة العنوان.

* **تعليمات الوكيل التقنية:** ابنِ قاعدة بيانات محلية بداخل الكود للكلمات المحفزة والعاطفية، واجعل التحليل يظهر في ثلاثة كروت منفصلة: النتيجة الكلية من 100، تحليل الطول بالرموز، والكلمات العاطفية والقوية المكتشفة.

* **هيكل ترجمة locales/en.json المطلوب:**
"headline_analyzer": {
  "title": "Headline & Hook Analyzer",
  "desc": "Evaluates hook titles against built-in diction lists to compute visual score cards profiling emotional conversion metrics local-side.",
  "platform_target": "Target Content Platform",
  "score": "Headline Strength Overall Score",
  "analysis_tip": "Optimization Action Tips"
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 24. منسق خطوط السوشيال ميديا (Social Media Font Formatter)]

* **خيارات التحكم والـ UI/UX:** صندوق كتابة النص الإنجليزي الأساسي، يعرض أسفله شبكة من الخطوط المزخرفة والسميكة الناتجة والجاهزة للنشر، وبجانب كل خط كرت مستقل وزر "نسخ سريع" مستقل بذاته للتسهيل.

* **تعليمات الوكيل التقنية:** استخدم خرائط ومصفوفات اليونيكود البرمجية لتحويل الحروف الإنجليزية القياسية (A-Z, a-z) إلى أشكالها الرياضية والجمالية والزخرفية الفاخرة بشكل فوري أثناء عملية الكتابة.

* **هيكل ترجمة locales/en.json المطلوب:**
"font_formatter": {
  "title": "Social Media Font Styler",
  "desc": "Maps generic alphanumeric English characters onto stylized mathematical Unicode vectors instantly to format striking bio text blocks.",
  "input_placeholder": "Type or paste your English text here...",
  "copy_style": "Copy Styled Text"
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 25. عداد الحروف والحدود (Character & Limits Counter)]

* **خيارات التحكم والـ UI/UX:** صندوق النص، ولوحة إحصائيات حية تعرض: عدد الحروف بالمسافات، عدد الحروف بدون مسافات, عدد الكلمات، عدد الأسطر، ومؤشرات تقدم مرئية (Progress Bars) تتلون بالأخضر ثم الأصفر ثم الأحمر توضح مدى الاقتراب من الحد الأقصى للمنصات.

* **تعليمات الوكيل التقنية:** اربط العدادات بحدث الـ `input` للنص لضمان التحديث اللحظي الفوري لكافة الأشرطة والنسب المئوية بدون أي تأخير برمي في المتصفح.

* **هيكل ترجمة locales/en.json المطلوب:**
"char_counter": {
  "title": "Character & Limit Analytics",
  "desc": "Monitors textual metrics natively on the viewport, tracking string lengths and sizing budgets against standard network ceiling metrics.",
  "stat_chars": "Total Character Count",
  "stat_words": "Total Word Count",
  "platform_limits": "Platform Character Budgets Tracking"
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 26. مؤقت قراءة السكربت (Script Reading Timer)]

* **خيارات التحكم والـ UI/UX:** صندوق النص، وقائمة خيارات أو أزرار لتحديد سرعة إلقاء المذيع المتوقعة (إلقاء بطيء وشرح، إلقاء طبيعي متزن، أو إلقاء سريع وحماسي للإعلانات الترويجية). يعرض الوقت المقدر بخط عريض جداً.

* **تعليمات الوكيل التقنية:** اضبط الحسابات الرياضية: الإلقاء البطيء (110 كلمة/دقيقة)، الطبيعي (140 كلمة/دقيقة)، السريع (180 كلمة/دقيقة)، وقم بعمل فلترة واحتساب الحجم وعرض الوقت بصيغة واضحة للمستخدم.

* **هيكل ترجمة locales/en.json المطلوب:**
"script_timer": {
  "title": "Script Reading Time Estimator",
  "desc": "Converts string item word arrays mathematically to estimate audio narration runtimes based on pre-calibrated verbal cadence options.",
  "pacing_mode": "Speech Pacing Delivery Speed",
  "pacing_slow": "Slow & Educational Pacing",
  "pacing_normal": "Natural / Balanced Pacing",
  "pacing_fast": "Fast & Energetic Pacing (Ads)",
  "result_time": "Estimated Content Video Duration"
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 27. فاحص الكلمات المحظورة (Banned Words Checker)]

* **خيارات التحكم والـ UI/UX:** صندوق لصق السكربت، خيارات الفحص بناءً على نوع سياسة المنصة عبر مربعات اختيار (فحص حظر خوارزميات TikTok، فحص شروط تحقيق الأرباح لليوتيوب Adsense)، مع زر "تعديل وتعمية تلقائي للكلمات المحظورة" المستهدفة بنقاط أو رموز (مثال: ح*ظر).

* **تعليمات الوكيل التقنية:** استخدم مصفوفة كلمات محظورة مدمجة محلياً، وقم بعمل استبدال (Replace) عبر Regex للكلمات المكتشفة مع تظليلها باللون الأصفر الفاتح بداخل الواجهة.

* **هيكل ترجمة locales/en.json المطلوب:**
"banned_checker": {
  "title": "Banned Words & Shadowban Checker",
  "desc": "Runs programmatic array scanning checks using local expressions to flag risk keywords that might trigger monetization censorship.",
  "policy_tiktok": "TikTok Algorithm Guard Check",
  "policy_adsense": "YouTube Monetization Filter Check",
  "obfuscate_btn": "Auto-Sanitize Banned Words (Censor)",
  "found_words": "Banned words detected in script"
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 28. منظف الوسوم والهاشتاجات (Hashtag Cleaner & Extractor)]

* **خيارات التحكم والـ UI/UX:** صندوق النص المليء بالهاشتاجات العشوائية، خيارات التنسيق عبر أزرار: ترتيب أبجدي، حذف الهاشتاجات المكررة، وتحويل المسافات لشرطة سفلية لتوحيد صياغة الهاشتاغ، مع خيار طريقة العرض (سطر واحد ممتد، أو كل هاشتاغ في سطر منفصل).

* **تعليمات الوكيل التقنية:** مرر الكلمات المستخرجة بـ Regex على كائن `new Set()` لتصفية التكرارات والهاشتاغات الزائدة محلياً وفورياً داخل المتصفح.

* **هيكل ترجمة locales/en.json المطلوب:**
"hashtag_cleaner": {
  "title": "Hashtag Extractor & Cleaner",
  "desc": "Scrubs block copy metadata to isolate hashtags, executing deduplication maps and lexical spacing rules locally in the client.",
  "clean_options": "Hashtag Formatting Rules",
  "remove_duplicates": "Remove Duplicate Hashtags",
  "alphabetical": "Sort Alphabetically (A-Z)",
  "layout_single_line": "Single Line Continuous Layout",
  "layout_multi_line": "Multiple Lines Split Layout"
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 29. قاموس الإيموجي السريع (Quick Emoji Dictionary)]

* **خيارات التحكم والـ UI/UX:** شريط بحث ذكي للبحث عن المعنى أو الوسم، تبويبات تصنيف علوية جاهزة (إيموجيات حماسية وصناعة محتوى، إيموجيات توجيهية وأسهم، وجوه ومشاعر)، مع زر لتفعيل "النسخ الفوري بمجرد الضغط" أو تفعيل التجميع (تصطف في شريط علوي ثم نسخها معاً).

* **تعليمات الوكيل التقنية:** قم بتخزين كائن JSON محلياً يحتوي على أشهر 300 إيموجي مستخدم في السوشيال ميديا مع وسوم الكلمات المفتاحية باللغتين العربية والإنجليزية لسرعة الفلترة والتحميل.

* **هيكل ترجمة locales/en.json المطلوب:**
"emoji_dictionary": {
  "title": "Creator Emoji Strategy Dictionary",
  "desc": "An embedded dictionary indexing viral emoji iconography alongside keyword lookup search inputs to rapidly collect stylistic assets.",
  "search_placeholder": "Search emoji (e.g., fire, viral, arrow)...",
  "tab_viral": "Viral Content Emojis",
  "tab_arrows": "Pointers & Signals Emojis",
  "mode_instant": "Enable Instant Copy on Click"
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 30. منظف الروابط وأكواد التتبع (URL Cleaner)]

* **خيارات التحكم والـ UI/UX:** حقل لصق الرابط الطويل، مربعات اختيار لتحديد ما يرغب المستخدم في حذفه: (حذف معاملات التتبع الإعلاني UTM، حذف تتبع فيسبوك fbclid، حذف أكواد الصفحات المنسوخة من مشاركة التطبيقات)، مع زر لمعاينة الرابط النظيف قبل نسخه.

* **تعليمات الوكيل التقنية:** استخدم كائن `URL` المدمج في المتصفح لفرز واستئصال الـ `URLSearchParams` غير المرغوبة وإعادة تركيب الرابط النظيف فورا وبأمان محلي كامل.

* **هيكل ترجمة locales/en.json المطلوب:**
"url_cleaner": {
  "title": "URL Tracking Parameter Cleaner",
  "desc": "Instantiates browser URL schemas to surgically strip ugly analytics trackers and referral token strings from pasted external links.",
  "strip_utm": "Strip Google UTM Tracking Tokens",
  "strip_fb": "Strip Facebook Analytics Tokens",
  "clean_url_btn": "Purify & Clean Link Now"
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 31. محرر ومحول ماركداون (Markdown Editor & Previewer)]

* **خيارات التحكم والـ UI/UX:** شاشة منقسمة عمودياً أو أفقياً (نصف لمحرر كود الماركداون، ونصف لمعاينة مرئية منسقة بالكامل)، أزرار تحكم علوية سريعة لحقن الأكواد (زر إضافة عنوان، زر إضافة جدول، زر إضافة رابط)، مع زر لتصدير الكود الناتج كملف `.html` مستقل.

* **تعليمات الوكيل التقنية:** استدِ مكتبة `marked.js` عبر CDN آمن واربط حدث الكتابة بالتحويل الفوري وحقن الـ innerHTML في قسم المعاينة الحية بدون تأخير.

* **هيكل ترجمة locales/en.json المطلوب:**
"markdown_editor": {
  "title": "Markdown Editor & Live Previewer",
  "desc": "Renders formatted hyper-text documentation interactively from syntax text strings via high-performance inline markdown parsers.",
  "preview_pane": "Live Preview Render",
  "toolbar_header": "Insert Markdown Header",
  "export_html": "Download Ready HTML File"
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 32. مولد نصوص الحشو العربية (Arabic Lorem Ipsum)]

* **خيارات التحكم والـ UI/UX:** حقل رقمي لتحديد العدد المطلوب، وبجواره أزرار اختيار نوع الوحدة (كلمة، جملة، فقرة كاملة)، وقائمة منسدلة لاختيار طابع النص (نص عربي فصيح قديم للشعر والخطوط الكلاسيكية، أو نص عربي عصري ومبسط للتصاميم التقنية والمواقع).

* **تعليمات الوكيل التقنية:** خزن نمطين مختلفين من المصفوفات النصية الموزونة، وقم بإنشاء دالة توليد عشوائية مكررة تعيد الحجم الدقيق الذي طلبه صانع المحتوى أو المصمم محلياً.

* **هيكل ترجمة locales/en.json المطلوب:**
"lorem_ipsum": {
  "title": "Arabic Lorem Ipsum Generator",
  "desc": "Generates arbitrary blocks of stylized placeholder Arabic prose based on classic linguistic forms or modern technical layout text configurations.",
  "unit_type": "Generation Unit Model",
  "unit_word": "Words Count",
  "unit_sentence": "Sentences Count",
  "unit_paragraph": "Paragraphs Count",
  "style_mode": "Text Linguistic Style Type",
  "style_classic": "Classical Traditional Arabic",
  "style_modern": "Modern Technology Style Arabic",
  "gen_btn": "Generate Text Placeholder Now"
}

---

### 📑 قسـم 4: أدوات الإنتاجية والأرباح والمسابقات (4 أدوات)

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 33. صانع صفحة الروابط الموحدة (Link-in-Bio Builder)]

* **خيارات التحكم والـ UI/UX:** زر ديناميكي ومريح "أضف رابط جديد" ينشئ حقلي (اسم الزر، والرابط)، لوحة لاختيار المظهر تشمل: أزرار دائرية، أزرار حادة الحواف، خلفية بلون واحد، أو خلفية بتدرج لوني نيون (Gradient)، وحقول لإضافة روابط السوشيال ميديا الرسمية لتظهر كأيقونات متناسقة أسفل الصفحة.

* **تعليمات الوكيل التقنية:** برمج دالة تقوم بجمع هذه البيانات وصياغتها داخل قالب نصي لصفحة HTML متكاملة ومتجاوبة، وتحميلها للمستخدم كملف مستقل باسم `index.html` بضغطة زر.

* **هيكل ترجمة locales/en.json المطلوب:**
"link_builder": {
  "title": "Link-in-Bio Page Builder Platform",
  "desc": "Assembles modern aesthetic link trees inside client sessions, exporting standalone responsive index.html landing page files on demand.",
  "add_link": "Add New Dynamic Link Button",
  "link_title_placeholder": "Button Label Title",
  "link_url_placeholder": "Target Redirect URL",
  "theme_select": "Background Design Theme Style",
  "export_page": "Download My Bio Landing Page (HTML)"
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 34. منظم أصول الميديا والمشاريع (Media Assets Organizer)]

* **خيارات التحكم والـ UI/UX:** تبويبات مقسمة بذكاء؛ تبويب "أكواد ألواني": لإضافة وحفظ كروت الألوان الخاصة بهوية القناة، تبويب "نصوصي الثابتة": لحفظ الكليشيهات المتكررة (روابط الدعم، هاشتاغات القناة الثابتة)، وزر "تصدير نسخة احتياطية Backup" لتحميل الأصول كملف JSON، وزر "استيراد نسخة" لرفعها على جهاز آخر.

* **تعليمات الوكيل التقنية:** استخدم الـ `localStorage` أو الـ `IndexedDB` لحفظ البيانات بشكل دائم وتلقائي فور أي عملية إدخال أو تعديل في الواجهة المحلية لمتصفح التابلت.

* **هيكل ترجمة locales/en.json المطلوب:**
"assets_organizer": {
  "title": "Media Brand Assets Organizer Dashboard",
  "desc": "A local operational database tracking active hex palette parameters and modular text descriptions with secure JSON state recovery.",
  "tab_colors": "My Brand Identity Colors",
  "tab_snippets": "Saved Template Text Snippets",
  "backup_export": "Export Config Backup (JSON)",
  "backup_import": "Import Configuration Backup File"
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 35. مستخرج الفائز في المسابقات (Giveaway Winner Extractor)]

* **خيارات التحكم والـ UI/UX:** صندوق كبير ومريح للصق الأسماء، حقل رقمي لتحديد عدد الفائزين المطلوب سحبهم، مربع اختيار لـ "حذف الأسماء المكررة تلقائياً لضمان العدالة"، وزر "بدء القرعة التفاعلية" مع خيار لتحديد مدة الأنيميشن وحركة الأسماء بالثواني قبل إعلان الفائز.

* **تعليمات الوكيل التقنية:** استخدم تأثير القرعة العشوائي لتغيير الاسم المعروض بسرعة عالية جداً عبر `setInterval` ثم إيقافها، واستدعِ تأثير القصاصات الملونة (Confetti) للاحتفال بالاسم الفائز فوراً لتبدو الأداة مبهرة وتفاعلية في الفيديوهات.

* **هيكل ترجمة locales/en.json المطلوب:**
"giveaway": {
  "title": "Giveaway Random Winner Picker",
  "desc": "Executes randomization algorithms over array list vectors to choose giveaway contest winners with eye-catching interactive UI confetti cycles.",
  "winners_count": "Target Number of Winners",
  "dedup_labels": "Remove Duplicate Names Automatically",
  "shuffle_duration": "Shuffle Animation Duration (s)",
  "draw_btn": "Draw Winner(s) Live!",
  "congratulations": "Winner Found! Congratulations to:"
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 36. حاسبات المبدعين المالية (Creators Financial Calculators)]

* **خيارات التحكم والـ UI/UX:** تبويب حاسبة اليوتيوب: حقل لإدخال المشاهدات المتوقعة، حقل لإدخال قيمة الـ RPM المتوقعة لبلده، مع قائمة منسدلة بها متوسطات الـ RPM الجاهزة لكل مجال (الطبخ، التقنية، الجيمنج) كمساعدة إرشادية. تبويب حاسبة الرعاية (Sponsorship): حقول رقمية لإدخال: عدد ساعات العمل، تكلفة المعدات والإنتاج، وهامش الربح المطلوب، ليظهر له السعر الأدنى المقترح لطلبه من الشركات الراغبة في الإعلان لديه.

* **تعليمات الوكيل التقنية:** برمج المعادلات المالية المباشرة بداخل الكود واجعل النتائج والتقارير تظهر في كروت مالية منظمة ومقروءة توضح صافي الربح والنسب والتحليلات محلياً.

* **هيكل ترجمة locales/en.json المطلوب:**
"creators_calc": {
  "title": "Creators Strategy Financial Calculators",
  "desc": "Runs rapid quantitative fiscal analysis modeling revenue potential, RPM parameters, and content creation labor costs instantly.",
  "tab_youtube": "YouTube Adsense Revenue Estimator",
  "tab_sponsor": "Brand Sponsorship Rate Calculator",
  "views_input": "Expected Monthly Views Budget",
  "rpm_input": "Estimated RPM Metric Value ($)",
  "calc_btn": "Calculate Projected Revenue",
  "result_revenue": "Estimated Net Target Earnings"
}

---

### 📑 قسـم 5: أدوات المطورين والمرافق (أداتان)

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 37. مرتب ومنسق الـ JSON / XML (JSON / XML Formatter & Minifier)]

* **خيارات التحكم والـ UI/UX:** صندوق لصق الكود غير المنظم، أزرار خيارات لتحديد مسافة التنسيق (Indent: مسافة بادئة بمقدار مسافتين 2 Spaces، أو 4 مسافات)، مع أزرار تشمل "تجميل وتنسيق الكود" وزر "ضغط وتقليص الكود (Minify)" لحذف كافة المسافات لتسريع الملفات البرمجية.

* **تعليمات الوكيل التقنية:** برمج نظام التقاط الأخطاء `try {} catch (e) {}` بحيث لو كان كود الـ JSON المرفوع به قوس ناقص أو خطأ، يظهر كرت تنبيه أحمر يوضح رقم السطر الذي يحتوي على الخطأ البرمجي لمساعدة المطور.

* **هيكل ترجمة locales/en.json المطلوب:**
"code_formatter": {
  "title": "JSON / XML Beautifier & Minifier Editor",
  "desc": "Parses and structuralizes raw data markup strings client-side to enforce strict formatting spacing loops or compress them to single lines.",
  "indent_style": "Indentation Padding Spaces",
  "beautify_btn": "Beautify & Format Code Structure",
  "minify_btn": "Minify / Compress Code Density",
  "error_invalid": "Invalid syntax discovered at structural line: "
}

بناءً على القواعد والمعايير العامة المحددة في ملف `instructions.md` بداخل المشروع (خصوصاً المعالجة المحلية 100%، التوافق التام مع اللمس والتابلت، ونظام الـ i18n الصارم)، قم الآن ببناء الأداة التالية كملف مستقل ومكتمل تماماً داخل مجلد الأدوات، مع تحديث ملفات التراجم بشكل صحيح:

[#### 38. مشفر ومفكك الـ Base64 (Base64 Encoder & Decoder)]

* **خيارات التحكم والـ UI/UX:** صندوق النص المدخل، وصندوق النص الناتج، زر "تشفير النص إلى Base64" وزر "فك تشفير كود Base64 إلى نص مقروء"، مع قسم خاص لرفع ملف صورة صغيرة (أقل من 2 ميغابايت) لتحويلها تلقائياً إلى كود Image Data-URI الجاهز للاستخدام المباشر في صفحات ومواقع الويب.

* **تعليمات الوكيل التقنية:** استخدم الدوال القياسية للمتصفح `btoa` و `atob` لمعالجة النصوص، واستخدم كائن الـ `FileReader` مدمجاً مع ميزة `readAsDataURL` لمعالجة ملفات الصور وتحويلها لكود نصي محلياً فورياً 100%.

* **هيكل ترجمة locales/en.json المطلوب:**
"base64_tool": {
  "title": "Base64 Text & Image Encoder / Decoder",
  "desc": "Converts text blocks or binary image assets into standardized web Data-URI character sets safely using native FileReader instances.",
  "encode_btn": "Encode Raw Text to Base64",
  "decode_btn": "Decode Base64 to Readable Text",
  "image_section": "Or Convert Small Image File to Data-URI String",
  "copy_uri_btn": "Copy Base64 Data-URI Content"
}

