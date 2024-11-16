



<a name="readme-top"></a>

<div align="center">
  <img src="./docs/static/img/logo.png" alt="Logo" width="200">
  <h1 align="center">OpenHands: Code Less, Make More</h1>
</div>

## شاهد الشرح الكامل على يوتيوب لـ OpenHands، أداة إدارة البرمجة بالذكاء الاصطناعي!

[![شاهد الفيديو](https://img.youtube.com/vi/N3byVQ4SLk8/0.jpg)](https://www.youtube.com/watch?v=N3byVQ4SLk8)


يُحدث OpenHands ثورة في عالم البرمجة!  فهو يُمكن من إدارة البرمجة بالكامل بواسطة الذكاء الاصطناعي، من التخطيط وكتابة الأكواد إلى تنفيذ الأوامر وتصفح الويب واستدعاء الـ APIs والبحث عن حلول في StackOverflow.  إنه "مهندس برمجيات" متكامل.


### الخطوة ١: نواة Linux (WSL2)

- **تفعيل ميزات Windows المطلوبة:**
  ```powershell
  dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart # تفعيل WSL
  dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart # تفعيل منصة الآلة الافتراضية
  ```

- **إعادة تشغيل الجهاز**

- **تثبيت WSL2 Linux kernel:** ([رابط التحميل](https://docs.microsoft.com/en-us/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package))


- **تعيين WSL2 كإصدار افتراضي:**
  ```powershell
  wsl --set-default-version 2 # تعيين الإصدار 2 من WSL كافتراضي
  ```

- **تثبيت توزيعة Linux (Ubuntu):** (من خلال Microsoft Store)

- **التحقق من التثبيت:**
  ```powershell
  wsl --version    # يعرض إصدار WSL
  wsl --list --verbose    # يعرض التوزيعات المثبتة ومعلومات عنها
  ```

- **إعداد Ubuntu:** (إنشاء اسم مستخدم وكلمة مرور)


### الخطوة ٢: تثبيت Docker Desktop

[رابط التحميل](https://www.docker.com/products/docker-desktop/)


### الخطوة ٣: تكامل Docker مع WSL2



**التحقق من التكامل:**
```bash
docker --version # يعرض إصدار Docker
docker ps # يعرض الحاويات المشغلة
```


### الخطوة ٤: تثبيت وتشغيل OpenHands

- **تحميل صورة OpenHands:**
```bash
docker pull docker.all-hands.dev/all-hands-ai/runtime:0.13-nikolaik # تحميل صورة Docker لـ OpenHands
```

- **إنشاء مجلد للمشروع (مثال: `D:\Hello World`)**

- **تحديد متغير بيئة لمسار المجلد في Ubuntu WSL:**
```bash
export WORKSPACE_BASE="/mnt/d/Hello World" # تحديد مسار مجلد المشروع
```

- **تشغيل OpenHands:**
```bash
docker run -it --rm --pull=always \ # تشغيل حاوية Docker تفاعلية، وإزالتها بعد الإغلاق، وتحديث الصورة دائمًا
-e SANDBOX_RUNTIME_CONTAINER_IMAGE=docker.all-hands.dev/all-hands-ai/runtime:0.13-nikolaik \ # تحديد صورة runtime
-e SANDBOX_USER_ID=$(id -u) \ # تحديد معرف المستخدم
-e WORKSPACE_MOUNT_PATH="$WORKSPACE_BASE" \ # تحديد مسار المجلد المشترك
-v "$WORKSPACE_BASE:/opt/workspace_base:rw" \ # ربط مجلد المشروع المحلي بمجلد داخل الحاوية مع صلاحية القراءة والكتابة
-v /var/run/docker.sock:/var/run/docker.sock \ # ربط Docker socket للسماح للحاوية بالوصول إلى Docker daemon
-p 3000:3000 \ # تعيين المنفذ 3000 للحاوية إلى المنفذ 3000 على الجهاز المضيف
-p 5000:5000 \ # تعيين المنفذ 5000 للحاوية إلى المنفذ 5000 على الجهاز المضيف
-e LOG_ALL_EVENTS=true \ # تفعيل تسجيل جميع الأحداث
--add-host host.docker.internal:host-gateway \ # إضافة host entry للوصول إلى الجهاز المضيف من داخل الحاوية
--name openhands-app \ # تسمية الحاوية
docker.all-hands.dev/all-hands-ai/openhands:0.13 # تحديد صورة OpenHands
```

- **فتح OpenHands في المتصفح:** `http://127.0.0.1:3000/`


### إعدادات LLM Provider



### استكمال مشروع بعد إعادة التشغيل



### التحكم بالمشروع من خلال Terminal منفصل:

```bash
docker exec -it openhands-app bash -c "cd '/opt/workspace_base' && bash" # الدخول إلى حاوية OpenHands وتغيير المسار إلى مجلد المشروع
python3 app.py # تشغيل تطبيق Flask (مثال)
```

لا تنسَ الاشتراك في القناة وتفعيل جرس التنبيهات! ❤️








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

Welcome to OpenHands (formerly OpenDevin), a platform for software development agents powered by AI.

OpenHands agents can do anything a human developer can: modify code, run commands, browse the web,
call APIs, and yes—even copy code snippets from StackOverflow.

Learn more at [docs.all-hands.dev](https://docs.all-hands.dev), or jump to the [Quick Start](#-quick-start).

![App screenshot](./docs/static/img/screenshot.png)

## ⚡ Quick Start

The easiest way to run OpenHands is in Docker.
See the [Installation](https://docs.all-hands.dev/modules/usage/installation) guide for
system requirements and more information.

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

You'll find OpenHands running at [http://localhost:3000](http://localhost:3000)!

Finally, you'll need a model provider and API key.
[Anthropic's Claude 3.5 Sonnet](https://www.anthropic.com/api) (`anthropic/claude-3-5-sonnet-20241022`)
works best, but you have [many options](https://docs.all-hands.dev/modules/usage/llms).

---

You can also [connect OpenHands to your local filesystem](https://docs.all-hands.dev/modules/usage/runtimes),
run OpenHands in a scriptable [headless mode](https://docs.all-hands.dev/modules/usage/how-to/headless-mode),
interact with it via a [friendly CLI](https://docs.all-hands.dev/modules/usage/how-to/cli-mode),
or run it on tagged issues with [a github action](https://github.com/All-Hands-AI/OpenHands/blob/main/openhands/resolver/README.md).

Visit [Installation](https://docs.all-hands.dev/modules/usage/installation) for more information and setup instructions.

If you want to modify the OpenHands source code, check out [Development.md](https://github.com/All-Hands-AI/OpenHands/blob/main/Development.md).

Having issues? The [Troubleshooting Guide](https://docs.all-hands.dev/modules/usage/troubleshooting) can help.

## 📖 Documentation

To learn more about the project, and for tips on using OpenHands,
**check out our [documentation](https://docs.all-hands.dev/modules/usage/getting-started)**.

There you'll find resources on how to use different LLM providers,
troubleshooting resources, and advanced configuration options.

## 🤝 How to Contribute

OpenHands is a community-driven project, and we welcome contributions from everyone.
Whether you're a developer, a researcher, or simply enthusiastic about advancing the field of
software engineering with AI, there are many ways to get involved:

- **Code Contributions:** Help us develop new agents, core functionality, the frontend and other interfaces, or sandboxing solutions.
- **Research and Evaluation:** Contribute to our understanding of LLMs in software engineering, participate in evaluating the models, or suggest improvements.
- **Feedback and Testing:** Use the OpenHands toolset, report bugs, suggest features, or provide feedback on usability.

For details, please check [CONTRIBUTING.md](./CONTRIBUTING.md).

## 🤖 Join Our Community

Whether you're a developer, a researcher, or simply enthusiastic about OpenHands, we'd love to have you in our community.
Let's make software engineering better together!

- [Slack workspace](https://join.slack.com/t/openhands-ai/shared_invite/zt-2tom0er4l-JeNUGHt_AxpEfIBstbLPiw) - Here we talk about research, architecture, and future development.
- [Discord server](https://discord.gg/ESHStjSjD4) - This is a community-run server for general discussion, questions, and feedback.

## 📈 Progress

<p align="center">
  <a href="https://star-history.com/#All-Hands-AI/OpenHands&Date">
    <img src="https://api.star-history.com/svg?repos=All-Hands-AI/OpenHands&type=Date" width="500" alt="Star History Chart">
  </a>
</p>

## 📜 License

Distributed under the MIT License. See [`LICENSE`](./LICENSE) for more information.

## 🙏 Acknowledgements

OpenHands is built by a large number of contributors, and every contribution is greatly appreciated! We also build upon other open source projects, and we are deeply thankful for their work.

For a list of open source projects and licenses used in OpenHands, please see our [CREDITS.md](./CREDITS.md) file.

## 📚 Cite

```
@misc{openhands,
      title={{OpenHands: An Open Platform for AI Software Developers as Generalist Agents}},
      author={Xingyao Wang and Boxuan Li and Yufan Song and Frank F. Xu and Xiangru Tang and Mingchen Zhuge and Jiayi Pan and Yueqi Song and Bowen Li and Jaskirat Singh and Hoang H. Tran and Fuqiang Li and Ren Ma and Mingzhang Zheng and Bill Qian and Yanjun Shao and Niklas Muennighoff and Yizhe Zhang and Binyuan Hui and Junyang Lin and Robert Brennan and Hao Peng and Heng Ji and Graham Neubig},
      year={2024},
      eprint={2407.16741},
      archivePrefix={arXiv},
      primaryClass={cs.SE},
      url={https://arxiv.org/abs/2407.16741},
}
```
