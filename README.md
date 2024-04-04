
Homeworks
Homeworks
Homework #1
YAML va JSON parsing

    YAML bilan ishlashda kerak bo'ladigan yq utilitasini install qiling. Ubuntu uchun quyidagi commanda bilan:

    ​​​​sudo wget https://github.com/mikefarah/yq/releases/latest/download/yq_linux_amd64 -O /usr/bin/yq && sudo chmod +x /usr/bin/yq

    Boshqa Linux distrolar uchun installation page ga ko'rsatilgan etaplar bilan ustanovka qiling.
    Link: https://github.com/mikefarah/yq#install

    example.yaml degan YAML faylni quyidagi data bilan yarating:

    ​​​​---
    ​​​​# Hashtag (#) belgisini qator boshiga qo'yish o'sha liniyani
    ​​​​# comment ga aylantiradi va bu parser (YAML faylni analiz qiladigan
    ​​​​# componenta) tomonidan ignarirovat qilinadi.
    ​​​​team: devopsUz
    ​​​​domain:
    ​​​​ - devops
    ​​​​ - devsecops
    ​​​​ - kubernetes
    ​​​​tutorial:
    ​​​​  - yaml:
    ​​​​      name: "YAML Ain't Markup Language"
    ​​​​      type: fast
    ​​​​      born: 2006
    ​​​​      extension:
    ​​​​         - .yaml
    ​​​​         - .yml
    ​​​​  - json:
    ​​​​      name: JavaScript Object Notation
    ​​​​      type: fast
    ​​​​      born: 2002
    ​​​​      extension: .json
    ​​​​  - xml:
    ​​​​      name: Extensible Markup Language
    ​​​​      type: slow
    ​​​​      born: 1996
    ​​​​      extension: .xml
    ​​​​published: true

    yq tool orqali example.yaml faylni YAML formatdan JSON formatga o'tkazing:

    ​​​​yq -o=json example.yaml --prettyPrint > example.json

    -o=json: natijani JSON ga o'girib ber

    >: yq convert qilgan natijani example.json degan faylga yuborish, ya'ni yozish.

    --prettyPrint: YAML dan JSON ga yoki teskarisini amalga oshirganda format ham qil degani. O'rniga -P flag ham ishlatishi mumkin. Misol uchun, format qilingan JSON ni ko'rishi (sizda ham shunaqa ko'rinishda bo'lishi kerak).

    ​​​​{
    ​​​​  "teams": "devopsUz",
    ​​​​  "domain": [
    ​​​​    "devops",
    ​​​​    "devsecops"
    ​​​​  ]
    ​​​​}

    format qilinganmagan JSON ni ko'rishi:

    ​​​​{"teams":"devopsUz","domain":["devops","devsecops"]}

    yq sozdat qilgan example.json ni ko'rinishi

    ​​​​{
    ​​​​  "team": "devopsUz",
    ​​​​  "domain": [
    ​​​​    "devops",
    ​​​​    "devsecops",
    ​​​​    "kubernetes"
    ​​​​  ],
    ​​​​  "tutorial": [
    ​​​​    {
    ​​​​      "yaml": {
    ​​​​        "name": "YAML Ain't Markup Language",
    ​​​​        "type": "fast",
    ​​​​        "born": 2006,
    ​​​​        "extension": [
    ​​​​          ".yaml",
    ​​​​          ".yml"
    ​​​​        ]
    ​​​​      }
    ​​​​    },
    ​​​​    {
    ​​​​      "json": {
    ​​​​        "name": "JavaScript Object Notation",
    ​​​​        "type": "fast",
    ​​​​        "born": 2002,
    ​​​​        "extension": ".json"
    ​​​​      }
    ​​​​    },
    ​​​​    {
    ​​​​      "xml": {
    ​​​​        "name": "Extensible Markup Language",
    ​​​​        "type": "slow",
    ​​​​        "born": 1996,
    ​​​​        "extension": ".xml"
    ​​​​      }
    ​​​​    }
    ​​​​  ],
    ​​​​  "published": true
    ​​​​}

    yq tool orqali example.json faylni JSON formatdan YAML formatga o’tkazing va natijasini converted_example.yaml ga yozing.

    ​​​​cat example.json | yq -P - > converted_example.yaml

    cat: - example.json ni terminalga print qilish uchun ishlatilgan

    |: pipe belgisi, cat dan chiqgan natijani olib yq ga uzatish uchun ishlatilyapti. Yani cat bizga example.json ni ichidagi data ni print qilib beradi, pipe eas o'sha natijani olib yq ga input qilib beradi.

    -P: yuqoridagi --prettyPrint bilan bir xil vazifani bajaradi.

YAML va JSON field ga access qilish

YAML ham JSON formatdagi data tree shaklida tuzilgan, boshqacha aytganda matryoshkaday. Yani ichma-ich bo'lishi mumkin. Misol uchun:

ism: Farruh
yoshi: 25
# manziliga kelganda, manzilni qiymati ber nechta qiymatlardan
# iborat, o'shanig uchun qo'shimcha space tashab ketyapmiz. Yani
# manzilni pastidan emas, balkim o'ngga bitta tab tashab yozyapmiz.
manzili:
    kocha: beruniy
    raqami: 15
    mahalla: kimyogarlar

Bu holatda, ko'cha, raqami, mahalla degan fieldlar manzili field ga tegishli. Ya'ni manzili degan field ni qiymati o'sha 3 ta field. Boshqa xolatda, masalan ism degan field ni qiymati shunchaki Farruh ga teng. Bu degani, ko'chani nomini bilmoqchi bo'lsak birinchi manzili field ga murojat qilamiz va undan keyin ko'cha field ga.

    resume.yaml degan fayl ni quyidagi data bilan yarating va mahalla nomini hamda yosh ni terminalga print qiling

    ​​​​---
    ​​​​ism: Farruh
    ​​​​yosh: 25
    ​​​​manzil:
    ​​​​  kocha: beruniy
    ​​​​  raqami: 15
    ​​​​  mahalla: kimyogarlar
    ​​​​malumot: oliy
    ​​​​mehnatFaoliyati:
    ​​​​- korxona: startUp
    ​​​​  lavozim: devops engineer
    ​​​​  davomiyligi: 3
    ​​​​  manzil: Toshkent
    ​​​​- korxon: Net
    ​​​​  lavozim: Lead engineer
    ​​​​  davomiyligi: 5
    ​​​​  manzil: Toshkent
    ​​​​- korxon: Google
    ​​​​  lavozim: Architect
    ​​​​  davomiyligi: 1
    ​​​​  manzil: Seattle
    ​​​​qisqachaMalumot: |
    ​​​​  Bu tekstni yozishimdan maqsad, mana shunaqa uzun, bir nechta qatorli string text
    ​​​​  qanday qilib yozilishini ko'rsatmoqchi edim. Agar oddiy/qisqa string bo'lganda edi
    ​​​​  shunchaki qisqachaMalumot: abc deb yozsak bo'lardi. Ammo bu holatda abc emas uzun
    ​​​​  tekst o'sha uchun | (pipe) belgisni ishlatyapmiz va keyingi qatordan yozib boshladik.
    ​​​​  Salom so'zi qayerdan boshlanganiga ham etibor bering. qisqachaMalumot ni tagidan
    ​​​​  emas, indentation (yani o'ngga surib) yozyapmiz.

    ​​​​# yosh top level da bo'lgani uchun shunchaki nuqta (.) bilan access qilamiz.
    ​​​​yq '.yosh' resume.yaml
    ​​​​# natijasi: 25

    ​​​​# mahalla manzil ni ichida, o'shaning uchun birinchi manzilga murojat qilamiz va undan keyin mahallaga.
    ​​​​yq '.manzil.mahalla' resume.yaml
    ​​​​# natijasi: kimyogarlar

    resume.yaml ni resume.json ga kovertatsiya qiling.

    ​​​​yq -j resume.yaml --prettyPrint > resume.json

    resume.json quyidagi ko'rinishda bo'lishi kerak sizlarda ham:

    ​​​​{
    ​​​​  "ism": "Farruh",
    ​​​​  "yosh": 25,
    ​​​​  "manzil": {
    ​​​​    "kocha": "beruniy",
    ​​​​    "raqami": 15,
    ​​​​    "mahalla": "kimyogarlar"
    ​​​​  },
    ​​​​  "malumot": "oliy",
    ​​​​  "mehnatFaoliyati": [
    ​​​​    {
    ​​​​      "korxona": "startUp",
    ​​​​      "lavozim": "devops engineer",
    ​​​​      "davomiyligi": 3,
    ​​​​      "manzil": "Toshkent"
    ​​​​    },
    ​​​​    {
    ​​​​      "korxon": "Net",
    ​​​​      "lavozim": "Lead engineer",
    ​​​​      "davomiyligi": 5,
    ​​​​      "manzil": "Toshkent"
    ​​​​    },
    ​​​​    {
    ​​​​      "korxon": "Google",
    ​​​​      "lavozim": "Architect",
    ​​​​      "davomiyligi": 1,
    ​​​​      "manzil": "Seattle"
    ​​​​    }
    ​​​​  ],
    ​​​​  "qisqachaMalumot": "Bu tekstni yozishimdan maqsad, mana shunaqa uzun, bir nechta qatorli string text\nqanday qilib yozilishini ko'rsatmoqchi edim. Agar oddiy/qisqa string bo'lganda edi\nshunchaki qisqachaMalumot: abc deb yozsak bo'lardi. Ammo bu holatda abc emas uzun\ntekst o'sha uchun | (pipe) belgisni ishlatyapmiz va keyingi qatordan yozib boshladik.\nSalom so'zi qayerdan boshlanganiga ham etibor bering. qisqachaMalumot ni tagidan\nemas, indentation (yani o'ngga surib) yozyapmiz.\n"
    ​​​​}

    Endi yq utilita bilan YAML faylni field larini print qilgan bo'lsak, jq degan utilita bilan JSON faylni field larini terminalga print qilamiz. Agar sizda jq uje mavjud bo'lmasa, quyidagi link (https://stedolan.github.io/jq/download/) orqali ustanovka qiling. Ubuntu uchun ustanovka qilish commandasi:

    ​​​​# Ubuntu uchun
    ​​​​sudo apt-get install jq

    resume.json fayldan yosh va mahalla nomini terminalga print qiling:

    ​​​​# yosh top level da bo'lgani uchun shunchaki nuqta (.) bilan access qilamiz.
    ​​​​jq '.yosh' resume.json

    ​​​​# mahalla manzil ni ichida, o'shaning uchun birinchi manzilga murojat qilamiz va undan keyin mahallaga.
    ​​​​jq '.manzil.mahalla' resume.json

Bash scripting

    run.sh degan faylni quyidagi commandalar bilan yarating.

    ​​​​#!/bin/bash

    ​​​​# cat <<EOF > bizga faylni on the fly yaratish imkonini beradi.
    ​​​​# Yani hozirgi xolatda biz devel.yaml degan fayl ni yaratyapmiz
    ​​​​# va uni ichiga pastdagi YAML data ni yozyapmiz.
    ​​​​cat <<EOF > devel.yaml
    ​​​​---
    ​​​​ism: Farruh
    ​​​​yosh: 25
    ​​​​manzil:
    ​​​​  kocha: beruniy
    ​​​​  raqami: 15
    ​​​​  mahalla: kimyogarlar
    ​​​​malumot: oliy
    ​​​​mehnatFaoliyati:
    ​​​​- korxona: startUp
    ​​​​  lavozim: devops engineer
    ​​​​  davomiyligi: 3
    ​​​​  manzil: Toshkent
    ​​​​- korxon: Net
    ​​​​  lavozim: Lead engineer
    ​​​​  davomiyligi: 5
    ​​​​  manzil: Toshkent
    ​​​​- korxon: Google
    ​​​​  lavozim: Architect
    ​​​​  davomiyligi: 1
    ​​​​  manzil: Seattle
    ​​​​EOF

    ​​​​# bu yerda YAML faylni JSON formatga konvert qilyapmiz va natijani yangi faylga devel.json ga soxranit qilyapmiz.
    ​​​​yq -o=json devel.yaml --prettyPrint > devel.json

    ​​​​# bu yerda dasturchiYoshi va dasturchiIsmi nomli o'zgaruvchi yaratyapmiz.
    ​​​​# dasturchiIsmi ning qiymatiga devel.json fayldagi `ism` degan field ning
    ​​​​# qiymatini beryapmiz, yani Farruh.
    ​​​​# dasturchiYoshi ning qiymatiga devel.json fayldagi `yosh` degan field ning
    ​​​​# qiymatini beryapmiz, yani 25.

    ​​​​dasturchiYoshi=$(jq '.yosh' devel.json)
    ​​​​dasturchiIsmi=$(jq '.ism' devel.json)

    ​​​​
    ​​​​if [ $dasturchiYoshi -lt 25 ]; then
    ​​​​    echo $dasturchiIsmi yoshi 25 dan kichik 😎
    ​​​​elif [ $dasturchiYoshi -gt 25 ]; then
    ​​​​    echo $dasturchiIsmi yoshi 25 dan katta 😎
    ​​​​else
    ​​​​    echo $dasturchiIsmi yoshi 25 ga teng 😎
    ​​​​fi

    ​​​​# For loop misoli. Bu yerda biz 10 marta hozirgi vaqtni print
    ​​​​# qilamiz va har bir print qilganimizdan keyin 1 sekundga dasturni
    ​​​​# to'xtatamiz, ya'ni sleep qilamiz.
    ​​​​for i in {1..10}
    ​​​​do
    ​​​​  date
    ​​​​  sleep 1s
    ​​​​done

    ​​​​echo "dastur natijasi: $?"

    run.sh hozir executable emas, uni executable qilish uchun

    ​​​​chmod +x runs.sh

    komandasini ishlating

    run.sh ni run qiling

    ​​​​./run.sh

Homework #2
Git

    git utilitasi uchun o'zingizning username va elektron pochtangizni configuratsiya qilib qo'ying. Bu odata bir marta qilinadigan nastroyka, lekin qaysidir bir sababga ko'ra email yoki username ni o'zgartiqmochi bo'lsangiz yana shu komandalarni run qilsnagiz bo'ladi.

    ​​​​git config --global user.name "John Smith"
    ​​​​git config --global user.email john.smith@example.com

    git uchun nastroka qilinga username va email ni tekshiring:

    ​​​​git config --global user.name 
    ​​​​git config --global user.email

    Yangi directory yarating va unit git proyektga aylantiring (initialize qilish).

    ​​​​mkdir webapp
    ​​​​cd webapp
    ​​​​git init

    webapp/ directory(papkasi) da index.html degan faylni quyidagi HTML content bilan yarating va git status commandasi natijasini analiz qiling.

    ​​​​cat <<EOF > index.html
    ​​​​<!doctype html>
    ​​​​<html>
    ​​​​  <head>
    ​​​​    <title>This is the title of the webpage!</title>
    ​​​​  </head>
    ​​​​  <body>
    ​​​​    <p>This is an example paragraph.</p>
    ​​​​  </body>
    ​​​​</html>
    ​​​​EOF

    ​​​​git status
    ​​​​
    ​​​​# bu git status dan chiqadigan natija
    ​​​​On branch master

    ​​​​No commits yet

    ​​​​Untracked files:
    ​​​​  (use "git add <file>..." to include in what will be committed)
    ​​​​    index.htnl

    ​​​​nothing added to commit but untracked files present (use "git add" to track)

    Hozirgi paytda index.html bu working areada. Uni commit qilish uchun staging area ga o'tkazing.

    ​​​​git add index.html

    index.html staging arega o'tganiga amin bo'lish uchun, git status bilan tekshiring:

    ​​​​On branch master

    ​​​​No commits yet

    ​​​​Changes to be committed:
    ​​​​  (use "git rm --cached <file>..." to unstage)
    ​​​​    new file:   index.htnl

    Chiqgan natijani analiz qiling.

    Endi index.html ni commit qilish uchun, commit area ga o'tkazing va birinchi commit ni yarating:

    ​​​​# -m  bu yerda commit ga sarvlavha berish uchun ishtatilyapti
    ​​​​git commit -m "Add index.html for the webapp"
    ​​​​
    ​​​​[master (root-commit) e179e75] Add index.html for the webapp
    ​​​​ 1 file changed, 9 insertions(+)
    ​​​​ create mode 100644 index.htnl

    git status natijasini analiz qiling

    ​​​​$ git status
    ​​​​
    ​​​​On branch master
    ​​​​nothing to commit, working tree clean

    README.md degan faylni quyidagi tekst bilan yarating

    ​​​​cat <<EOF > README.md
    ​​​​Welcome to my webapp page. Currently it is under development!
    ​​​​EOF

    git status natijasini analiz qiling:

    ​​​​git status
    ​​​​
    ​​​​# bu git status dan chiqadigan natija
    ​​​​On branch master
    ​​​​Untracked files:
    ​​​​  (use "git add <file>..." to include in what will be committed)
    ​​​​    README.md

    ​​​​nothing added to commit but untracked files present (use "git add" to track)

    README.md faylni staging arega o'tkazing

    ​​​​git add README.md

    git status komandasi natijasini analiz qiling

    Tasavvur qiling, bazi bir sababga ko'ra biz bu fayldagi o'zgarishlardan commit yaratmoqchi emasmiz, yoki unga tayyor emasmi, yoki hali yana qo'shimcha o'zgartirish kerakligi ma'lum bo'lib qoldi va shu sababli README.md ni staging area dan working area ga qaytormoqchimiz. U uchun git restore komandasini ishlatamiz:

    ​​​​git restore --staged README.md

    Restore qilgandan keyin, yani faylni staging area dan wokring area ga o'tkazgandan keyin, git status komandasini analiz qiling va bu fayl haqiqatdan working area ga o'tganiga e'tibor bering.

    ​​​​On branch master
    ​​​​Changes not staged for commit:
    ​​​​  (use "git add <file>..." to update what will be committed)
    ​​​​  (use "git restore <file>..." to discard changes in working directory)
    ​​​​    modified:   README.md

    ​​​​no changes added to commit (use "git add" and/or "git commit -a")

    README.md faylni qaytadan working area dan staging area ga o'tkazing va undan keyin u uchun yangi bir commit yarating

    ​​​​git add README.md
    ​​​​git commit -m "Add user document"
    ​​​​
    ​​​​# git commit komandasining natijasi
    ​​​​[master 002a4ba] Add user document
    ​​​​ 1 file changed, 1 insertions(+), 0 deletions(-)
    ​​​​ create mode 100644 README.md

    Hozirgi paytda sizda ikkita commit mavjud va buni tekshirish uchun git log comandasini ishlating

    ​​​​git log
    ​​​​
    ​​​​# sizda ham shunga o'xshash natija chiqishi kerak. 
    ​​​​# Faqat commit hash yani 002a4baaa86a60fd5e40807e429e1a228871f623 va
    ​​​​# e179e75250c0af2717d85c447a6028dcb35fccbb boshqacha bo'ladi, hamda Author
    ​​​​# va date ham.
    ​​​​
    ​​​​commit 002a4baaa86a60fd5e40807e429e1a228871f623 (HEAD -> master)
    ​​​​Author: Smith, John <john.smith@example.com>
    ​​​​Date:   Mon April 10 11:15:07 2023 +0300

    ​​​​    Add user document

    ​​​​commit e179e75250c0af2717d85c447a6028dcb35fccbb
    ​​​​Author: Smith, John <john.smith@example.com>
    ​​​​Date:   Mon April 10 11:08:20 2023 +0300

    ​​​​    Add index.html for the webapp

    git log komandasi ko'rsatgan natijani analiz qiling.

Homework #3
Docker images

https://github.com/instructorUz/kubernetes-practise.git GitHub project ni fork qiling va clone qiling va lokalniy proyektni ichida biror bir branch yarating.

    Project ni docker/dockerfile/ directory ni ichida, o'zingizning GitHub usernamingiz nomi bilan directory yarating. Directory ni ko'rinishi mana shunaqa bo'lishi kerak.

    ​​​​$ kubernetes-practise$ tree -d
    ​​​​.
    ​​​​└── docker
    ​​​​    └── dockerfile
    ​​​​        └── username

    username ga ko'ching va uni ichida oddiy Hello World! degan textni print qilib beradigan hello.sh bash script yozing.

    Dockerfile yarating. Bu dockerfile da quyidagi instruksiyalarni yozing.
        Base image Ubuntu 22:04 bo'lsin.
        /app degan directory yaratilsin working directory sifatid
        hello.sh script ni kopiravat qiling container image ni ichiga
        hello.sh script ga executable permission bering.
        hello.sh ni container start bo'lganda run bo'lishi kerak.

    Yuqoridagi dockerfile asosida container image yarating va uni nomini my-docker-image deb nomlang va alpha degan tag bering.

    O'zingiz yaratgan image asosida container run qiling. Container stop bo'lgandan keyin uni o'chirib tashlang (Image ni emas, container ni!)

    Yaratilgan image ni o'zingizning container registratoringizga (Docker Hub) upload qiling. Agar Docker hub da accountingiz bo'lmasa, avval akkount oching.

    Yozilgan shell script va dockerfile ni man ko'rishim uchun https://github.com/instructorUz/kubernetes-practise.git ga o'zingizning branchingizdan pull request yuboring.

    Pull request ni nomini docker image deb qo'ying va description da upload qilingan container image ga link ni qo'shib qo'ying.

Docker networking (bridge)

    Yangi bridge network yarating va uni nomini dev-net-bridge deb qo'ying

    Network yaratilganiga amin bo'lish uchun network larni list qiling va dev-net-bridge bridge driver asosida yaratilganiga amin bo'ling.

    2 ta nginx container start qiling va
        ikklasini ham dev-net-bridge network ga ulang
        ularga nginx1 va nginx2 degan nomlar bering
        ikkalsini ham detached mode da run qiling
        nginx1 da 80-port ni oching va host ni 8001 portiga map qiling
        nginx2 da 80-port ni oching va host ni 8002 portiga map qiling

    Ikkala container ni ham IP larini toping

    Host dan turib nginx1 va nginx2 ga terminaldan curl qiling va mana bunaqa natijani ko'rishingiz kerak. Yoki browser dan tekshirib ko'ring.

    ​​​​<!DOCTYPE html>
    ​​​​<html>
    ​​​​<head>
    ​​​​<title>Welcome to nginx!</title>
    ​​​​<style>
    ​​​​html { color-scheme: light dark; }
    ​​​​body { width: 35em; margin: 0 auto;
    ​​​​font-family: Tahoma, Verdana, Arial, sans-serif; }
    ​​​​</style>
    ​​​​</head>
    ​​​​<body>
    ​​​​<h1>Welcome to nginx!</h1>
    ​​​​<p>If you see this page, the nginx web server is successfully installed and
    ​​​​working. Further configuration is required.</p>

    ​​​​<p>For online documentation and support please refer to
    ​​​​<a href="http://nginx.org/">nginx.org</a>.<br/>
    ​​​​Commercial support is available at
    ​​​​<a href="http://nginx.com/">nginx.com</a>.</p>

    ​​​​<p><em>Thank you for using nginx.</em></p>
    ​​​​</body>
    ​​​​</html>

    Container larni to'xtating va host dan o'chirib tashlang.

    Container uchun ishlatilgan image larni ham o'chirib tashlang.

    Yartilgan dev-net-bridge network ni o'chiring.

Docker networking (host)

    Yangi host network yarating va uni nomini dev-net-host deb qo'ying

    Network yaratilganiga amin bo'lish uchun network larni list qiling va dev-net-host host driver asosida yaratilganiga amin bo'ling.

    1 ta nginx container start qiling va
        dev-net-host network ga ulang
        nginx1 degan nom bering
        detached mode da run qiling

    Container ni IP sini toping

    Host dan turib nginx1 ga terminaldan curl qiling va mana bunaqa natijani ko'rishingiz kerak. Yoki browser dan tekshirib ko'ring.

    ​​​​<!DOCTYPE html>
    ​​​​<html>
    ​​​​<head>
    ​​​​<title>Welcome to nginx!</title>
    ​​​​<style>
    ​​​​html { color-scheme: light dark; }
    ​​​​body { width: 35em; margin: 0 auto;
    ​​​​font-family: Tahoma, Verdana, Arial, sans-serif; }
    ​​​​</style>
    ​​​​</head>
    ​​​​<body>
    ​​​​<h1>Welcome to nginx!</h1>
    ​​​​<p>If you see this page, the nginx web server is successfully installed and
    ​​​​working. Further configuration is required.</p>

    ​​​​<p>For online documentation and support please refer to
    ​​​​<a href="http://nginx.org/">nginx.org</a>.<br/>
    ​​​​Commercial support is available at
    ​​​​<a href="http://nginx.com/">nginx.com</a>.</p>

    ​​​​<p><em>Thank you for using nginx.</em></p>
    ​​​​</body>
    ​​​​</html>

    2-nginx container start qiling va
        dev-net-host network ga ulang
        nginx2 degan nom bering
        detached mode da run qiling

    Container ni IP sini toping

    nginx2 container run bo'lganiga amin bo'ling. Agar run bo'lmasdan stop bo'lgan bo'lsa nimaga stop bo'lganini topishga harakat qiling.

    Container larni to'xtating va host dan o'chirib tashlang.

    Container uchun ishlatilgan image larni ham o'chirib tashlang.

    Yartilgan host network ni o'chiring.

NOTE: Bu task ni GitHubdan pull request sifatida yuborish kerak emas.
Homework #4

Bularni hammasini bajarish uchun kerak bo'ladigan komandasini yozing.
Javoblarni alohida mani telegram lichkamga yoki slackdagi accountimga yuboring.
Gruppaga tashlamang!

har bir raqam ostida javob yozing. Masalan:

    yangi devel-api branch yaratib unga ko'ching
    git abc dsdsd …
    master branch ga ko'ching
    git switch …

Git

    yangi devel-api branch yaratib unga ko'ching
    master branch ga ko'ching
    test deb nomlangan branch ni o'chirib tashlang
    commit yaratib unga "Add API server" degan sarvlahva bering va commitni sign qiling
    mavjud remote larni list qiling
    yangi upstream degan remote qo'shing mana bu URL bilan https://github.com/kubernetes/kubernetes.git
    dowstream deb nomlangan remote ni o'chiring
    staging area dagi main.go faylni o'zgarishlarini qaytaring (restore qilish)
    working area dagi api.go faylni o'zgarishlarini qaytaring (restore qilish)
    https://github.com/kubernetes/kubernetes.git clone qiling
    qilingan commit ni upstream deb nomlangan remote ga test branchiga push qiling
    hozirgi git proyekti bo'lmagan proketni git proyektiga aylantiring, git ni initialize qiling
    remote ning master branchidan oxirgi o'zgarishlarni pull qiling
    lokalniy git uchun o'zingizning email addresingiz va ismingizni nastroyit qiling

Docker

    docker image build qiling va uni nomini webapp va v1alpha1 degan tag qo'ying
    docker image larni list qiling
    docker container ni list qiling
    docker volume larni list qiling
    docker network larni list qiling
    adminNet nomli bridge network yarating
    l2 nomli macvlan network yarating
    nginx container run qiling uni adminNet nomli bridge network ga hamda l2 nomli macvlan network ga ulang. container ni nomini webserver qo'ying. 80-portini host ni 8091-portiga ulang. Container ni detached modda run qiling.
    c1 nomli container ni hostdan o'chirib tashlang
    barcha image larni o'chirib tashlang
    barcha container larni o'chirib tashlang
    barcha volume larni o'chirib tashlang
    c2 nomli container run qiling va unga host dagi /etc/crio/ degan directory ni /etc/runtime/ degan directory ga mount qiling
    database nomli volume yarating va uni c3 degan container ga attach qiling
    database volume ni o'chirib tashlang
    Kernel versionni print qilib beradigan bash script yozing va uni container da run qilish uchun kerak bo'ladigan Dockerfile ni yozing. Kernel versionni bilish uchun, uname -r komandasi yetarli.
    hello-world container image ni pull qiling
    docker hub ga terminaldan autentifikatsiya qiling
    terminalda docker hub dan logout qiling

Homework #5
Docker Swarm

Bu labda siz ovoz berish applicationini docker containerlarda deploy qilasiz.
App da, Barcelona yoki Real Madridga ovoz berish mumkin. App ni arxitekturasi quyidagicha:

App ning komponentalari:

    frontend #1: App ni clientlari ovoz beradigan web portal (code python da yozilgan)
    frontend #2: Ovoz berganlarning umumiy sonini va natijalarini foizini ko'rsatish real vaqtda (Node.js da yozilgan)
    database (Postgres da)
    backend (.NET da yozilgan)
    Redis

Har bir komponenta alohida docker container sifatida run bo'ladi. Bu containerlarni bittada deploy qilish uchun siz docker compose faylni yaratishingiz kerak ba docker swarm stack yaratishingiz kerak.
Lab environment

Bu lab uchun siz https://labs.play-with-docker.com/ ni ishlating. Jami 4 ta server yarating. Bitta server docker swarm manager va qolgan 3 tasi worker sifatida bo'lsin.
Docker-compose ni yaratish

Quyida sizga docker-compose da app ni deploy to'g'ri deploy qilish uchun kerak bo'ladigan etaplar berilgan.

    compose.yaml nomli fayl yarating va unda docker-compose da yoziladigan standard field larni qo'shing
    frontend va backend nomli networklar yarating. frontend networkga biz frontend servicelarni ulaymiz. backend networkga biz backend servicelarni ulaymiz.
    db-data nomli volume yarating
    Yaratiladigan barcha servicelar faqat worker node larda run bo'lsin.
    redis nomli service yarating va uni frontend networkga ulang. Bu service uchun redis:alpine image ni ishlating.
    db nomli service yarating va uni backend networkga ulang, db-data nomli volume ni, servicening /var/lib/postgresql/data directoriyasiga mount (tiking) qiling. Bu service uchun postgres:15-alpine container image ni ishlating. 2 ta environment variable qo'shing quyidagi qiymatlar bilan

    ​​​​​​POSTGRES_USER: "postgres"
    ​​​​​​POSTGRES_PASSWORD: "postgres"

    Bu variablar postgress databse ga boshqa containerlardan access qilish uchun kerak bo'ladi.
    frontend-ovoz nomli service yarating uni frontend networkga ulang. Bu webservice va u 80-portda eshitadi. Biz bu servicega hostdan ulanish uchun, servicening 80-portini hostning 5000-portiga ulang. Bu servicening replicasini 2 ta bo'lsin. Image uchun: feruzjon/ovoz:latest image ni ishlating. E'tibor bering, bu image python da yozilgan code ni o'z ichiga oladi. Bizning maqsan docker swarm bilan ishlash bo'lgani uchun, python code ni yozish bizga kerak emas va yozilgan code ni ishlatamiz xolos.
    frontend-natija nomli service yarating uni backend networkga ulang. Bu webservice va u 80-portda eshitadi. Biz bu servicega hostdan ulanish uchun, servicening 80-portini hostning 5001-portiga ulang. Image uchun: feruzjon/natija:latest image ni ishlating.
    backend nomli service yarating va uni ham backend ham frontend networklariga ulang. Bu service ham frontend bilam ham database bilan ishlagani uchun, uni ikkala networkga ham ulash kerak. 2 ta replica bo'lsin. Image uchun feruzjon/backend:latest ni ishlating.

Swarm cluster ni yaratish

Docker lab environmentda biror bir serverda docker swarm ni initialize qiling va qolgan 3 ta server ni bu clusterga worker sifatida qo'shing.
Manager da swarm stack ni yarating bundan oldin yaratgan compose.yaml fayl orqali. Stackning nomini vote-app deb nomlang.
Tekshirish

Yangi compose-visualizer.yaml degan fayl yarating va unda visualizer serviceni yarating quyodagi content asosida.
Bu pastdagi visualizer servicening bitta kamchiligi bor, uni deploy qilishdan oldin bu kamchilikni to'g'irlang. Ya'ni, visualizer service ni manager node da run qilishni ta'minlang. Kamchilikni to'g'irlaganingizdan keyin, stack ni deploy qiling va nomini visualizer deb nomlang.

version: "3"
services:
  visualizer:
    image: dockersamples/visualizer
    ports:
    - "8080:8080"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock

Agar hammasini to'g'ri bajarilan bo'lsa, docker labdan 5000-portini ochib real ga yoki barca ga ovoz bersangiz bo'ladi. Yangi ovoz berish uchun, linkni incognitodan oching.


Visualizerga (8080 -port) ga kiring hamda visualizerdan tashqari barcha servicelar worker node larda run bo'layotganiga a'min bo'ling.
Topshirish

Bu homeworda yaratgan compose.yaml ni hamda visualizerdan ko'ringan natijani screenshot qilib uni visuazlier deb nomlang va bu ikkita faylni GitHub Pull Request sifatida jo'nating.
Homework #6
Ansible playbook creation

Bu labda siz ansible playbook orqali 2 ta serverda docker install qilishingiz kerak va ularda docker swarm cluster yaratishingiz kerak bo'ladi. Hamda bu stackda Homework5 yaratgan compose.yaml ni run qiling va ovoz berish applicationini ishga tushuring.

Yani Homework5 da siz docker lab muhitida web browserda ruchnoy swarm init, szarm join qildingiz, docker install qilmadingiz, chunki docker lab bu narsalarni bizga qilib bergan edi. Endi, bu taskda, siz infrastrukturani adminisiz deb tasavvur qiling va birinchi qilishingiz kerak bo'lgani bu 2 ta serverni kerakli holatga keltirib olish va keyin application ni deploy qilish va buning hammasini bitta playbook orqali bajaramiz.
Lab environment

Sizga 2 ta server berilgan bo'ladi. Ularning biriga ssh orqali kirib, Ansibleni install qiling. Bu server sizda ansible controlplane/manager sifatida bo'ladi. Serverlarning IP addresslar va username/passwordlari telegramdan yuboriladi.
Ansible Playbook

Ansible controlplane da vote-app degan directory yarating. Bu directoryda inventory nomli fayl yarating. Inventory faylda 2 ta gruppa yarating.

    worker nomli, bunga ikkinchi serverning IP addresini qo'shing
    servers bunga ikkala serverning ham IP addresini qo'shing

swarm.yaml nomli ansible playbook yarating. Unda, 4 ta play yozing.

    Birinchi playda ikkala serverda ham docker install qiling. Playning nomini Install Docker deb nomlang. Node lar haqida fact yig'ishni o'chirib qo'yin. Bizga bu kerak emas. Buning uchun siz inventoriydagi servers gruppasini ishlatishingiz kerak.
    Ikkinchi play da hozir turgan serverda (manager) da swarm cluster yarating, yani initialize qiling. Playning nomini Init swarm cluster deb nomlang. Docker swarm initdan chiqgan token ni token nomli o'zgaruvchiga saqlang. Buning play uchun siz localhost ishlatishingiz kerak. Swarm bilan ishlash Ansible ning docker_swarm moduleni ko'rib chiqing: https://docs.ansible.com/ansible/2.9/modules/docker_swarm_module.html. O'zgaruvchi yaratish uchun: set_fact module qo'l keladi.
    Uchinchi playda worker node ni swarm cluster ga join qiling. Bunda sizga 2-etapdagi token kerak bo'ladi. Token qiymati token nomli o'zgaruvchiga saqlangan, ya'ni siz o'sha o'zgaruvchini ishlatishingiz kerak bo'ladi. Buning play uchun siz inventoriydagi worker gruppasini ishlatishingiz kerak. Playning nomini Join nodes to swarm cluster deb nomlang.
    To'rtinchi playda swarm manager bo'lgam node da stack yarating va uning nomini vote_app deb nomlang va stack ni homework5 da yaratgan compose.yaml bo'lsin. Playning nomini Create swarm stack deb nomlang.

Takshirish

Agar hammasi to'g'ri bajarilgan bo'lsa, siz sizga berilgan serverlarning IP:5000 va IP:5001 - portlariga kirib Barcelona yoki Real Madridga ovoz berishingiz mumkin.
Topshirish

Taskni bajarib bo'lganingizdan keyin, manga ayting, man serverlarga kirib tekshirib ko'raman.
Pull request yuborish shart emas. Omad!
Homework #7
Kubernetes pods

    Kind/Minikube ni install qiling
        kind: https://kind.sigs.k8s.io/docs/user/quick-start/#installation
        minikube: https://minikube.sigs.k8s.io/docs/start/
    kubectl ni install qiling (instruksiya: https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)
    Kind/Minikube asosida 1 ta node (control-plane) li local kubernetes cluster ko'taring.
    pod.yaml fayl ni yarating, va bu faylda nginx:latest container image aossida run bo'ladigan Pod manifest ni yozing. Pod ga webapp deb nom bering. Pod ga version: v1 label ni bering. Pod ni dev namespaceda run qiling. Podning ichidagi containerga nginx deb nom bering.
    kubectl bilan dev nomli namespace yarating.
    kubectl bilan pod.yaml ni apply qiling.
    kubectl bilan dev namespace da webapp pod yaratilganini tekshiring.
    webapp pod ga exec orqali kiring va curl localhost orqali NGINX container ishlab turganiga a'min bo'ling. Agar curl comandasi bo'lmasa, uni apt update && apt install curl comandasi bilan install qiling.
    kubectl bilan webapp podni delete qiling.
    Clusterdagi barcha namespace dagi podlarni list qiling.
    Clusterdagi barcha namespace larni list qiling.
    Kind/Minikube cluster ni delete qiling.

Yaratilgan pod.yaml ni manga telegram/slack dan yuboring.
Homework #8
Podlarni Yaratish va Boshqarish

    nginx-pod deb nomlangan Kubernetes Pod yarating va uning ichida nginx konteynerini ishga tushiring.
    nginx-pod ning loglarini tekshirib, nginx serverining ishlayotganligini tekshiring.
    Podning image ni httpd:latest ga o'zgartiring.
    nginx-pod ni o'chiring va uning o'chganiga a'min bo'ling.
    Yaratilgan Pod manifestni manga yuboring.

Deployments boshqarish

    web-app nomli Deployment yarating va unda nginx:latest image bilan ishlaydigan Podning 3 ta replicasini yarating. Podlarga tier:frontend nomli label bering.
    web-app Deploymentning replicasini 3 tadan 5 taga ko'taring.
    Deploymentni nginx:1.21.1 image ni ishlatish uchun edit qiling.
    Rolling update holatini tekshirib, muvaffaqiyatli yakunlanganiga a'min bo'ling. Buning uchun, yaratilgan Pod larning image larini tekshirib chiqing.
    Yaratilgan Deployment manifestni manga yuboring.

Service bilan ishlash

    app-deployment nomli Deployment yarating va unda nginx:latest container image ni ishlating. Replica soni 2 ta bo'lsin. Podlarga tier:frontend nomli label set qiling.
    app-service nomli ClusterIP type dagi Service yarating va bu Service ni app-deployment Deployment yaratgan Podlarning 80-portiga ulang. Service ning o'ziga 9091-portni bering.
    app-service orqali cluster ichida curl yoki wget orqali NGINX serverlarga ulanishni tekshirib ko'ring. Buning uchun, minikube node ga ssh qiling (minikube ssh orqali) va curl/wget comandasi bilan app-service nomli service ning IP:9091 addresiga ulanib ko'ring.
    app-service-nodeport nomli NodePort type dagi Service yarating va bu Service ni app-deployment Deployment yaratgan Podlarning 80-portiga ulang. Service ning o'ziga 9092-portni bering va har bir kubernetes Node ning 30019-portini oching.
    Cluster dagi node larni list qiling va ularni IP larini toping. Keyin, clusterdan tashqarida, node ning IP:30019 addresiga curl qilib ko'ring.
    Yaratilgan Service manifestlarini manga yuboring.

Debug qilish

Sizga har xil manifestlar berilgan va ularda kamchiligi bor, bu kamchiliklarni topib, to'g'irlab, to'g'irlangan YAML fayallarni manga yuboring.
Deployment

Quyidagi Deployment ni apply qiling, va 2 ta nginx Pod yaratilishiga sabab bo'layotgan maummoni topid, dayploymentni fix qiling.

apiVersion: apps/v1
kind: Deployment
metadata:
  name: http
spec:
  replicas: 2 
  selector:
    matchLabels:
      env: development
  template:
    metadata:
      labels:
        env: production
    spec:
      containers:
      - name: myapp
        image: nginx:latest

Pod

Quyidagi Podni ni apply qiling, va webapp Podning ichida nima sababdan nginx hamda apache containerlarni ishga tushmayotgani toping hamda muammo to'g'irlang.

apiVersion: v1
kind: Pod
metadata:
  name: webapp
spec:
  containers:
  - name: http
    image: apache:latest
  - name: nginx
    image: nginx:latest

Pod & Service

Quyidagi Pod va Service ni apply qiling. Bu service bilan, siz kubernetes node ning IP is hamda 30077 porti orqali K8s ichidagi webapp podga curl qia olishingiz hamda natijada NGINX serverdan response olishingiz kerak. Muammoni toping, va uni to'g'irlang.

apiVersion: v1
kind: Pod
metadata:
  name: webapp
spec:
  containers:
  - name: nginx
    image: nginx:latest
---
apiVersion: v1
kind: Service
metadata:
  name: webapp-service
spec:
  type: NodePort
  selector:
    app: webapp
  ports:
  - port: 7989
    targetPort: 80
    nodePort: 30077

Homework #9
Case #1. ReplicaSet bilan ishlash. case1.yaml fayl yarating.

    1 ta worker, 1 ta controlplane dan iborat Kind cluster yarating. Yaratgan confingizni case1.yaml yozing.
    ReplicaSet obyektini yarating. NGINX pod ning 3 ta replicasini yarating. NGINX pod uchun, nginx:1.25.2 container image ni ishlating. Podlarga, app: web labelini bering. ReplicaSet ga myapp-replicaset nomini bering va bu mani manifestni case1.yaml ga save qiling.
    prod namespace kubectl orqali yarating.
    ReplicaSet ni prod namespace da yarating.
    prod namespace da 3 ta NGINX pod yaratilganini tekshiring.
    Endi sizdan NGINX webserverlarning imageni o'zgartirish so'raldi. Buning uchun, clusterdagi siz yaratgan ReplicaSet ni edit qiling (kubectl edit ... orqali) va Pod larning imageni nginx:latest ga o'zgartiring.
    prod namespace dagi NGINX podlarning image larini tekshirib ko'ring, (kubectl get pod.....-oyaml orqali) va nginx:latest ishlatilganiga a'min bo'ling. Agar image nginx:latest image ishlatilmagan bo'lsa, sabibini toping va buni case1.yaml ga yozing.
    Yaratilgan case1.yaml faylni manga yuboring.

Case #2. Deployment bilan ishlash. case2.yaml fayl yarating.

    1 ta worker, 1 ta controlplane dan iborat Kind cluster yarating. Yaratgan confingizni case2.yaml yozing.
    apache serverning 3 ta kopiyasini Deployment orqali yarating. Podlar uchun httpd:latest image ni ishlating. Podlarga, app:frontend label ni bering. Deploymentga myapp-deployment deb nom bering va bu mani manifestni case2.yaml ga save qiling
    Deployment ni default namespace da deploy qiling.
    kubectl orqali myapp-deployment Deployment yaratilganini tekshiring
    kubectl orqali Pod larni list qiling va myapp-deployment Deployment yaratgan podlarning nomlarini case2.yaml faylga save qiling
    kubectl orqali myapp-deployment Deployment obyektining to'liq ko'rinishi YAML formatda print qiling va uni case2.yaml fayl ga save qiling.
    myapp-deployment Deployment ning replicasini 3 tadan 1 taga kamaytiring
    kubectl orqali Pod larni list qiling va myapp-deployment Deployment yaratgan podlarning nomlarini case2.yaml faylga save qiling
    kubectl orqali default namespace dagi ReplicaSet larni list qiling. Agar default namespace da myapp-deployment bilan boshlanadigan ReplicaSet ko'rsangiz uni kim yaratganini topib ko'ring va fikringizni case2.yaml ga yozing.
    myapp-deployment bilan boshlanadigan ReplicaSet ni delete qiling (kubectl bilan)
    kubectl orqali default namespace dagi ReplicaSet larni list qiling va myapp-deployment bilan boshlanadigan ReplicaSet o'chganiga a'min bo'ling. O'chmagan bo'lsa yana o'chirib ko'ring. Agar o'chmasa, nimaga o'chmayotganini tushuntiringva fikringizni case2.yaml ga yozing.

Case #3. NodeSelector bilan ishlash. case3.yaml fayl yarating.

    3 ta worker, 1 ta controlplane dan iborat Kind cluster yarating. Yaratgan confingizni case3.yaml yozing.
    Har bir worker node ning labellarini tekshirib chiqing(e'tibor bering, har bir node da unikalniy label bor va shu label siza qo'l keladi), kubectl orqali va bu labellarni case3.yaml faylga save qiling.
    3 ta Deployment yarating va har bir Deployment yaratigan Podlarning, belgilangan worker node larda run bo'lishini ta'minlang
            image=nginx, Deployment nomi nginx, replicas=1. Bu Deployment yaratigan Podlar birinchi workerda run bo'lishi kerak. Manifestni case3.yaml faylga yozing.
            image=busybox, Deployment nomi busybox, replicas=2. Bu Deployment yaratigan Podlar ikkinchi workerda run bo'lishi kerak. Manifestni case3.yaml faylga yozing.
            image=wordpress, Deployment nomi wordpress, replicas=3. Bu Deployment yaratigan Podlar uchinchi workerda run bo'lishi kerak. Manifestni case3.yaml faylga yozing.
    kubectl orqali default namespace dagi Podlarni list qiling va ularni qaysi node larda run bo'layotgani ham ko'rsating (kubectl orqali). Chiqgan natijani case3.yaml ga save qiling.
    Yaratilgan case3.yaml faylini manga yuboring.

Case #4. NodeAffinity bilan ishlash. case4.yaml fayl yarating.

    3 ta worker, 1 ta controlplane dan iborat Kind cluster yarating. Yaratgan confingizni case4.yaml yozing.
    Har bir worker node ning labellarini tekshirib chiqing(e'tibor bering, har bir node da unikalniy label bor va shu label siza qo'l keladi), kubectl orqali va bu labellarni case4.yaml faylga save qiling.
    3 ta Deployment yarating va har bir Deployment yaratigan Podlarning, belgilangan worker node larda run bo'lishini ta'minlang. Buning uchun NodeAffinity ni ishlating.
            image=nginx, Deployment nomi nginx, replicas=1. Bu Deployment yaratigan Podlar birinchi workerda run bo'lishi kerak. Manifestni case4.yaml faylga yozing.
            image=busybox, Deployment nomi busybox, replicas=2. Bu Deployment yaratigan Podlar ikkinchi workerda run bo'lishi kerak. Manifestni case4.yamlfaylga yozing.
            image=wordpress, Deployment nomi wordpress, replicas=3. Bu Deployment yaratigan Podlar uchinchi workerda run bo'lishi kerak. Manifestni case4.yaml faylga yozing.
    kubectl orqali default namespace dagi Podlarni list qiling va ularni qaysi node larda run bo'layotgani ham ko'rsating (kubectl orqali). Chiqgan natijani case4.yaml ga save qiling.
    Yaratilgan case4.yaml faylini manga yuboring.

Case #5. NodeAntiAffinity bilan ishlash. case5.yaml fayl yarating.

    2 ta worker, 1 ta controlplane dan iborat Kind cluster yarating. Yaratgan confingizni case5.yaml yozing.
    Har bir worker node ning labellarini tekshirib chiqing (e'tibor bering, har bir node da unikalniy label bor va shu label siza qo'l keladi), kubectl orqali va bu labellarni case5.yaml faylga save qiling. Faqat labellarini, boshqa info ni save qilmang faylga.
    Deployment yarating va Deployment yaratigan Podlarning ikkinchi workerda run qilishini ta'minlang. Buning uchun NodeAntiAffinity ni ishlating. Deployment nomi nginx, replicas=1, image=nginx. Manifestni case5.yaml faylga yozing.
    kubectl orqali default namespace dagi Podlarni list qiling va ularni qaysi node larda run bo'layotgani ham ko'rsating (kubectl orqali). Chiqgan natijani case5.yaml ga save qiling.
    Yaratilgan case5.yaml faylini manga yuboring.

Case #6. Taint & tolerations bilan ishlash. case6.yaml fayl yarating.

    2 ta worker, 1 ta controlplane dan iborat Kind cluster yarating. Yaratgan confingizni case6.yaml yozing.
    Birinchi worker nodega, class=business:NoSchedule degan taint set qiling
    Ikkinchi worker nodega, class=economy:NoSchedule degan taint set qiling
    NGINX ning 3 ta kopiyasini yaratadigan myapp nomli Deployment manifest yozing va uni case6.yaml ga save qiling. O'zingiz xoxlagan label bering Deployment Podlariga. Yaratilgan Deployment ni clusterga apply qiling.
    default namespacega podlarni list qiling va myapp Deployment yaratgan podlarning statusini tekshiring. Agar Podlar RUNNING state da bo'lmasa, sababini yozing.
    myapp Deployment ni o'chiring clusterdan
    NGINX ning 3 ta kopiyasini yaratadigan myapp-business nomli Deployment manifest yozing va uni case6.yaml ga save qiling. Bu Deployment Podlari birinchi worker da run bo'lish imkonini beradigan toleration qo'shing.
    Busybox ning 2 ta kopiyasini yaratadigan myapp-economy nomli Deployment manifest yozing va uni case6.yaml ga save qiling. Bu Deployment Podlari ikkinchi worker da run bo'lish imkonini beradigan toleration qo'shing.
    kubectl orqali default namespace dagi podlarni list qiling (-owide bilan qaysi node da run bo'layotgaini ko'rish uchun) va chiqgan natijani case6.yaml ga yozing.
    Yaratilgan case6.yaml faylini manga yuboring.

Homework #10

Bu tasklarni o'zingizning laptop/serverda bajaring. Tasklarni boshlashdan oldin, 3 ta worker va 1 ta control-plane ga ega bo'lgan clusterni kind/minikube orqali yarating.
DaemonSet

    daemonetset.yaml fayl yarating va unda quyidagi DaemonSet obyektini yozing.

    ​​​​apiVersion: apps/v1
    ​​​​kind: DaemonSet
    ​​​​metadata:
    ​​​​  name: my-daemonset
    ​​​​spec:
    ​​​​  template:
    ​​​​    metadata:
    ​​​​      labels:
    ​​​​        app: my-app
    ​​​​    spec:
    ​​​​      containers:
    ​​​​      - name: my-container
    ​​​​        image: nginx:latest

    DaemonSet obyektini apply qiling

    ​​​​kubectl apply -f daemonset.yaml

    DaemonSet yaratilganini tekshirib ko'ring

    ​​​​kubectl get daemonSet my-daemonset

    DaemonSet tomonidan Podlar yaratilganini tekshirib ko'ring. DaemonSet Podlarni yaratishda, biz har bir Pod ga app=my-app labelni berishini so'raganiz. Buning uchun DaemonSet obyektini ko'rsangiz bo'ladi birinchi etapda. Ya'ni hozir biz Pod larni list qilganimizda, faqatgina app=my-app label ga ega bo'lgan Podlarni list qilamiz. -l ('label') degani.

    ​​​​kubectl get pods -l app=my-app

    DaemonSet tomonidan Podlar clusterdagi har bir Node da bittadan kopiyasi yaratilgani tekshirib ko'ring, -owide orqali.

    ​​​​kubectl get pods -l app=my-app -owide

ConfigMaps

    configmap.yaml nomli fayl ni quyidagi ConfigMap obyektining contenti bilan yarating:

    ​​​​apiVersion: v1
    ​​​​kind: ConfigMap
    ​​​​metadata:
    ​​​​  name: my-configmap
    ​​​​data:
    ​​​​  my-key: "Hello World!"

    ConfigMap ni apply qiling

    ​​​​kubectl apply -f configmap.yaml

    my-configmap nomli ConfigMap yaratilganini tekshirib ko'ring.

    ​​​​kubectl get configmap my-configmap

    my-configmap nomli ConfigMapnig kontentini tekshirib ko'ring

    ​​​​kubectl get configmap my-configmap -oyaml

    my-configmap nomli ConfigMapni datasini ishlatadigan Podni yarating. Buning uchun configmap-pod.yaml faylni quyidagi Pod manifesti bilan to'ldiring

    ​​​​apiVersion: v1
    ​​​​kind: Pod
    ​​​​metadata:
    ​​​​  name: my-pod
    ​​​​spec:
    ​​​​  containers:
    ​​​​    - name: my-container
    ​​​​      image: nginx:latest
    ​​​​      env:
    ​​​​        - name: MY_ENV_VAR
    ​​​​          valueFrom:
    ​​​​            configMapKeyRef:
    ​​​​              name: my-configmap
    ​​​​              key: my-key

    configmap-pod.yaml ni apply qiling

    ​​​​kubectl apply -f configmap-pod.yaml

    my-pod nomli Pod yaratilganini tekshirib ko'ring

    ​​​​kubectl get pods my-pod 

    my-pod nomli Podga exec qilib MY_ENV_VAR nomli environment variableni tekshirib ko'ring

    ​​​​kubectl exec -it my-pod -- env | grep MY_ENV_VAR
    ​​​​# YOKI
    ​​​​kubectl exec -it my-pod bash
    ​​​​echo $MY_ENV_VAR

Secret

    secret.yaml nomli faylni yarating va unda quyidagi Secret obyektining kontentini yozing

    ​​​​apiVersion: v1
    ​​​​kind: Secret
    ​​​​metadata:
    ​​​​  name: my-secret
    ​​​​type: Opaque
    ​​​​data:
    ​​​​  my-secret-key: anVkYS1oYW0teGF2c2l6LXBhcm9sCg==

    secret.yaml ni apply qiling

    ​​​​kubectl apply -f secret.yaml

    my-secret nomli Secret yaratilganini tekshirib ko'ring

    ​​​​kubectl get secrets my-secret

    my-secret nomli Secretning kontentini tekshirib ko'ring

    ​​​​kubectl get secret my-secret -oyaml

    my-secret nomli Secretning data qismini ishlatadigan Pod yarating. Quyidagi Pod manifestni secret-pod.yaml ga yozing

    ​​​​apiVersion: v1
    ​​​​kind: Pod
    ​​​​metadata:
    ​​​​  name: my-secret-pod
    ​​​​spec:
    ​​​​  containers:
    ​​​​    - name: my-container
    ​​​​      image: nginx:latest
    ​​​​      env:
    ​​​​        - name: MY_SECRET_ENV_VAR
    ​​​​          valueFrom:
    ​​​​            secretKeyRef:
    ​​​​              name: my-secret
    ​​​​              key: my-secret-key

    pod.yaml ni apply qiling

    ​​​​kubectl apply -f secret-pod.yaml

    my-secret-pod nomli Pod yaratilganini tekshirib ko'ring

    ​​​​kubectl get pods

    my-secret-pod nomli Podga exec qilib MY_SECRET_ENV_VAR nomli environment variableni tekshirib ko'ring

    ​​​​kubectl exec -it my-secret-pod -- env | grep MY_SECRET_ENV_VAR
    ​​​​# YOKI
    ​​​​kubectl exec -it my-secret-pod bash
    ​​​​echo $MY_SECRET_ENV_VAR

Select a repo
