<a name="readme-top"></a>

<div align="center">
  <img src="./docs/static/img/logo.png" alt="Logo" width="200">
  <h1 align="center">OpenHands: Code Less, Make More</h1>
</div>



يُحدث OpenHands ثورة في عالم البرمجة!  فهو يُمكن من إدارة البرمجة بالكامل بواسطة الذكاء الاصطناعي، من التخطيط وكتابة الأكواد إلى تنفيذ الأوامر وتصفح الويب واستدعاء الـ APIs والبحث عن حلول في StackOverflow.  إنه "مهندس برمجيات" متكامل.

## شاهد الشرح الكامل على يوتيوب لـ OpenHands، أداة إدارة البرمجة بالذكاء الاصطناعي!

[![شاهد الفيديو](https://img.youtube.com/vi/N3byVQ4SLk8/0.jpg)](https://www.youtube.com/watch?v=N3byVQ4SLk8)

### الخطوة ١: نواة Linux (WSL2)

- **تفعيل ميزات Windows المطلوبة:**
```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```
  -  `dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart` : يُفعّل WSL.
  -  `dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart` : يُفعّل منصة الآلة الافتراضية.

- **إعادة تشغيل الجهاز**

- **تثبيت WSL2 Linux kernel:** ([رابط التحميل](https://docs.microsoft.com/en-us/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package))


- **تعيين WSL2 كإصدار افتراضي:**
```powershell
wsl --set-default-version 2
```
  -  `wsl --set-default-version 2`: يُعيّن الإصدار 2 من WSL كافتراضي.

- **تثبيت توزيعة Linux (Ubuntu):** (من خلال Microsoft Store)

- **التحقق من التثبيت:**
```powershell
wsl --version
wsl --list --verbose
```
  - `wsl --version`: يعرض إصدار WSL.
  - `wsl --list --verbose`: يعرض التوزيعات المثبتة ومعلومات عنها.


- **إعداد Ubuntu:** (إنشاء اسم مستخدم وكلمة مرور)


### الخطوة ٢: تثبيت Docker Desktop

[رابط التحميل](https://www.docker.com/products/docker-desktop/)


### الخطوة ٣: تكامل Docker مع WSL2



**التحقق من التكامل:**
```bash
docker --version
docker ps
```
  - `docker --version`: يعرض إصدار Docker.
  - `docker ps`: يعرض الحاويات المشغلة.


### الخطوة ٤: تثبيت وتشغيل OpenHands

- **تحميل صورة OpenHands:**
```bash
docker pull docker.all-hands.dev/all-hands-ai/runtime:0.14-nikolaik
```
  - يقوم هذا الأمر بتحميل أحدث صورة  Docker لـ OpenHands (0.14-nikolaik).


- **إنشاء مجلد للمشروع (مثال: `D:\Hello World`)**

- **تحديد متغير بيئة لمسار المجلد في Ubuntu WSL:**
```bash
export WORKSPACE_BASE="/mnt/d/Hello World"
```
  -  `export WORKSPACE_BASE="/mnt/d/Hello World"`: يُحدد مسار مجلد المشروع داخل WSL.  تأكد من تغيير المسار إلى المسار الصحيح لمجلد مشروعك.

- **تشغيل OpenHands:**
```bash
docker run -it --pull=always \
    -e SANDBOX_RUNTIME_CONTAINER_IMAGE=docker.all-hands.dev/all-hands-ai/runtime:0.14-nikolaik \
    -e LOG_ALL_EVENTS=true \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -p 3000:3000 \
    --add-host host.docker.internal:host-gateway \
    --name openhands-app \
    docker.all-hands.dev/all-hands-ai/openhands:0.14
```
  -  `docker run ...`:  يشغّل حاوية Docker لتطبيق OpenHands.  لاحظ استخدام `--pull=always`  للتأكد من  استخدام أحدث صورة.


- **فتح OpenHands في المتصفح:** `http://127.0.0.1:3000/`




### التحكم بالمشروع من خلال Terminal منفصل:

```bash
docker exec -it openhands-app bash -c "cd '/opt/workspace_base' && bash"
```
  - `docker exec -it openhands-app bash -c "cd '/opt/workspace_base' && bash"`:  يسمح بالدخول إلى حاوية OpenHands  وتنفيذ الأوامر داخلها.  يُغير المسار إلى `/opt/workspace_base`  الذي يُمثل مجلد مشروعك داخل الحاوية.  يمكنك بعدها تشغيل الأوامر اللازمة  مثل  `python3 app.py`.


لا تنسَ الاشتراك في القناة وتفعيل جرس التنبيهات! ❤️




## التوثيق الرسمي من ترجمة مجتمع بايثون العربي:

<div align="center">
  <a href="https://github.com/All-Hands-AI/OpenHands/graphs/contributors"><img src="https://img.shields.io/github/contributors/All-Hands-AI/OpenHands?style=for-the-badge&color=blue" alt="Contributors"></a>
  <a href="https://github.com/All-Hands-AI/OpenHands/stargazers"><img src="https://img.shields.io/github/stars/All-Hands-AI/OpenHands?style=for-the-badge&color=blue" alt="Stargazers"></a>
  <a href="https://codecov.io/github/All-Hands-AI/OpenHands?branch=main"><img alt="CodeCov" src="https://img.shields.io/codecov/c/github/All-Hands-AI/OpenHands?style=for-the-badge&color=blue"></a>
  <a href="https://github.com/All-Hands-AI/OpenHands/blob/main/LICENSE"><img src="https://img.shields.io/github/license/All-Hands-AI/OpenHands?style=for-the-badge&color=blue" alt="MIT License"></a>
  <br/>
  <a href="https://join.slack.com/t/openhands-ai/shared_invite/zt-2tom0er4l-JeNUGHt_AxpEfIBstbLPiw"><img src="https://img.shields.io/badge/Slack-Join%20Us-red?logo=slack&logoColor=white&style=for-the-badge" alt="Join our Slack community"></a>
  <a href="https://discord.gg/ESHStjSjD4"><img src="https://img.shields.io/badge/Discord-Join%20Us-purple?logo=discord&logoColor=white&style=for-the-badge" alt="Join our Discord community"></a>
  <a href="https://github.com/All-Hands-AI/OpenHands/blob/main/CREDITS.md"><img src="https://img.shields.io/badge/Project-Credits-blue?style=for-the-badge&color=FFE165&logo=github&logoColor=white" alt="Credits"></a>
  <br/>
  <a href="https://docs.all-hands.dev/modules/usage/getting-started"><img src="https://img.shields.io/badge/Documentation-000?logo=googledocs&logoColor=FFE165&style=for-the-badge" alt="Check out the documentation"></a>
  <a href="https://arxiv.org/abs/2407.16741"><img src="https://img.shields.io/badge/Paper%20on%20Arxiv-000?logoColor=FFE165&logo=arxiv&style=for-the-badge" alt="Paper on Arxiv"></a>
  <a href="https://huggingface.co/spaces/OpenHands/evaluation"><img src="https://img.shields.io/badge/Benchmark%20score-000?logoColor=FFE165&logo=huggingface&style=for-the-badge" alt="Evaluation Benchmark Score"></a>
  <hr>
</div>

مرحبًا بكم في OpenHands (المعروف سابقًا باسم OpenDevin)، وهي منصة لعوامل تطوير البرمجيات مدعومة بالذكاء الاصطناعي.

يمكن لعوامل OpenHands القيام بأي شيء يمكن لمطور بشري القيام به: تعديل التعليمات البرمجية، وتشغيل الأوامر، وتصفح الويب، واستدعاء واجهات برمجة التطبيقات، وحتى نسخ مقاطع التعليمات البرمجية من StackOverflow.

تعرف على المزيد على [docs.all-hands.dev](https://docs.all-hands.dev)، أو انتقل إلى [البدء السريع](#-البدء-السريع).

![لقطة شاشة للتطبيق](./docs/static/img/screenshot.png)

## ⚡ البدء السريع

أسهل طريقة لتشغيل OpenHands هي باستخدام Docker.
راجع دليل [التثبيت](https://docs.all-hands.dev/modules/usage/installation) لمعرفة متطلبات النظام ومزيد من المعلومات.

```bash
docker pull docker.all-hands.dev/all-hands-ai/runtime:0.14-nikolaik

docker run -it --pull=always \
    -e SANDBOX_RUNTIME_CONTAINER_IMAGE=docker.all-hands.dev/all-hands-ai/runtime:0.14-nikolaik \
    -e LOG_ALL_EVENTS=true \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -p 3000:3000 \
    --add-host host.docker.internal:host-gateway \
    --name openhands-app \
    docker.all-hands.dev/all-hands-ai/openhands:0.14
```

ستجد OpenHands قيد التشغيل على [http://localhost:3000](http://localhost:3000)!

أخيرًا، ستحتاج إلى موفر نموذج ومفتاح API.
يعمل [Anthropic's Claude 3.5 Sonnet](https://www.anthropic.com/api) (`anthropic/claude-3-5-sonnet-20241022`) بشكل أفضل، ولكن لديك [العديد من الخيارات](https://docs.all-hands.dev/modules/usage/llms).

---

يمكنك أيضًا [ربط OpenHands بنظام الملفات المحلي](https://docs.all-hands.dev/modules/usage/runtimes)، وتشغيل OpenHands في [وضع بدون رأس](https://docs.all-hands.dev/modules/usage/how-to/headless-mode) قابل للبرمجة، والتفاعل معه عبر [واجهة سطر أوامر سهلة](https://docs.all-hands.dev/modules/usage/how-to/cli-mode)، أو تشغيله على المشكلات الموسومة باستخدام [إجراء github](https://github.com/All-Hands-AI/OpenHands/blob/main/openhands/resolver/README.md).

تفضل بزيارة [التثبيت](https://docs.all-hands.dev/modules/usage/installation) لمزيد من المعلومات وتعليمات الإعداد.

إذا كنت ترغب في تعديل التعليمات البرمجية المصدر لـ OpenHands، فراجع [Development.md](https://github.com/All-Hands-AI/OpenHands/blob/main/Development.md).

هل تواجه مشكلات؟ يمكن أن يساعدك [دليل استكشاف الأخطاء وإصلاحها](https://docs.all-hands.dev/modules/usage/troubleshooting).


## 📖 التوثيق

لمعرفة المزيد عن المشروع، وللحصول على نصائح حول استخدام OpenHands، **راجع [التوثيق](https://docs.all-hands.dev/modules/usage/getting-started)**.

ستجد هناك موارد حول كيفية استخدام مختلف موفري نماذج اللغات الكبيرة، وموارد استكشاف الأخطاء وإصلاحها، وخيارات التكوين المتقدمة.


## 🤝 كيفية المساهمة

OpenHands هو مشروع قائم على المجتمع، ونرحب بمساهمات الجميع. سواء كنت مطورًا أو باحثًا أو متحمسًا ببساطة لتطوير مجال هندسة البرمجيات بالذكاء الاصطناعي، فهناك العديد من الطرق للمشاركة:

- **مساهمات التعليمات البرمجية:** ساعدنا في تطوير عوامل جديدة، أو وظائف أساسية، أو واجهة المستخدم الأمامية والواجهات الأخرى، أو حلول وضع الحماية.
- **البحث والتقييم:** ساهم في فهمنا لنماذج اللغات الكبيرة في هندسة البرمجيات، وشارك في تقييم النماذج، أو اقترح تحسينات.
- **الملاحظات والاختبار:** استخدم مجموعة أدوات OpenHands، وأبلغ عن الأخطاء، واقترح ميزات، أو قدم ملاحظات حول سهولة الاستخدام.

للحصول على التفاصيل، يرجى مراجعة [CONTRIBUTING.md](./CONTRIBUTING.md).


## 🤖 انضم إلى مجتمعنا

سواء كنت مطورًا أو باحثًا أو متحمسًا ببساطة لـ OpenHands، يسعدنا انضمامك إلى مجتمعنا. لنجعل هندسة البرمجيات أفضل معًا!

- [مساحة عمل Slack](https://join.slack.com/t/openhands-ai/shared_invite/zt-2tom0er4l-JeNUGHt_AxpEfIBstbLPiw) - هنا نتحدث عن البحث والهندسة المعمارية والتطوير المستقبلي.
- [خادم Discord](https://discord.gg/ESHStjSjD4) - هذا خادم يديره المجتمع للمناقشة العامة والأسئلة والملاحظات.


## 📈 التقدم

<p align="center">
  <a href="https://star-history.com/#All-Hands-AI/OpenHands&Date">
    <img src="https://api.star-history.com/svg?repos=All-Hands-AI/OpenHands&type=Date" width="500" alt="مخطط تاريخ النجوم">
  </a>
</p>


## 📜 الترخيص

موزع بموجب ترخيص MIT. راجع [`LICENSE`](./LICENSE) لمزيد من المعلومات.


## 🙏 شكر وتقدير

تم بناء OpenHands بواسطة عدد كبير من المساهمين، ويتم تقدير كل مساهمة بشكل كبير! كما أننا نبني على مشاريع مفتوحة المصدر أخرى، ونحن ممتنون للغاية لعملهم.

للحصول على قائمة بمشاريع المصادر المفتوحة والتراخيص المستخدمة في OpenHands، يرجى مراجعة ملف [CREDITS.md](./CREDITS.md).


## 📚 الاستشهاد

```
@misc{openhands,
      title={{OpenHands: منصة مفتوحة لمطوري برامج الذكاء الاصطناعي كعوامل عامة}},
      author={Xingyao Wang and Boxuan Li and Yufan Song and Frank F. Xu and Xiangru Tang and Mingchen Zhuge and Jiayi Pan and Yueqi Song and Bowen Li and Jaskirat Singh and Hoang H. Tran and Fuqiang Li and Ren Ma and Mingzhang Zheng and Bill Qian and Yanjun Shao and Niklas Muennighoff and Yizhe Zhang and Binyuan Hui and Junyang Lin and Robert Brennan and Hao Peng and Heng Ji and Graham Neubig},
      year={2024},
      eprint={2407.16741},
      archivePrefix={arXiv},
      primaryClass={cs.SE},
      url={https://arxiv.org/abs/2407.16741},
}
```






