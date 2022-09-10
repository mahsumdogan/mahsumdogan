- 👋 Hi, I’m @mahsumdogan
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
mahsumdogan/mahsumdogan is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
whatsapp 05432762600
instegram mahsumdgn72
facebook mahsum doğan
Birleştir
EV
HAKKINDA
BLOG
GÖSTERGE PANELİ
TARTIŞMALAR
DURUM
🧪Örnek Kurallar
➡️Başlarken
Kurulum
Yapılandırma
Birleştirme Çek Raporunu Anlama
Komutlarla Birleştirmeyi Kontrol Etme
🔖Yapılandırma Dosyası
Kullanılan Dosya
Biçim
Veri tipleri
🎯Koşullar
Dilbilgisi
Koşulları Operatörlerle Birleştirme
Öznitellikler
operatörler
Listeler Nasıl Eşleştirilir
Durum Kontrolleri Hakkında
Şube Koruması Hakkında
🚀Hareketler
atamak
destek
kapat
kopyalamak
yorum
delete_head_branch
reddet_reviews
Düzenle
etiket
birleştirmek
post_check
sıra
yeniden temel almak
request_reviews
gözden geçirmek
Güncelleme
squash
⚙️Komutlar
yeniden temel almak
Güncelleme
destek
kopyalamak
squash
yenilemek
sıra
sırayı kaldırmak
yeniden kuyruğa girmek
🧪Örnek Kurallar
✅CI çalıştığında ve incelemeleri onaylarken Otomatik Birleştirme
🗂Değiştirilmiş Dosyalara Göre Birleştirme
🏖Stabil Şubeler için Daha Az Katı Kurallar
🎬Birleştirmeyi Etkinleştirmek/Devre Dışı Bırakmak için Etiketleri Kullanma
⚡️Birleştirmeye Öncelik Vermek için Etiketleri Kullanma
🙅️ İstenen Tüm İncelemelerin Onaylanmasını Gerektirin
☑️Çekme İsteklerini Görev Listeleriyle Eşleştirme
🤖Botlar
🔌API
kimlik doğrulama
daha ileri gitmek
🎖rozet
gömme
Stiller
💬SSS
Mergify, şube koruma ayarlarım nedeniyle çekme isteğimi birleştiremiyor
Tüm koşullar doğru değilken Mergify neden çekme isteğimi birleştirmiş görünüyor?
🧪Örnek Kurallar
Mergify, birçok özel kural ve iş akışı tanımlamanıza olanak tanır. Kuralları tanımlamak için çok sayıda ölçüt mevcuttur: çekme isteği yazarı, temel dal, etiketler, dosyalar vb.

Bu bölümde, başlamanıza yardımcı olacak ve birçok yaygın kullanım örneğini kapsayacak birkaç örnek oluşturuyoruz.

✅CI çalıştığında ve incelemeleri onaylarken Otomatik Birleştirme

🗂Değiştirilmiş Dosyalara Göre Birleştirme

🏖Stabil Şubeler için Daha Az Katı Kurallar

🎬Birleştirmeyi Etkinleştirmek/Devre Dışı Bırakmak için Etiketleri Kullanma

⚡️Birleştirmeye Öncelik Vermek için Etiketleri Kullanma

🙅️ İstenen Tüm İncelemelerin Onaylanmasını Gerektirin

☑️Çekme İsteklerini Görev Listeleriyle Eşleştirme

🤖Botlar

✅CI çalıştığında ve incelemeleri onaylarken Otomatik Birleştirme
Bu bir klasik! Bu kural, sürekli entegrasyon sistemi çekme talebini doğruladığında ve bir insan tarafından gözden geçirildiğinde Mergify otomatik birleştirmeyi etkinleştirir.

pull_request_rules:
  - name: automatic merge for main when CI passes and 2 reviews
    conditions:
      - "#approved-reviews-by>=2"
      - check-success=Travis CI - Pull Request
      - base=main
    actions:
      merge:
        method: merge
Elbette, check-successhangi CI sistemini kullandığınızı yansıtmak için koşulu uyarlamanız gerekir.

Bu kuralı istediğiniz gibi değiştirebilirsiniz. Örneğin, work-in-progressbir çekme isteğinin onaylansa bile birleştirilmeye hazır olmadığını belirtmek gibi bir etiket kullanabilirsiniz:

pull_request_rules:
  - name: automatic merge for main when CI passes and 2 reviews and not WIP
    conditions:
      - "#approved-reviews-by>=2"
      - check-success=Travis CI - Pull Request
      - base=main
      - label!=work-in-progress
    actions:
      merge:
        method: merge
Yalnızca belirli bir üye tarafından onaylanmışsa, bir çekme isteğini birleştirmek isteyebilirsiniz. Bu nedenle böyle bir kural yazabilirsiniz:

pull_request_rules:
  - name: automatic merge for main when CI passes approved by octocat
    conditions:
      - approved-reviews-by=octocat
      - check-success=Travis CI - Pull Request
    actions:
      merge:
        method: merge
🗂Değiştirilmiş Dosyalara Göre Birleştirme
Yalnızca dokundukları dosyalara dayalı olarak bazı çekme isteklerini birleştirmeye karar verebilirsiniz. filesÖzniteliği, değiştirilmiş dosya listesine erişmek ve dosya #filessayısına erişmek için kullanabilirsiniz .

Bu ince ayar, Mergify'ın yalnızca bir komut dosyası veya linter tarafından doğrulanabilen veri dosyalarını birleştirmesini istediğinizde kullanışlıdır.

Aşağıdaki örnek yalnızca data.jsondeğiştirilirse ve çekme talebi Circle CI'nin doğrulama testlerini geçerse birleşir:

pull_request_rules:
  - name: automatic merge on CircleCI success if only data.json is changed
    conditions:
      - "check-success=ci/circleci: validate"
      - files=data.json
      - "#files=1"
    actions:
      merge:
        method: merge
Ayrıca, düzenli ifadeyi kullanarak kalıpları eşleştirebilirsiniz. Aşağıdaki kural, CI geçtiğinde ve tüm dosyalar src/dizinin içindeyken çekme isteklerini birleştirir:

pull_request_rules:
  - name: automatic merge on CircleCI success if only data.json is changed
    conditions:
      - "check-success=ci/circleci: validate"
      - -files~=^(!?src/)
    actions:
      merge:
        method: merge
🏖Stabil Şubeler için Daha Az Katı Kurallar
Bazı projeler, bakım dalları için daha kolay inceleme gereksinimlerine sahip olmak gibi. Bu genellikle, örneğin birleştirmek için 2 inceleme talep edilmesi main, ancak kararlı bir dal için yalnızca bir inceleme talep edilmesi anlamına gelir - çünkü bu çekme talepleri esasen main.

Bu durumda birleştirmeyi otomatikleştirmek için, bunlara bazı kurallar yazabilirsiniz:

pull_request_rules:
  - name: automatic merge for main when reviewed and CI passes
    conditions:
      - "check-success=ci/circleci: my_testing_job"
      - "#approved-reviews-by>=2"
      - base=main
    actions:
      merge:
        method: merge
  - name: automatic merge for stable branches
    conditions:
      - "check-success=ci/circleci: my_testing_job"
      - "#approved-reviews-by>=1"
      - base~=^stable/
    actions:
      merge:
        method: merge
🎬Birleştirmeyi Etkinleştirmek/Devre Dışı Bırakmak için Etiketleri Kullanma
Bazı geliştiriciler tam otomatik birleştirme konusunda rahat değiller - kodu birleştirmeden önce son bir söz söylemekten hoşlanıyorlar. Bu durumda, bir etiket kullanarak bir koşul ekleyebilirsiniz :

pull_request_rules:
  - name: automatic merge for main when reviewed and CI passes
    conditions:
      - check-success=Travis CI - Pull Request
      - "#approved-reviews-by>=2"
      - base=main
      - label=ready-to-merge
    actions:
      merge:
        method: merge
Çekme talebi 2 katılımcı tarafından onaylanır ve etiketi alır ready-to-be-mergedalmaz, çekme talebi Mergify tarafından birleştirilecektir.

Öte yandan, bazı geliştiriciler, bir etiketle otomatik birleştirme özelliğini devre dışı bırakma seçeneği istiyor. Bu, şu şekilde etiketlenmiş bir çekme isteğinin work-in-progressbirleştirilmemesi gerektiğini belirtmek için faydalı olabilir:

pull_request_rules:
  - name: automatic merge for main when reviewed and CI passes
    conditions:
      - check-success=continuous-integration/travis-ci/pr
      - "#approved-reviews-by>=2"
      - base=main
      - label!=work-in-progress
    actions:
      merge:
        method: merge
Bu durumda, bir çekme isteği ile etiketlenirse work-in-progress, 2 katılımcı tarafından onaylansa ve Travis CI'yi geçse bile birleştirilmez.

⚡️Birleştirmeye Öncelik Vermek için Etiketleri Kullanma
Premium Plan
Özelliği🦾
Kuyruk eylemini kullanırken ve birçok çekme isteği birleştirilmeyi beklerken, bazıları daha acil olabilir. Bu durumda, bir etiket kullanarak bir koşul ekleyebilir ve kuyruk eyleminin öncelik seçeneğini yapılandırabilirsiniz :

pull_request_rules:
  - name: automatic merge of 🚑 hotfix (high priority)
    conditions:
      - check-success=Travis CI - Pull Request
      - "#approved-reviews-by>=2"
      - base=main
      - label=🚑 hotfix
    actions:
      queue:
        method: merge
        priority: high
  - name: automatic merge of bot 🤖 (low priority)
    conditions:
      - author=dependabot[bot]
      - check-success=Travis CI - Pull Request
      - "#approved-reviews-by>=2"
      - base=main
    actions:
      queue:
        method: merge
        priority: low
  - name: automatic merge for main when reviewed and CI passes
    conditions:
      - check-success=Travis CI - Pull Request
      - "#approved-reviews-by>=2"
      - base=main
    actions:
      queue:
        method: merge
        priority: medium
Çekme talebi 2 katılımcı tarafından onaylanır onaylanmaz, çekme talebi birleştirme kuyruğuna eklenecektir. Birleştirme kuyruğunda, önce etiketli çekme istekleri birleştirilir. Dependabot'tan gelen çekme istekleri her zaman en son birleştirilir.🚑 hotfix

🙅️ İstenen Tüm İncelemelerin Onaylanmasını Gerektirin
İstenen tüm incelemeler onaylandıysa, o zaman sayısı review-requested0 olmalıdır. Yine de, en az bir olumlu inceleme olduğundan emin olmak istediğiniz için bu, birleşme için yeterli bir koşul değildir.

pull_request_rules:
  - name: merge when all requested reviews are valid
    conditions:
      - "#approved-reviews-by>=1"
      - "#review-requested=0"
      - "#changes-requested-reviews-by=0"
    actions:
        merge:
          method: merge
İstenen bir inceleme reddedilirse, birleştirmeyi önleyecek bir inceleme olarak sayılmayacaktır.

☑️Çekme İsteklerini Görev Listeleriyle Eşleştirme
GitHub Markdown , kullanıcıların çekme isteği gövdesinde görev listelerini kullanmalarına olanak tanır. Görev listeleri, yorumlarda tıklanabilir onay kutuları ile işlenir ve bunları eksiksiz veya eksik olarak işaretlemek için onay kutularını seçebilir veya seçimini kaldırabilirsiniz. Görev listeleri genellikle çekme isteği şablonlarında kullanılır .

../_images/tasklist.png
body Özniteliği ve normal ifadeleri kullanarak görev listelerini eşleştirmek için Birleştirme koşullarından yararlanabilirsiniz . Vücudunuz aşağıdaki Markdown'ı içeriyorsa, örneğin bir birleştirme yapmadan önce bu kutuların işaretlendiğinden emin olabilirsiniz.

[ ] Security has been checked
[ ] Changes have been documented
pull_request_rules
  - name: merge when checkboxes are checked
    conditions:
      - body~=(?m)^\[X\] Security has been checked
      - body~=(?m)^\[X\] Changes have been documented
      - check-success=my favorite ci
    actions:
      merge:
        method: merge
🤖Botlar
Bazı çekme istekleri, otomatik bağımlılık güncellemesi gönderenler gibi diğer araçlar tarafından otomatik olarak oluşturulabilir. Sürekli entegrasyon sisteminiz bunları doğruladığı sürece, bu çekme isteklerini manuel olarak incelemeye ve onaylamaya gerek olmadığına karar verebilirsiniz.

Aşağıdaki kurallar bu tür hizmetlere örnektir: sürekli entegrasyon sistemi tarafından doğrulanırsa bu güncellemeleri insan müdahalesi olmadan otomatik olarak birleştirmek için tasarlanmıştır. burada CI kontrol adı olarak kullanılır - ne kullanırsanız kullanın onu ayarlayın.Travis CI - Pull Request

bağımlı robot
Dependabot , GitHub otomatik güvenlik güncellemesinin arkasındaki bottur. Projenizin bağımlılıkları için güvenli olduklarından emin olmak için otomatik güncellemeler gönderir.

Bağımlı bot tarafından oluşturulan çekme isteğinin birleştirilmesini aşağıdaki gibi bir kuralla otomatikleştirebilirsiniz :

pull_request_rules:
  - name: automatic merge for Dependabot pull requests
    conditions:
      - author=dependabot[bot]
      - check-success=Travis CI - Pull Request
    actions:
      merge:
        method: merge
Alternatif olarak, yalnızca aynı ana sürüm içinse, bağımlı bot çekme isteği için otomatik birleştirmeyi de etkinleştirebilirsiniz .

pull_request_rules:
  - name: automatic merge for Dependabot pull requests
    conditions:
      - author=dependabot[bot]
      - check-success=Travis CI - Pull Request
      - title~=^Bump [^\s]+ from ([\d]+)\..+ to \1\.
    actions:
      merge:
        method: merge
Ek başlık tabanlı kural conditions, yalnızca 1.x'ten 1.y'ye güncellemelerin otomatik olarak birleştirildiğinden emin olun. 2.x'ten 3.x'e güncellemeler Mergify tarafından yok sayılır.

Snyk
Snyk , projenizin bağımlılıkları için otomatik güncellemeler gönderir.

pull_request_rules:
  - name: automatic merge for Snyk pull requests
    conditions:
      - title~=^\[Snyk\]
      - head~=^snyk-fix
      - check-success~=^security/snyk
    actions:
      merge:
        method: merge
Yenilemek
Renovate , projenizin bağımlılıkları için otomatik güncellemeler gönderir.

pull_request_rules:
  - name: automatic merge for Renovate pull requests
    conditions:
      - author=renovate[bot]
      - check-success=Travis CI - Pull Request
    actions:
      merge:
        method: merge
Requires.io
Requires.io , projenizin bağımlılıkları için otomatik güncellemeler gönderir (yalnızca Python'un paketleri).

pull_request_rules:
  - name: automatic merge for Requires.io pull requests
    conditions:
      - title~=^\[requires.io\]
      - head~=^requires-io
      - check-success=Travis CI - Pull Request
    actions:
      merge:
        method: merge
PyUp
PyUp , projenizin Python bağımlılıkları için otomatik güncellemeler gönderir.

pull_request_rules:
  - name: automatic merge for PyUp pull requests
    conditions:
      - author=pyup-bot
      - check-success=Travis CI - Pull Request
    actions:
      merge:
        method: merge
Depfu
Depfu , Ruby, JavaScript ve Elixir projenizin bağımlılıklarının yeni sürümleri hakkında sizi otomatik olarak bilgilendirir.

pull_request_rules:
  - name: automatic merge for Depfu pull requests
    conditions:
      - author=depfu[bot]
      - check-success=Travis CI - Pull Request
    actions:
      merge:
        method: merge
ImgBot
ImgBot , resimlerinizi optimize eder ve size zaman kazandırır.

pull_request_rules:
  - name: automatic merge for ImgBot pull requests
    conditions:
      - author=imgbot[bot]
      - check-success=Travis CI - Pull Request
    actions:
      merge:
        method: merge
© Copyright 2022, Birleştirme
